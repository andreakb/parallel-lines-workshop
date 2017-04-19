# Rsync Guide
## What is Rsync?
Rsync is a fast, reliable and versatile file copying tool. It's a lot more efficient and
safe to copy files using Rsync than using methods like dragging and dropping. You can transfer files from  your computer to a
server, or vice versa. Rsync **always** verifies that each transferred file was correctly reconstructed on the destination side by checking a the file's checksum is the same on the source side. You can feed Rsync a text file containing a list of files and their locations, and
Rsync will copy only those files in the same file structure as their source. If you're unsure if the file transfer completed successfully, Rsync can check the files on the source and the output directory and only copy the
missing or incomplete files to the output location. While copying, Rsync can print out information
about the source files like checksums and file modification dates. Rsync is a powerful tool
to add to your arsenal when processing digital records!

## Sounds good! How can I get it?

### **On Windows**

There are various tools for Windows that use Rsync algorithms and provide graphical interfaces (aka [GUIs](http://www.linfo.org/gui.html))  
[DeltaCopy](http://www.aboutmyip.com/AboutMyXApp/DeltaCopy.jsp) is a Windows wrapper for Rsync that has a GUI, but you can also
use a command line interface for further customization of your Rsync commands. After you download and install DeltaCopy,
you'll see an application called rsync.exe in the DeltaCopy folder
![alt text](https://github.com/andreakb/parallel-lines-workshop/raw/master/src/images/deltacopy.PNG "deltaCopy")

You can use this .exe file in your command prompt window to run Rsync.
![alt text](https://github.com/andreakb/parallel-lines-workshop/raw/master/src/images/rsyncwindows.PNG "command line rsycn on windows")

### **On Macs**
Rsync is already provided with OS X, but it may be an older version. Type
`rsync --version` into your terminal to check to see if your Rsync is up-to-date (the latest version is
  3.1.2). To update Rsync, install [homebrew](http://brew.sh/), a package manager for OS X. You will need  xcode command line tools. Check if this is already install by typing `xcode-select -p` into your terminal. If the command returns something like `/Applications/Xcode.app/Contents/Developer`, then you're good to go. If not, either install xcode through the [iTunes store](https://itunes.apple.com/us/app/xcode/id497799835) or by typing `xcode-select --install` into your terminal and following the instructions from the prompt window.

  To install homebrew , type
  ```
  /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

  ```
  into the terminal. There are further  instructions on [Homebrew's git page](https://github.com/Homebrew/brew/blob/master/share/doc/homebrew/Installation.md#installation)

  Once Homebrew is installed, type
  ```
  brew tap homebrew/dupes
  brew install rsync

```
into your terminal and a new version of Rsync should install.

### **On Linux**

Like on a Mac, type `rsync --version` into your terminal to see if Rsync is installed and if it's the latest version.
If not, type `sudo apt-get install rsync` to install it.

## How to run Rsync

It's a good idea to [RTFM](https://en.wikipedia.org/wiki/RTFM) in any and all instances of using a tool! Do this on Linux or your Mac by typing `man rsync` into the terminal. You can also find [man pages](https://en.wikipedia.org/wiki/Man_page) on the internet, but they may not be the most up-to-date manual.

The common usage is:

`rsync [OPTIONS] <source> <destination>`

You will need to use full paths to the files. On Linux or Mac, this looks something like this:
```
   rsync -rlptDv /mnt/live\ transfers\ working/digital\ archaeology/Peter\ Dunne\ -\ E4 /home/andrea/Documents/

  ```
On Windows, if you are copying files from a networked location, you will either need to use the network address or put `\cygdrive\` in the begining of your path. For example. this command uses both the network address and cygdrive

```
rsync -rlptDvn "//dpprod.archives.net/ingest/Digitised/Wellington/linz_data/" "/cygdrive/e/FOUND_LINZ_INGEST/"

```
### What does -rlptDv mean?

When running tools from a command line interface, you can specify what options the tool offers you want to invoke when running that specific command. Rsync has loads of options.

![alt text](https://github.com/andreakb/parallel-lines-workshop/raw/master/src/images/optionssummary.png "options summary from rsync man page")

rlptDv are the options I use by default, but I switch them up depending on the circumstance. These options may or may not work for your purposes.

### **r - copies directories recursively**
  This makes Rsync copy all the files not only from the directory you specify in the command, but from all subdirectories contained in the file structure.

### **l - recreates symbolic links in the destination location**
A symbolic link is any file or directory that, instead of containing the actual file or directory contents, is actually a reference (or link!) to another file or directory.

### **p - preserves permissions from the source location**

### **t -preserves modify dates from the source location**
Without this option, the files on the destination location will have the modification date of the day/time they were copied.

### **D - allows Rsync to copy special and device files**
These include system files like tmp files or null files.

### **v - increases verbosity**
Rsync will print out the names of the files and directories it is copying to the screen as it's copying them, along with any error or info messages.

Information on the command can also be found on [explainshell.com](https://explainshell.com/explain?cmd=+rsync+-rlptDv+%2Fmnt%2Flive%5C+transfers%5C+working%2Fdigital%5C+archaeology%2FPeter%5C+Dunne%5C+-%5C+E4+%2Fhome%2Fandrea%2FDocuments%2F)

## Test it out!

To test how your Rsync command will work before actually copying files, you can use the **-n** option. This makes Rsync perform a trial run, and doesn't make any changes. Use this with the -v option (verbose) or -i option (creates an itemized list of changes being made to each file on the destination location) in order to see the actual results of the trial run.

## Copy files from a list of files

Rysnc allows you to do this with the **--files-from=FILE** option (instead of the word FILE, use the name of the file that contains the list of files).

Invoke the option in a command like this:

`rsync -lptDv --files-from=filelist.txt /mnt/livetransfers/ /home/andrea/Documents/`

I usually don't use the **-r** option when copying from a list of files. **Why** do you think I don't do this?

The list of files should look like this:

![alt text](https://github.com/andreakb/parallel-lines-workshop/raw/master/src/images/filelist.PNG "files list")

Notice all the slashes in the file paths are forward slashes. This is the protocol in Linux based systems and programs, like Rsync.

The source location (in the above location, the source is '/mnt') refers to the relative path of the files in the list. In the above example, all the files in the list can be found in a directory on my computer called Peter Dunne - E4 in the location **/mnt/livetransfers/**

When the files are copied over to /home/andrea/Documents, they will retain the same file structure from the source. So, a directory called Peter Dunne - E4 will be created, along with the specified sub-directories in the file list. The file structure will omit the location specified in the relative source (i.e. a directory called 'mnt' will not be created in my Documents directory), and only contain the directories in the file list.  For example, these are the files transferred from the list in my Documents folder.

![alt text](https://github.com/andreakb/parallel-lines-workshop/raw/master/src/images/posttransfer.PNG "post transfer")

You can use this option to transfer files listed in the rogues and heroes outputs from the [droid report tool](https://github.com/exponential-decay/droid-siegfried-sqlite-analysis-engine).

## What if there are errors in the transfer?

Like the connection between the source and the destination drops out? Or you accidentally  stop the transfer process? Or the modification times are different, for some reason? Or, even after the fact, some files in your working directory accidentally got deleted or modified and you don't know which ones? Rsync is there for you!

With the `--inplace` option Rsync can amend partial files, without copying over another new file and leaving a partial file in the directory.

Rsync's normal behavior is to do a 'quick check' which involves checking if the source file and the destination file have a different size or a different modification date to see if the  destination file is in need of an update. Invoking the `-c` option will compare checksums of the files that pass this 'quick check' criteria to ensure that the files are the same or  need to be replaced with the source file.  

Make sure to also use `-t` when using `-c` and/or `--inplace`, to either restore or maintain the modify dates from the source files to the destination location.

And, if you want to see what is actually changing in the destination location, use the `-i`  option. This creates an itemized list of changes that are being made to each file. Before you do an actual transfer, it may be a good idea to use the `-n` (dry run) option with `-i`, to see exactly what will change and if the command you're running will do what you want it to do. The list looks something like this.

![alt text](https://github.com/andreakb/parallel-lines-workshop/raw/master/src/images/itemizelist.PNG "itemized list")

(This list was created using the command `rsync -rncit  --inplace  <source> <destination>`)

You'll notice that there is a particular syntax to the itemized list that may not make sense without looking at the man page! Just another reminder to read the man page!

## What about that thing about printing out checksum and file modification dates?

It's pretty easy to have Rsync print out a variety of information during the transfer process. You can even manipulate the output to be in form that works for you.
To print out the file modification date, md5 checksum, and filename into a csv, I use the following command

`rsync -rlptDc --out-format='%C, %M, %f' <source> <destination> > <output.csv>`

The --out-format option allows you to control exactly what Rsync outputs during a transfer.
In this case, I am telling Rsync to output a string containing a checksum (%C), the last modified date (%M), and the full filename (%f). The percentage signs are a signal to Rsync that says: Pay attention, the next character is a command, not just a letter. Because the out format specification is inside single quotes, Rsync outputs exactly what you specify in the single quotes. In this example, all the values are separated by a comma, which makes it easy to output to a csv. For a complete list of what information can be reported by Rsync and what character values to use for each one, see the man page for rsyncd.conf.

![alt text](https://github.com/andreakb/parallel-lines-workshop/raw/master/src/images/outputcharacters.PNG "output characters")

I put filename last in the string when creating a csv. Why do you think I do this?

The `>` character acts like a pipe, and, instead of printing the output to the screen, it directs it to a file called output.csv (you can name the file whatever you want!) You can use this character across programs and tools on a Linux-based command line.


I hope this helped to demonstrate how versatile Rsync is, and what a great tool it is for moving files around. Of course, this just skims the surface! There's loads more you can make Rsync do, just read the man page.
