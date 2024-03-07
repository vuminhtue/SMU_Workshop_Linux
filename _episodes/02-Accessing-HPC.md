---
title: "Accessing the SMU HPC Cluster"
teaching: 15
exercises: 0
questions:
- "How can I access the SMU HPC cluster from my local machine?"
objectives:
- "Logging into ManeFrame3/SuperPOD from a local Mac / Windows computer."
---

To be able to run commands on the M3/SuperPOD from your own machine,
you will first need to be able to log in to the M3/SuperPOD.
This is known as a *remote login*.

Open Visual Studio Code, and click on **Terminal** to open new terminal window:

![image](https://github.com/vuminhtue/SMU_Workshop_Linux/assets/43855029/6fb9bf06-78cb-4121-9122-232e31a23005)

~~~
ssh <your username>@superpod.smu.edu
ssh <your username>@m3.smu.edu
~~~
{: .bash}

When logged in, you are presented with a welcome message and the following "prompt":

~~~
[username@slogin-01 ~]$
~~~
{: .bash}

The prompt in a bash shell usually consists of a dollar (`$`) sign, and shows that the shell is waiting for input. The prompt may also contain other information: this prompt tells you `your username` and which node you are connected to - `slogin-01` is the "login" node.

It also tells you your current directory, i.e., `~`, which, as you will learn shortly,
is short for your *home* directory. We will mostly refer to the prompt as just `$`, i.e.,

~~~
$
~~~
{: .bash}

Let's enter our first command! 

Type the command `whoami`,
then press the Enter key (sometimes marked Return) to send the command to the shell.
The command's output is the ID of the current user.

~~~
$ whoami
~~~
{: .bash}
