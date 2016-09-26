# Basic Command Line Commands
This is an overview of some basic commands you can use in the Linux, OS X (on mac) or cygwin terminal. Of course, there is a lot more information than what is written below. Some people have written up in depth tutorials for, say grep! You can learn more about all of these, and learn different options by typing `man <command>` into your shell. When using these commands on your own, don't put `<>` around your input.

### **pwd** - prints the full name name of the current directory
usage: `pwd`

### **cd** - changes working directory
usage: `cd <dir>`
typing `cd` without a directory will take you back to the home directory.
`cd ..` will take you up one directory level.
`cd ../..` will take you up two directory levels (../../.. will take you up three levels and so on)

### **ls** - lists a directory's contents
usage: `ls` - displays the current directory's contents.
Specify a different directory by typing `ls <dir>`
The `-a` option displays all contents, including those that start with `.`
The `-l` option displays the in a long list

### **mkdir** - creates a new directory
usage: mkdir <dir>

### **rmdir** - removes an empty directory
usage: `rmdir <dir>`

### **rm** - removes files and directories
usage: `rm <file>` removes a specific file.

Using the wildcard `*` allows you to remove more than one file at a time.
`rm *` removes all files the current directory.

You can also use the wildcard to match patterns, for instance  `rm aaa*` will remove all the files that start with aaa. Or if you want to remove all files with an extension, try `rm *.txt`

The `-r` option invokes recursion, which means that if you type `rm -r *.txt`, all files in the current directory and in all the subdirectories that have a txt extension will be deleted.

`rm` deletes all files permanently. There is no trash bin with discarded file you can restore. So be careful when using this tool!

### **mv** - moves/renames files and directories
usage: `mv <source> <destination>`
You can use mv to change a name, and/or to move a file or directory to a different location

### **nano** - a simple text editor
usage: `nano <file>`
Nano may not be available on cygwin, but there are a number of other text editors you can try to use in your terminal. Nano is just the most basic. Try looking at notepad, vi, vim, emacs etc.  

### **less** - displays the contents of a file
usage: `less <file>`
If the file is longer than the size of your terminal screen, you will be able to scroll through the file. You can also search for a text pattern inside the file with `/ <text pattern>` for forward search or `? <text pattern>` for backwards search

### **grep** - searches for a text pattern
usage: `grep <"text pattern"> <file>`. The pattern should be in quotes. For instance, if you wanted to search the file bar.txt for the word "foo", type `grep "foo" bar.txt`

### **history** - displays list of recently used commands
usage: `history`

### Pipes

Command line tools usually take the standard input as noted in this guide and then print to the screen, or standard output. The `|` and `>` operators redirect outputs from one command to another.

For instance, if you wanted to create a text file of the contents of a directory, you could use `ls -l > filelist.txt`

Or if you wanted to search your history for the last times you used the cd command, you could use `history | grep "cd"`
