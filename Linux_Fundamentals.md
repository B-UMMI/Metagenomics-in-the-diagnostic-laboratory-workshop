---
Author: "C I Mendes" \
Date: "October, 2018" 
---

## Linux Fundamentals

Welcome to the world of Bash! In this section we'll introduce you to bash (the standard Linux shell) and show you how
to take advantage of standard commands like *ls*, *cp* and *mv*. We'll cover hard and symbolic links, pipes and 
redirection, and a also a few tools like *htop* that exist to make your life easier.

This part is ideal for those who are new to Linux (or any other Unix system), or those who want to review or improve
fundamental concepts. 

Commands you can run on the shell show up `$ like so` and `<file_name>` should be replace with whatever is appropriate.


#### What is the Shell and Why do you need it?

All the Linux operating systems (OS) are built on [Unix](https://en.wikipedia.org/wiki/Unix), an open-source operating 
system.

A computer's [Shell](https://en.wikipedia.org/wiki/Unix_shell) is a direct way to access an OS's functions through a 
text-interface, often called the "command line” or "terminal". Besides the regular functions of opening files, creating 
folders, moving or removing both, it allows for more complex interactions with the hardware to automate complex tasks. 

The most commonly used Shell is called [bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell)). You can check what 
shell you're using by running the command `echo $SHELL`

Why should you use it?

1. Shells can do many things GUI's can't, from a parallelised BLAST run analysis to complex interactions between 
different tools. 

2. Shells let you automate otherwise time-consuming tasks. 


#### First Commands


###### Where am I? Where do I go?

To start navigating in your OS through the terminal you first need to learn the appropriate shell commands.
First, it's good to know where you are. 

`$ pwd`

If you enter the command "pwd", meaning present working directory, it will output the path of your current location.
A bash session usually starts at the home directory, also called *$HOME*.

The path, describing a location in your computer system, can be absolute, like what *pwd* outputs, or relative to 
your current location. 
 
 The path is also the argument to the *cd* command. This command allows you to change your current working directory.
 
 `$ cd <directory_path>` OR  `$ cd /absolute/path/to/directory`
 
 
```
 Note: All the directories on the system form a tree, and / is considered the top of this tree, or the root.
```

Relative paths may contain one or more  *..*, signifying the parent directory. So, if you want to return to the
directory before your current one, you just have to do the command:

`$ cd ..`

If you want to return to your home directory, all you have to do is use the *~* character.

`$ cd ~` OR `$ cd`

Another special directory that you can use with *cd* is the *.*, which means "the current directory". This can be
ignored when using the *cd* command, but it's often used to execute some program in the current directory.

`$ cd ./<some_directory>`

`$ ./my_program`

###### What's in here?

To list the contents of a given, or your current, directory, you can use the command *ls*. This command has a
multitude of modifiers. The most useful are *-l*, to show the output in full list form, and *-a* to show hidden folders
and files.  

`$ ls -la .` OR `$ ls <Directory>` OR `$ ls /absolute/path/`

```
To see the options and modifiers of any command, use the *man* funcion. For example, `man ls`. 

```

###### Creating something new!

The *mkdir* command can be used to create a new directory.  The following example created a directory called *test* 
in the home directory:

`$ mkdir $HOME/temp`

To create a file you can use the *touch* command, or alternatively the *nano* program to create a file and
add text to it or edit and existing file. 

`$ touch <some_file>` OR `$ nano <other_file>`

To see the contents of a file you can use the *less* command, or the *head* and *tail* commands to see the top and 
bottom lines of a file.

`$ less <some_file>` OR `$ head <some_file>` OR `$ tail <some_file>`

The *cat* command displays the contents of a file on the terminal.

`$ cat <some_file>`

###### Copying and moving

The *cp* command allows you to copy items, like folders and files, to other locations. When moving folders, the `-r`
flag needs to be used to tell the command to move all the contents inside the folder recursively. 

`$ cp /path/to/file .`

`$ cp -r Data/ ~`

The *mv* command can do two things: it can move items to other paths or it can rename items. In the example, we've
renamed the *textA.txt* file to *textB.txt* and then we move it to the Documents directory in the *$HOME*.

`$ mv textA.txt textB.txt`

`$ mv textB.txt ~/Documents`


###### How do I delete things?

To remove a file or a directory you can use the *rm* command, but be aware that once an item is removed, it's gone 
forever!

`$ rm <file>` OR `$ rm -r <directory>`


###### The wild-card game

There may be many many times when you need to do a certain single operation repeatedly on many items. In these
situations, instead of having to type in many files in the command line, you can take advantage of Linux's built-in
wild card support. 

If you want to see all the text files in your current directory, you can do the following command.

`$ ls *.txt`

The * wildcard matches any character or sequence of characters. 

If you want to remove a sequence of files, you can do the following command, and it will remove all the files that
are numbered between 1 and 4 in the current directory. 

`$ rm file[1-4].txt` as alternative to `$ rm file1.txt file2.txt file3.txt file4.txt`

If you want to remove just the files numbered 1 and 2, you can do:

`$ rm file[1,2].txt`

###### Creating and removing links

In simple terms, a link is a connection to a given item in your system. Instead of copying a file, we can simply create
a link that points to that file original location, and use it as if you had copyied the file to the new location.

There's two kinds of links, hard and symbolic. We'll only mention symbolic links, but you can learn more about hard
links with the command `$man ln`.

The symbolic link, also called symlink, is a special file type where the link refers to another file by name.
Symlinks do not prevent a file from being deleted; if the target file disappears, then the symlink will just 
be unusable, or broken. 

Symlinks can ve created by passing the -s option to *ln*.

`$ ln -s ~/somefile.txt .`
 
When listing the contents of a directory with symlinks, the target filename is indicated preceded by a *->*. 
 
 
#### What else is out there

There are many useful programs that facilitate working on a Linux system. One of the most used tools is *wget* or
*curl*. These commands allow to retrieve files using the most widely-used Internet protocols, 

`$ curl <link_address>` OR `$ wget <link_address>`

The *Pipe* (|) allows you to take one command's output and use it as the input for another

*Htop* allows you to monitor the usage of resources in your machine.


```
Note: Package managers, like apt and brew, will install software and their dependencies into your machine. If 
you're in a ubuntu/debian OS, you can do *apt-get install <package>*. 
```

 
#### Useful material

- https://www.funtoo.org/Linux_Fundamentals,_Part_1
- https://dev.to/maxwell_dev/the-shell-introduction-i-wish-i-had-551k
- https://learncodethehardway.org/unix/bash_cheat_sheet.pdf



