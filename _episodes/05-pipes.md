---
title: "Pipes and Filters"
teaching: 15
exercises: 0
questions:
- "How can I combine existing commands to do new things?"
objectives:
- "Redirect a command's output to a file."
- "Process a file instead of keyboard input using redirection."
- "Construct command pipelines with two or more stages."
- "Explain what usually happens if a program or pipeline isn't given any input to process."
- "Explain Unix's 'small pieces, loosely joined' philosophy."
keypoints:
- "`cat` displays the contents of its inputs."
- "`head` displays the first few lines of its input."
- "`tail` displays the last few lines of its input."
- "`sort` sorts its inputs."
- "`wc` counts lines, words, and characters in its inputs."
- "`*` matches zero or more characters in a filename, so `*.txt` matches all files ending in `.txt`."
- "`?` matches any single character in a filename, so `?.txt` matches `a.txt` but not `any.txt`."
- "`command > file` redirects a command's output to a file."
- "`first | second` is a pipeline: the output of the first command is used as the input to the second."
- "The best way to use the shell is to use pipes to combine simple single-purpose programs (filters)."
---

Now that we know a few basic commands,
we can finally look at the shell's most powerful feature:
the ease with which it lets us combine existing programs in new ways.

For training purposes, let's use some data from the Software Carpentry workshop. We will download them using the GitHub interface and the `git clone` command. Let's put them inside the `linux_workshop` folder.

~~~
$ cd ~/linux_workshop
$ git clone https://github.com/silshack/pipes.git
~~~

This will create a folder called `pipes`, which will contain a subfolder called `molecules`. Lets's see its contents.

~~~
$ cd pipes
$ cd molecules
$ ls
~~~

~~~
cubane.pdb    ethane.pdb    methane.pdb
octane.pdb    pentane.pdb   propane.pdb
~~~
{: .output}


The folder `molecules` contains six files describing some simple organic molecules.
The `.pdb` extension indicates that these files are in Protein Data Bank format,
a simple text format that specifies the type and position of each atom in the molecule.

We can print out the contents of these files using the `cat` command. Let's print out `methane.pdb`:

~~~
$ cat methane.pdb
~~~
{: .bash}

~~~
COMPND      METHANE
AUTHOR      DAVE WOODCOCK  95 12 18
ATOM      1  C           1       0.257  -0.363   0.000  1.00  0.00
ATOM      2  H           1       0.257   0.727   0.000  1.00  0.00
ATOM      3  H           1       0.771  -0.727   0.890  1.00  0.00
ATOM      4  H           1       0.771  -0.727  -0.890  1.00  0.00
ATOM      5  H           1      -0.771  -0.727   0.000  1.00  0.00
TER       6              1
END
~~~
{: .output}

Now, I would like to introduce you to a command that could be very useful: `wc`, which stands for "word count" but it actually counts the number of lines, words, and characters in files. Let's apply it to `methane.pdb` and see what we get:

~~~
$ wc methane.pdb
~~~
{: .bash}

~~~
  9  57 431 methane.pdb
~~~
{: .output}

So, the file `methane.pdb` has nine lines, 57 words, and 431 characters. Now, let's apply the `wc` command to all six files that have the `.pdb` extension. We can run `wc` command six times, but thankfully, there is a way to do it with a single use of the `wc` command using the very useful feature of Linux called *wildcards*. Let me show you how it works:

~~~
$ wc *.pdb
~~~
{: .bash}

~~~
  20  156 1158 cubane.pdb
  12   84  622 ethane.pdb
   9   57  422 methane.pdb
  30  246 1828 octane.pdb
  21  165 1226 pentane.pdb
  15  111  825 propane.pdb
 107  819 6081 total
~~~
{: .output}

> ## Wildcards
>
> `*` is a **wildcard**. It matches zero or more
> characters, so `*.pdb` matches `ethane.pdb`, `propane.pdb`, and every
> file that ends with '.pdb'. On the other hand, `p*.pdb` only matches
> `pentane.pdb` and `propane.pdb`, because the 'p' at the front only
> matches filenames that begin with the letter 'p'. If you want to apply the command to all the 
> files in the folder, you can do `wc *`.
{: .callout}

If we run `wc -l` instead of just `wc`,
the output shows only the number of lines per file:

~~~
$ wc -l *.pdb
~~~
{: .bash}

~~~
  20  cubane.pdb
  12  ethane.pdb
   9  methane.pdb
  30  octane.pdb
  21  pentane.pdb
  15  propane.pdb
 107  total
~~~
{: .output}

We can also use `-w` to get only the number of words,
or `-c` to get only the number of characters.

Which of these files is shortest?
It's an easy question to answer when there are only six files,
but what if there were 6000?
Our first step toward a solution is to run the command:

~~~
$ wc -l *.pdb > lengths.txt
~~~
{: .bash}

The greater than symbol, `>`, tells the shell to **redirect** the command's output
to a file instead of printing it to the screen. (This is why there is no screen output:
everything that `wc` would have printed has gone into the
file `lengths.txt` instead.)  The shell will create
the file if it doesn't exist. If the file exists, it will be
silently overwritten, which may lead to data loss and thus requires
some caution.
`ls lengths.txt` confirms that the file exists:

~~~
$ ls lengths.txt
~~~
{: .bash}

~~~
lengths.txt
~~~
{: .output}

We can now send the content of `lengths.txt` to the screen using `cat lengths.txt`.

~~~
$ cat lengths.txt
~~~
{: .bash}

~~~
  20  cubane.pdb
  12  ethane.pdb
   9  methane.pdb
  30  octane.pdb
  21  pentane.pdb
  15  propane.pdb
 107  total
~~~
{: .output}

> ## Output Page by Page
>
> We'll continue to use `cat` in this lesson, for convenience and consistency,
> but it has the disadvantage that it always dumps the whole file onto your screen.
> More useful in practice is the command `less`,
> which you use with `$ less lengths.txt`.
> This displays a screenful of the file, and then stops.
> You can go forward one screenful by pressing the spacebar,
> or back one by pressing `b`.  Press `q` to quit.
{: .callout}

Now let's use the `sort` command to sort its contents.
We will also use the `-n` flag to specify that the sort is
numerical instead of alphabetical.
This does *not* change the file;
instead, it sends the sorted result to the screen:

~~~
$ sort -n lengths.txt
~~~
{: .bash}

~~~
  9  methane.pdb
 12  ethane.pdb
 15  propane.pdb
 20  cubane.pdb
 21  pentane.pdb
 30  octane.pdb
107  total
~~~
{: .output}

We can put the sorted list of lines in another temporary file called `sorted-lengths.txt`
by putting `> sorted-lengths.txt` after the command,
just as we used `> lengths.txt` to put the output of `wc` into `lengths.txt`.
Once we've done that,
we can run another command called `head` to get the first few lines in `sorted-lengths.txt`:

~~~
$ sort -n lengths.txt > sorted-lengths.txt
$ head -n 1 sorted-lengths.txt
~~~
{: .bash}

~~~
  9  methane.pdb
~~~
{: .output}

Using the parameter `-n 1` with `head` tells it that
we only want the first line of the file;
`-n 20` would get the first 20,
and so on.
Since `sorted-lengths.txt` contains the lengths of our files ordered from least to greatest,
the output of `head` must be the file with the fewest lines.

If you think this is confusing,
you're in good company:
even once you understand what `wc`, `sort`, and `head` do,
all those intermediate files make it hard to follow what's going on.
We can make it easier to understand by running `sort` and `head` together:

~~~
$ sort -n lengths.txt | head -n 1
~~~
{: .bash}

~~~
  9  methane.pdb
~~~
{: .output}

The vertical bar, `|`, between the two commands is called a **pipe**.
It tells the shell that we want to use
the output of the command on the left
as the input to the command on the right.
The computer might create a temporary file if it needs to,
or copy data from one program to the other in memory,
or something else entirely;
we don't have to know or care.

Nothing prevents us from chaining pipes consecutively.
That is, we can for example send the output of `wc` directly to `sort`,
and then the resulting output to `head`.
Thus we first use a pipe to send the output of `wc` to `sort`:

~~~
$ wc -l *.pdb | sort -n
~~~
{: .bash}

~~~
   9 methane.pdb
  12 ethane.pdb
  15 propane.pdb
  20 cubane.pdb
  21 pentane.pdb
  30 octane.pdb
 107 total
~~~
{: .output}

And now we send the output ot this pipe, through another pipe, to `head`, so that the full pipeline becomes:

~~~
$ wc -l *.pdb | sort -n | head -n 1
~~~
{: .bash}

~~~
   9  methane.pdb
~~~
{: .output}

This is exactly like a mathematician nesting functions like *log(3x)*
and saying "the log of three times *x*".
In our case,
the calculation is "head of sort of line count of `*.pdb`".

Here's what actually happens behind the scenes when we create a pipe.
When a computer runs a program --- any program --- it creates a **process**
in memory to hold the program's software and its current state.
Every process has an input channel called **standard input**.
(By this point, you may be surprised that the name is so memorable, but don't worry:
most Unix programmers call it "stdin".
Every process also has a default output channel called **standard output**
(or "stdout").

The shell is actually just another program.
Under normal circumstances,
whatever we type on the keyboard is sent to the shell on its standard input,
and whatever it produces on standard output is displayed on our screen.
When we tell the shell to run a program,
it creates a new process
and temporarily sends whatever we type on our keyboard to that process's standard input,
and whatever the process sends to standard output to the screen.

Here's what happens when we run `wc -l *.pdb > lengths.txt`.
The shell starts by telling the computer to create a new process to run the `wc` program.
Since we've provided some filenames as parameters,
`wc` reads from them instead of from standard input.
And since we've used `>` to redirect output to a file,
the shell connects the process's standard output to that file.

If we run `wc -l *.pdb | sort -n` instead,
the shell creates two processes
(one for each process in the pipe)
so that `wc` and `sort` run simultaneously.
The standard output of `wc` is fed directly to the standard input of `sort`;
since there's no redirection with `>`,
`sort`'s output goes to the screen.
And if we run `wc -l *.pdb | sort -n | head -n 1`,
we get three processes with data flowing from the files,
through `wc` to `sort`,
and from `sort` through `head` to the screen.

![Redirects and Pipes](../fig/redirects-and-pipes.png)

This simple idea is why Unix has been so successful.
Instead of creating enormous programs that try to do many different things,
Unix programmers focus on creating lots of simple tools that each do one job well,
and that work well with each other.
This programming model is called "pipes and filters".
We've already seen pipes;
a **filter** is a program like `wc` or `sort`
that transforms a stream of input into a stream of output.
Almost all of the standard Unix tools can work this way:
unless told to do otherwise,
they read from standard input,
do something with what they've read,
and write to standard output.

The key is that any program that reads lines of text from standard input
and writes lines of text to standard output
can be combined with every other program that behaves this way as well.
You can *and should* write your programs this way
so that you and other people can put those programs into pipes to multiply their power.

> ## Redirecting Input
>
> As well as using `>` to redirect a program's output, we can use `<` to
> redirect its input, i.e., to read from a file instead of from standard
> input. For example, instead of writing `wc ammonia.pdb`, we could write
> `wc < ammonia.pdb`. In the first case, `wc` gets a command line
> parameter telling it what file to open. In the second, `wc` doesn't have
> any command line parameters, so it reads from standard input, but we
> have told the shell to send the contents of `ammonia.pdb` to `wc`'s
> standard input.
{: .callout}


> ## Pipe Reading Comprehension
>
> A file called `animals.txt` contains the following data:
>
> ~~~
> 2012-11-05,deer
> 2012-11-05,rabbit
> 2012-11-05,raccoon
> 2012-11-06,rabbit
> 2012-11-06,deer
> 2012-11-06,fox
> 2012-11-07,rabbit
> 2012-11-07,bear
> ~~~
> {: .source}
>
> What text passes through each of the pipes and the final redirect in the pipeline below?
>
> ~~~
> $ cat animals.txt | head -n 5 | tail -n 3 | sort -r > final.txt
> ~~~
> {: .bash}
{: .challenge}

> ## Pipe Construction
>
> For the file `animals.txt` from the previous exercise, the command:
>
> ~~~
> $ cut -d , -f 2 animals.txt
> ~~~
> {: .bash}
>
> produces the following output:
>
> ~~~
> deer
> rabbit
> raccoon
> rabbit
> deer
> fox
> rabbit
> bear
> ~~~
> {: .output}
>
> What other command(s) could be added to this in a pipeline to find
> out what animals the file contains (without any duplicates in their
> names)?
{: .challenge}

> ## Which Pipe?
>
> A file called animals.txt contains 586 lines of data formatted as follows:
>
> ~~~
> 2012-11-05,deer
> 2012-11-05,rabbit
> 2012-11-05,raccoon
> 2012-11-06,rabbit
> ...
> ~~~
> {: .output}
>
> What command would you use to produce a table that shows
> the total count of each type of animal in the file?
>
> 1.  `grep {deer, rabbit, raccoon, deer, fox, bear} animals.txt | wc -l`
> 2.  `sort animals.txt | uniq -c`
> 3.  `sort -t, -k2,2 animals.txt | uniq -c`
> 4.  `cut -d, -f 2 animals.txt | uniq -c`
> 5.  `cut -d, -f 2 animals.txt | sort | uniq -c`
> 6.  `cut -d, -f 2 animals.txt | sort | uniq -c | wc -l`
{: .challenge}

> ## Appending Data
>
> Consider the file `animals.txt`, used in previous exercise. 
> After these commands, select the alternative that 
> corresponds the file `animalsUpd.txt`:
>
> ~~~
> $ head -3 animals.txt > animalsUpd.txt
> $ tail -2 animals.txt >> animalsUpd.txt
> ~~~
> {: .bash}
> 
> 1. The first three lines of `animals.txt`
> 2. The last two lines of `animals.txt`
> 3. The first three lines and the last two lines of `animals.txt`
> 4. The second and third lines of `animals.txt`
{: .challenge}