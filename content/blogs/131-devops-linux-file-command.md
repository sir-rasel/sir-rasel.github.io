---
title: "DevOps - Step By Step Learning : Part 8 (Linux Command for File, Directory and Text Manipulation)"
description: "Let's learn the fundamental DevOps concepts!"
date: "2026-02-20T00:00:00Z"
tags: ["devops" , "linux"]
draft: false
showtoc: false
tocOpen: false
hidemeta: false
comments: true
disableHLJS: false
disableShare: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowCodeCopyButtons: true
cover:
    image: "img/blogs/131-devops-linux-file-command.jfif"
    caption: "DevOps Linux File Manipulation Commands"
    alt: "DevOps Linux File Manipulation Commands"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 7:** [DevOps - Step By Step Learning : Part 7 (Understand Linux Kernel, Boot Process and Filesystem Hierarchy)]({{< ref "blogs/130-devops-linux-kernel-boot-file-system.md" >}})
---

{{< figure
    src="/img/blogs/131-devops-linux-file-command.jfif"
    caption="DevOps Linux File Manipulation Commands (Photo Credit: Unsplash)"
    align=center
>}}

## Story:

Rasel grabbed the knowledge and understanding about the Linux kernel, how it boots, and the Linux file system. As the server runs mostly using CLI and no UI like Windows, so Rasel now wanted to learn the commands that help to work with files and directories. Like commands that are used for file and directory creation and content in its manipulation.

* * *

## Basic Structure of a Command:

The general structure of a Linux command line looks like:

```bash
command [-flag(s)] [-option(s) [value]] [argument(s)]
```
- **command** - is an executable file or program to be run/execute. Like: cd, ls, cat.
- **flag** - A short switch (usually with \-) that modifies the command’s behavior. Like: -l.
- **option** - Like a flag, but often with a value or longer form. Like: --sort=time.
- **argument** - The target on which the command operates. Like: a file or directory name.

* * *

## Helper Commands:

Linux has some helper commands which helps to find and understand other command, in case need clarifications or clues. Some of the most common of them are:

```bash
[command] --help
```
This gives description and prototype of a command.

```bash
man [command]
```
This gives manual of a command.

```bash
whatis [command]
```
This gives single line description of a command.

```bash
apropos [keyword]
```
This gives possible command with the given keyword.

Example:
```bash
cp --help 
man cp
whatis ls
apropos cd        
```

* * *

## Directory Related Commands:

Linux has some basic commands which helps to create, rename, delete and move directories. Means command that help to work with directory. Some of them are:

```bash
mkdir [directory name]
```
This create a new directory with the given name.

```bash
cd [directory name]
```
This checkout into the given directory name.

```bash
pwd
```
This print or give current working directory.

```bash
rmdir [directory name]
```
This remove or delete the directory with given name.

```bash
mv [source directory] [destination directory]
```
This move source directory to the given destination directory. Interestingly this command is also used for rename as well.

Example:
```bash
mkdir newFolder
cd newFolder
pwd
mv newFolder oldFolder
rmdir oldFolder        
```

* * *

## File Related Commands:

Linux has commands which helps to create, rename, delete and move files. Means command that help to work with file. Some of them are:

```bash
file [file name]
```
This command gives the file type of the given file.

```bash
touch [file name]
```
This command create a new file with the given name.

```bash
rm [file name]
```
This command remove or delete the file with given name.

```bash
mv [source file path] [destination file path]
```
This command move the file source file to the destination. This also used for rename as well.

Example:
```bash
touch a.txt
file a.txt
mv a.txt b.txt
rm b.txt        
```

* * *

## File and Directory Structure Explore and Visit Commands:

Linux has commands which helps to explore the file and directory structures. Also help to locate and jump from one to another location. Some of them are:

```bash
tree
```
This command gives the tree of the file and directory relationship.

```bash
ls
```
This command gives the file and directory list.

```bash
cd [directory]
```
This command checkout into the given directory name.

Example:
```bash
tree
ls
cd folder
```

* * *

## File Content Related Commands:

Linux has commands which helps to work with file content. Means manipulating a file. Some of them are:

```bash
cat [file name]
```
This command view the full content of file with the given name.

```bash
head [file name]
```
This command view the first 10 lines content of file with the given name.

```bash
tail [file name]
```
This command view the last 10 lines content of file with the given name.

```bash
cat > [file name]
```
This command start inserting for content to file with the given name.

```bash
cp [source file path] [destination file path]
```
This command copy the file source file to the destination.

```bash
find . -name "*.log"
```
This command find files with the given regex.

```bash
grep "*error" [file name]
```
This command find content with the given regex within given file name.

```bash
sed 's/before/after/g' [file name]
```
This command replace content before with after of given file name.

Other command as well like, **sort** for sorting content, **uniq** for getting unique content, **cut** for getting split column content etc.

Example:
```bash
cat a.txt
cat > a.txt
head a.txt
tail a.txt
sed 's/before/after/g' a.txt
grep "*error" a.txt        
```

* * *

## Working With Vim:

**Vim** is an advanced text editor based on the older vi. It's keyboard-driven, super fast, and works inside the terminal, perfect for server environments.

Vim has 3 main mode:

1.  **Normal Mode (Default)**: Navigate and issue commands (Esc key)
2.  **Insert Mode**: Insert text (like typing normally) (Press i, I, a etc.)
3.  **Command Mode**: Save, quit, search, etc. (Press : from Normal)

```bash
vim [file name]
```
This command open the file for working with the given name.

***Vim Summary***:

- Open file - vim filename
- Insert mode - i, a, o, O
- Save + Quit - :wq or ZZ
- Quit without saving - :q!
- Search - /pattern then n / N
- Replace all - :%s/old/new/g
- Copy/Cut/Paste - yy, dd, p
- Undo / Redo - u, Ctrl + r
- Go to line - :line_number or G / gg

* * *

## Summary:

In Linux, working with files and directories is an essential skill for DevOps. You can create files using touch and directories using mkdir. To view or organize them, you use commands like ls, cp to copy, mv to move or rename, and rm to delete. To view file content, you use cat, less, head, and tail, while tools like vim help you edit files directly from the terminal. Searching inside files can be done with grep, and locating files can be done with find. For text manipulation, you use commands like cut, sed, sort, uniq to extract, modify, or organize text data.