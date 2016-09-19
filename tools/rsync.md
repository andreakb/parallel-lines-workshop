# Rsync Guide
## What is Rsync?
Rsync is a fast, reliable and versitile file copying tool. It's a lot more efficent and
safer to copy files from a source to a working directory or from a source to an ingest location
using Rsync than using methods like dragging and dropping on a desktop. You can transfer files from  your computer to a
server, or vice vesra. You can feed Rsync a text file containing a list of files and their locations, and
Rsync will copy only those files in the same file structure as their source. If you're unsure if the file transfer
was completely successful, Rsync can check the files on the source and the output directory and only copy the
missing or incomplete files to the output location. While copying, Rsync can print out information
about the source files like checksums and file modification dates. Rsync is a powerful tool
to add to your arsenal when processing digital records!

## Sounds good! How can I get it?

### **On Windows**

There are various tools that for use Rsync algorithims and provide graphical interfaces (aka [GUIs](http://www.linfo.org/gui.html))  
[DeltaCopy](https://www.google.com) is a Windows wrapper for Rsync that has a gui, but you can also
use a command line interface for further customzation of your Rsync commands. After you download and install DeltaCopy,
you'll see an application called rsync.exe in the DeltaCopy folder
![alt text](https://github.com/andreakb/parallel-lines-workshop/raw/master/src/images/deltacopy.PNG "deltaCopy")

You can use this .exe file in your command prompt window to run Rsync.
![alt text](https://github.com/andreakb/parallel-lines-workshop/raw/master/src/images/rsyncwindows.PNG "command line rsycn on windows")

### **On Macs**
Rsync is already provided with OS X, but it may be an older version. Type
`rsync --version` into your terminal to check to see your rsync is up-to-date (the latest version is
  3.1.2). To update rsync, install [homebrew](http://brew.sh/), a package manager for OS X. You will need  xcode command line tools. Check if this is already install by typing `xcode-select -p` into your terminal. If the command returns something like `/Applications/Xcode.app/Contents/Developer`, then you're good to go. If not, either install xcode through the [iTunes store](https://itunes.apple.com/us/app/xcode/id497799835) or by typing `xcode-select --install` into your terminal and following the instructions from the prompt window.

  To install howebrew , type
  `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
  into the terminal. There are futher instructions on [Homebrew's git page](https://github.com/Homebrew/brew/blob/master/share/doc/homebrew/Installation.md#installation)

  Once Homebrew is installed, type
  ```
  brew tap homebrew/dupes
brew install rsync

```
into your termainal and an new version of rsync should install.

### **On Linux**

Like on a Mac, type `rsync --version` into your termainal to see if rsync is installed and if it's the latest version.
If not, type `sudo apt-get install rsync` to install it.

## How to run rsync

It's a good idea to [RTFM](https://en.wikipedia.org/wiki/RTFM) in any and all instances of using a tool! Do this on linux or mac by typing `man rsync` into the terminal. You can also find [man pages](https://en.wikipedia.org/wiki/Man_page) on the internet, but they may not be the most up-to-date manual.

The common usage is:

`rsync [OPTIONS] <source> <destination>`

You will need to use full paths to the files. On linux or mac, this looks something like this:
```
  rsync -rlptDv /mnt/live\ transfers\ working/E7\ working/Minister\ Hon.\ Mita\ Ririnui\ -\ E7/ /mnt/live\ transfers\ working/E7\ working/heroes/

  ```
On Windows, if you are copying files from a networked location, you will either need to use the network address or put `\cygdrive\` in the begining of your path. For example. this command uses both the network adress and cygdrive

```
rsync -rlptDvn "//dpprod.archives.net/ingest/Digitised/Wellington/linz_data/" "/cygdrive/e/FOUND_LINZ_INGEST/"

```
### What does -rlptDv mean?

When running tools from a command line interface, you can specify what options the tool offers you want to invoke when running that specific command. Rsync has loads of options.

![alt text](https://github.com/andreakb/parallel-lines-workshop/raw/master/src/images/optionssummary.png "options summary from rsync man page")

rlptDv are the options I use by default, but I switch them up depending on the cirucmstance. These options may or may not work for your purposes.

### **r - copies directories recursively**
  This makes rsync copy all the files not only from the directory you specify in the command, but from all subdirectories contained in the file sturcture.

### **l - recreates symbolic links in the destination location**
A symbolic link is any file or directory that, instead of containing the actual file or directory contents, is actually a reference (or link!) to another file or directory.

### **p - preserves permissions from the source location**

### **t -preserves modify dates from the source location**
Without option, the files on the destination location will have the modification date of the day/time they were copied.

### **D - allows rsync to copy special and device files.**
These include system files like tmp files or null files.

### **v - stands for increase versbosity.**
rsync will print out the files it is copying to the screen as it's copying them, along with any error or info messages.

## Test it out!

To see how your rsync command will work without copying files, you can use the **-n** option. This makes rsync perform a trial run, and doesn't make any changes. Use this with the -v option (verbose) or -i option (creates an itemized list of changes being made to each file on the destination location) in order to see the actual results of the trial run.

## Copy files from a list of files

Rysnc allows you to do this with the **--files-from=FILE** option (instead of the word FILE, use the name of the file that contains the list of files).

Invoke the option in a command like this:

`rsync -lptDv --files-from=filelist.txt /mnt/livetransfers/ /home/andrea/Documents/`

I don't use the **-r** option when copying from a list of files. Why do you think I don't do this?

The list of files should look like this:

![alt text](https://github.com/andreakb/parallel-lines-workshop/raw/master/src/images/filelist.PNG "files list")

Notice all the slashes in the file paths are forward slashes. This is the protocol in linux based systems and programs, like rsync.

The source location (in the above location, the source is '/mnt') refers to the relative path of the files in the list. In the above example, all the files in the list can be found in a directory called Peter Dunne - E4 in the location: **/mnt/livetransfers/**

When the files are copied over to /home/andrea/Documents, they will retain the same file sturcture from the source. So, a directory called Peter Dunne - E4 will be created, along with the specified sub-directories in the file list. The file structure will omit the location specified in the relative source (a directory called 'mnt' will not be created in my Documents directory), and only contain the directories in the file list.  For example, these are the files transfered from the list in my Documents folder.

![alt text](https://github.com/andreakb/parallel-lines-workshop/raw/master/src/images/posttransfer.PNG "post transfer")

You can use this option to transfer files listed in the rouges and heroes outputs from the [droid report tool](https://github.com/exponential-decay/droid-siegfried-sqlite-analysis-engine). 
