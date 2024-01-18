---
title: "Introducing the Shell"
teaching: 15
exercises: 0
questions:
- "What is a command shell?"
objectives:
- "Explain how the shell relates to the keyboard, the screen, the operating system, and users' programs."
- "Explain when and why command-line interfaces should be used instead of graphical interfaces."
---
## What is UNIX/Linux?
UNIX is an operating system which was first developed in the 1960s, and has been under constant development ever since. By operating system, we mean the suite of programs which make the computer work. It is a stable, multi-user, multi-tasking system for servers, desktops and laptops.

UNIX systems also have a graphical user interface (GUI) similar to Microsoft Windows which provides an easy to use environment. However, knowledge of UNIX is required for operations which aren’t covered by a graphical program, or for when there is no windows interface available, for example, in a ssh session.

## Types of UNIX
There are many different versions of UNIX, although they share common similarities. The most popular varieties of UNIX are GNU/Linux and macOS. Within the “Linux” category, there are a multitude of flavors: Debian (Ubuntu, Mint, Crunchbang), RedHat (RHEL, Fedora, CentOS), SuSE, etc.

## The UNIX operating system
The UNIX operating system is made up of three parts; the kernel, the shell, and the programs.

### The Kernel
The kernel of UNIX is the hub of the operating system: it allocates time and memory to programs and handles the filestore and communications in response to system calls.

### The Shell 
The shell acts as an interface between the user and the kernel. When a user logs in, the login program checks the username and password, and then starts another program called the shell. The shell is a command line interpreter (CLI). It interprets the commands the user types in and arranges for them to be carried out. The commands are themselves programs: when they terminate, the shell gives the user another prompt.
Users will typically have the TCSH shell or Bash shell by default (Bash is typically the default on modern Linux distributions).

These shells have certain features to help the user inputting commands:

- Filename Completion - By typing part of the name of a command, filename or directory and pressing the [Tab] key, the tcsh and bash shells will complete the rest of the name automatically. If the shell finds more than one name beginning with those letters you have typed, it will beep, prompting you to type a few more letters before pressing the [Tab] key again.

- History - The shell keeps a list of the commands you have typed in. If you need to repeat a command, use the cursor keys to scroll up and down the list or type history for a list of previous commands.
