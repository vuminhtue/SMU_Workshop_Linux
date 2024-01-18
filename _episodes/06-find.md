---
title: "Finding Things"
teaching: 15
exercises: 0
questions:
- "How can I find things in files?"
objectives:
- "Use `grep` to select lines from text files that match simple patterns."
keypoints:
- "`grep` selects lines in files that match patterns."
- "`--help` is a flag supported by many bash commands, and programs that can be run from within Bash, to display more information on how to use these commands or programs."
---

In the same way that many of us now use "Google" as a 
verb meaning "to find", Unix programmers often use the 
word "grep".
"grep" is a contraction of "global/regular expression/print",
a common sequence of operations in early Unix text editors.
It is also the name of a very useful command-line program.

## Find matching filename using `find`

```
$ cd shell-lesson-data
$ find -name haiku*
# Find all files with prefix haiku
```
##
~~~
$ cd ~/shell-lesson-data/exercise-data/writing
$ nano haiku.txt
~~~

~~~
The Tao that is seen
Is not the true Tao, until
You bring fresh toner.

With searching comes loss
and the presence of absence:
"My Thesis" not found.

Yesterday it worked
Today it is not working
Software is like that.
~~~

Let's find lines that contain the word "not":

~~~
$ grep not haiku.txt
~~~

~~~
Is not the true Tao, until
"My Thesis" not found
Today it is not working
~~~

Here, `not` is the pattern we're searching for.
It's pretty simple:
every alphanumeric character matches against itself.
After the pattern comes the name or names of the files we're searching in.
The output is the three lines in the file that contain the letters "not".

Let's try a different pattern: "day".

~~~
$ grep day haiku.txt
~~~

~~~
Yesterday it worked
Today it is not working
~~~

This time,
two lines that include the letters "day" are outputted.
However, these letters are contained within larger words.
To restrict matches to lines containing the word "day" on its own,
we can give `grep` with the `-w` flag.
This will limit matches to word boundaries.

~~~
$ grep -w day haiku.txt
~~~


In this case, there aren't any, so `grep`'s output is empty. Sometimes we don't
want to search for a single word, but a phrase. This is also easy to do with
`grep` by putting the phrase in quotes.

~~~
$ grep -w "is not" haiku.txt
~~~


~~~
Today it is not working
~~~

We've now seen that you don't have to have quotes around single words,
but it is useful to use quotes when searching for multiple words.
It also helps to make it easier to distinguish between the search term or phrase
and the file being searched.
We will use quotes in the remaining examples.

Another useful option is `-n`, which numbers the lines that match:

~~~
$ grep -n "it" haiku.txt
~~~

~~~
5:With searching comes loss
9:Yesterday it worked
10:Today it is not working
~~~

Here, we can see that lines 5, 9, and 10 contain the letters "it".

We can combine options (i.e. flags) as we do with other Unix commands.
For example, let's find the lines that contain the word "the". We can combine
the option `-w` to find the lines that contain the word "the" and `-n` to number the lines that match:

~~~
$ grep -n -w "the" haiku.txt
~~~

~~~
2:Is not the true Tao, until
6:and the presence of absence:
~~~

Now we want to use the option `-i` to make our search case-insensitive:

~~~
$ grep -n -w -i "the" haiku.txt
~~~

~~~
1:The Tao that is seen
2:Is not the true Tao, until
6:and the presence of absence:
~~~

Now, we want to use the option `-v` to invert our search, i.e., we want to output
the lines that do not contain the word "the".

~~~
$ grep -n -w -v "the" haiku.txt
~~~

~~~
1:The Tao that is seen
3:You bring fresh toner.
4:
5:With searching comes loss
7:"My Thesis" not found.
8:
9:Yesterday it worked
10:Today it is not working
11:Software is like that.
~~~

`grep` has lots of other options. To find out what they are, we can type:

~~~
$ grep --help
~~~

You can also save it into a text file by redirecting the output: `history > logfile.txt`. You can also clear the history by typing `history -c`.

