---
title: "Working With Files and Directories"
teaching: 15
exercises: 0
questions:
- "How can I create, copy, and delete files and directories?"
- "How can I edit files?"
objectives:
- "Create files in that hierarchy using an editor or by copying and renaming existing files."
- "Display the contents of a directory using the command line."
- "Delete specified files and/or directories."
keypoints:
- "`cp old new` copies a file."
- "`mkdir path` creates a new directory."
- "`mv old new` moves (renames) a file or directory."
- "`rm path` removes (deletes) a file."
- "`rmdir path` removes (deletes) an empty directory."
- "The shell does not have a trash bin: once something is deleted, it's really gone."
---


# Creating thing
## Create new directory

The next command we will discuss is `mkdir`, which creates a new directory. Let's create a directory with the name `linux_workshop` inside shell-lesson-data:

~~~
$ cd $HOME/shell-lesson-data
$ mkdir linux_workshop
~~~
{: .bash}

Now, if you type `ls`, you should see `linux_workshop` lited among the contents of your home directory. 

~~~
$ cd linux_workshop
~~~
{: .bash}

Now, our current directory is `linux_workshop`:
~~~
$ pwd
~~~
{: .bash}

If you type `ls`, you won't see anything, because we have just created this directory and it is empty.

To go back to your home directory, you need to go one level up on the directory tree. There is a shortcut in the shell to move up one directory level
that looks like this: 

~~~
$ cd ..
~~~
{: .bash}

`..` is a special directory name meaning "the directory containing this one", or more succinctly,
the **parent** of the current directory.

The special directory `..` doesn't usually show up when we run `ls`.  If we want 
to display it, we can give `ls` the `-a` flag:

~~~
$ ls -F -a
~~~
{: .bash}


`-a` stands for "show all", including hidden files/folders;
it forces `ls` to show us file and directory names that begin with `.`,
such as `..` (which in our case is the `/home` directory).
As you can see, it also displays another special directory that's just called `.`,
which means "the current working directory".
It may seem redundant to have a name for it, but we'll see some uses for it soon.

> ## Good Names for Files and Directories
>
> Complicated names of files and directories can make your life very painful
> when working on the command line. Here we provide a few useful
> tips for the names of your files from now on.
>
> 1. Don't use whitespaces.
>
>    White spaces can make a name more meaningful
>    but since whitespace is used to break arguments on the command line
>    is better to avoid them on name of files and directories.
>    You can use `-` or `_` instead of whitespace.
>
>
>    Commands treat names starting with `-` as options.
>
> 2. Stay with letters, numbers, `.`, `-` and `_`.
>
> 3. Don't begin the name with `-`.
>   
>
> If you need to refer to names of files or directories that have whitespace
> or another non-alphanumeric character you should put quotes around the name.
{: .callout}


## Create new file


> ## Which Editor?
>
> When we say, "`nano` is a text editor," we really do mean "text": it can
> only work with plain character data, not tables, images, or any other
> human-friendly media. We use it in examples because almost anyone can
> drive it anywhere without training, but please use something more
> powerful for real work. On Unix systems (such as Linux and Mac OS X),
> many programmers use [Emacs](http://www.gnu.org/software/emacs/) or
> [Vim](http://www.vim.org/) (both of which are completely unintuitive,
> even by Unix standards), or a graphical editor such as
> [Gedit](http://projects.gnome.org/gedit/). On Windows, you may wish to
> use [Notepad++](http://notepad-plus-plus.org/).  Windows also has a built-in 
> editor called `notepad` that can be run from the command line in the same 
> way as `nano` for the purposes of this lesson.  
>
> No matter what editor you use, you will need to know where it searches
> for and saves files. If you start it from the shell, it will (probably)
> use your current working directory as its default location. If you use
> your computer's start menu, it may want to save files in your desktop or
> documents directory instead. You can change this by navigating to
> another directory the first time you "Save As..."
{: .callout}


### Using touch command

**touch** command will create new file instantly:

```
$ cd linux_workshop
$ touch file1.txt
$ ls
```

### Using nano command
**nano** is used to create text file very easily.
All the commands inside nano are introduced below with **^** stands for **Ctrl** button

```
$ nano file2.txt
```

![image](https://github.com/vuminhtue/SMU_Workshop_Linux/assets/43855029/f5d38e06-72bd-4040-94b1-1f2928c5d1e6)

### Using vim command
**vim** editor is a little bit more complicated to create a file with content:

```
vim file3.txt
```

### Using emacs command 

```
emacs file4.txt
```

![image](https://github.com/vuminhtue/SMU_Workshop_Linux/assets/43855029/a5814109-9c36-487e-a8cb-3c7edb4afb7a)
Hint: F10 to go to emacs virtual menu dropdown

## Removing files and folders:


This command removes files (**rm** is short for "remove").
which tells us that our file is gone:

### Removing file

~~~
$ ls
$ rm file1.txt
$ ls
~~~
{: .bash}

### Removing folder
Using recursive **-r** flag:

```
$ mkdir test1
$ ls
$ rm -r test1
$ ls
```

## Copy the file

File can be copied using **cp** command:

```
$ cp file2.txt file2cp.txt
```

## Rename the file

To rename the file, we can use the **mv** command, which stands for "move". The same command is used to move a file from one folder to another. Let's rename `draft.txt` to `quotes.txt`: 

~~~
$ mv file2.txt file2mv.txt
~~~
{: .bash}


