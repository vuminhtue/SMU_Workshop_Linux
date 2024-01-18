---
title: "Navigating"
teaching: 15
exercises: 0
questions:
- "How can I move files around?"
- "How can I see what files and directories I have?"
- "How can I specify the location of a file or directory on my computer?"
objectives:
- "Explain the similarities and differences between a file and a directory."
- "Translate an absolute path into a relative path and vice versa."
- "Construct absolute and relative paths that identify specific files and directories."
keypoints:
- "The file system is responsible for managing information on the disk."
- "Information is stored in files, which are stored in directories (folders)."
- "Directories can also store other directories, which forms a directory tree."
- "`cd path` changes the current working directory."
- "`ls path` prints a listing of a specific file or directory; `ls` on its own lists the current working directory."
- "`pwd` prints the user's current working directory."
- "`whoami` shows the user's current identity."
- "`/` on its own is the root directory of the whole file system."
- "A relative path specifies a location starting from the current location."
- "An absolute path specifies a location from the root of the file system."
- "'..' means 'the directory above the current one'; '.' on its own means 'the current directory'."
---

# Navigation

The part of the operating system responsible for managing files and directories
is called the **file system**. It organizes our data into files, which hold information,
and directories (also called "folders"), which hold files or other directories.

You need to be able to navigate without a Graphical User Interface (GUI). Unix file systems are trees with the roots at the top:

![image](https://github.com/vuminhtue/SMU_Workshop_Linux/assets/43855029/fa2cb24d-750b-42e2-a9ec-957362281d00)

The first command that we will look at is called `pwd` (**print working directory**). Let's type it in your VSCode Terminal once logged in:

~~~
$ pwd
~~~

Now let's download the sample data from [here](https://swcarpentry.github.io/shell-novice/data/shell-lesson-data.zip) using **wget** command:

```
$ wget https://swcarpentry.github.io/shell-novice/data/shell-lesson-data.zip
```

Once downloaded the zip file to your home directory on SuperPOD, you can unzip it using command **unzip**:

```
$ unzip shell-lesson-data.zip
```

We can see what's in our the downloaded directory by running command **ls**, which stands for "listing":

~~~
$ ls shell-lesson-data
~~~
Tips: you can try the feature called **Auto completion** in linux using **Tab** button by typying:

```
$ ls sh (tab)
```

Now let change the current prompt into the folder that just unzipped using **cd** command:

```
$ cd shell-lesson-data
```

`ls` prints the names of the files and directories in the current directory in alphabetical order,
arranged neatly into columns. 
We can make its output more comprehensible by using the **flag** `-F`, which tells `ls` to add a trailing `/` to the names of directories:

~~~
$ ls -F
~~~
{: .bash}

And note that there is a space between `ls` and `-F`:
without it, the shell thinks we're trying to run a command called `ls-F`, which doesn't exist.

Now let try **ls -l** stands for long listing, we check the content of the folder named **exercise-data**:

```
$ ls -l exercise-data/
```

![image](https://github.com/vuminhtue/SMU_Workshop_Linux/assets/43855029/622f51f5-18c3-441a-a4d2-175da8365227)


`ls` has lots of other options. To find out what they are, we can type:

~~~
$ ls --help
~~~

For more information on how to use `ls` we can type `man ls`.
`man` is the Unix "manual" command:
it prints a description of a command and its options,
and (if you're lucky) provides a few examples of how to use it.

```
$ man ls
```

To navigate through the `man` pages,
you may use the up and down arrow keys to move line-by-line,
or try the "b" and spacebar keys to skip up and down by full page.
Quit the `man` pages by typing "q".

We can also use `ls` to see the contents of a different directory. Let's list the directories of all the SuperPOD users (note that you cannot actually go inside other people's directories):  
~~~
$ ls /home
~~~
{: .bash}

Note that on SuperPOD you cannot access other people's directories. 

> ## Other Hidden Files
> 
> In addition to the hidden directories `..` and `.`, you may also see a file
> called `.bash_profile`. This file usually contains shell configuration
> settings. You may also see other files and directories beginning
> with `.`. These are usually files and directories that are used to configure
> different programs on your computer. The prefix `.` is used to prevent these
> configuration files from cluttering the terminal when a standard `ls` command
> is used.
{: .callout}


These  are the basic commands for navigating the filesystem on your computer: 
`pwd`, `ls` and `cd`.  Let's explore some variations on those commands.  What happens 
if you type `cd` on its own, without giving 
a directory?  

~~~
$ cd
~~~
{: .bash}

How can you check what happened?  `pwd` gives us the answer!  

~~~
$ pwd
~~~
{: .bash}

It turns out that `cd` without an argument will return you to your home directory, 
which is great if you've gotten lost in your own filesystem.  

If we want to move up one level from the shell directory, we could use `cd ..`.  But 
there is another way to move to any directory, regardless of your 
current location.  

> ## Few More Shortcuts
>
> The shell interprets the character `~` (tilde) at the start of a path to
> mean "the current user's home directory". For example, `~/shell-lesson-data` is equivalent to
> `/users/<your SuperPOD username>/shell-lesson-data`.
>
> In addition, you can also use **$HOME** as the shortcut to your home directory:
> 
> Another shortcut is the `-` (dash) character.  `cd` will translate `-` into
> *the previous directory I was in*, which is faster than having to remember, 
> then type, the full path.  This is a *very* efficient way of moving back 
> and forth between directories. The difference between `cd ..` and `cd -` is 
> that the former brings you *up*, while the latter brings you *back*. 
{: .callout}
