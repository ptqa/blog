---
title: "The mystery of docker & .pyc"
date: 2019-08-13T04:05:41+03:00
---
## Docker containers are the same, right?
Once upon a time developers showed me strange problem. There were trying to obfuscate python code by compiling .py files (python code) to .pyc files (python compiled bytecode) the problem was that client could not run this .pyc files although it worked on dev host (work on my machine). Turns out that devs were trying to run .pyc file like this:
```
$ chmod +x /app/run.pyc
$ /app/run.pyc
```

It worked fine on their host and assuming all docker containers are the same it should work the same on client host when he runs same container. But it was not the case, client was getting error like:
```
$ /app/run.pyc
pyc: line 1: $'3\r\r': command not found
```

Looks like system is trying to interpret this file as bash script and looking for shabang. Devs already checked all ENV variables and it was identical. SHA256 sums of images were identical. 
## Strace time
Dunno what is happening? Run strace and see what linux is doing to your files! Strace on dev host:
```
$ strace -f /app/run.pyc
execve("/app/run.pyc..., 0x7ffc9cdaf9f8 /* 77 vars */) = 0
```

Strace on client host
```
$ strace -f /app/run.pyc
execve("/app/run.pyc..., 0x7ffc9cdaf9f8 /* 77 vars */) = -1 ENOEXEC (Exec format error)
```

Ok, so problem with this system call `execve`. For some reason it returns 0 inside one container and returns -1 error inside another. 

## it's not docker, it's kernel

Syscall is a way to access kernel via user space and all docker containers share kernel with host machine. That's why we observer different behaviour on the same docker container, although whole environment is the same kernel is different. But what's different about it?

Docs about execve() have the following:

> execve() executes the program referred to by pathname. ... pathname must be either a binary executable, or a script starting with a line of the form:  #!interpreter [optional-arg]

So we need to make kernel think that our .pyc file is binary executable. But wait, isn't ELF the only executable binary format we have in linux? Is our file ELF?

```
$ readelf -h /app/run.pyc
readelf: Error: Not an ELF file - it has the wrong magic bytes at the start
```

The answer is no and no.

## Binfmt

To determine what file format we have kernel tries to read it's magic number which is `0x7F` for ELF. But as you can imagine there are various cases (virtualization, crosscompilation, etc) when you want provide some other binary format. That's why in lunux kernel devs added system called `binfmt` that allows you to add customer binary format (customer magic numbers) and specify how to run it.


You can register custom binary format using virtual file `/proc/sys/fs/binfmt_misc/register` and there is a package binfmt-support that does it for you for popular stuff including python & java. Installing this package solves the issue for client. Although I would never recommend running python or java this way since you often don't have access to host system and/or you can't control kernel configuration.



