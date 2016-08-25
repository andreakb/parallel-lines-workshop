# Using Bash across Operating Systems
## Why?
A command line interface can be a powerful tool when assessing files in a transfer. It increases the ability to do batch changes, search multiple directories, use safer
transfer protocols, install, update and and run tools, and bonus, makes you feel like a 1337 haxor. it should be noted that using a bash shell *does* give you direct access to your computer's innards, so you'll want to be careful when making any sort of system changes. However, when running most commands that do make changes (rather than those that are asking for information) you'll have to use an admin password through a command called 'sudo.'


## On Windows

Windows has it's own command interface, **Command Prompt**. It uses a different sytanx
and language, [batch](http://www.infionline.net/~wtnewton/batch/batguide.html).
![alt text](https://github.com/andreakb/parallel-lines-workshop/raw/master/src/images/cmdprompt.gif "command window")

You can use command prompt to run different programs, like rsync or [python programs](https://github.com/exponential-decay/droid-siegfried-sqlite-analysis-engine) (as long as [python is installed](http://www.howtogeek.com/197947/how-to-install-python-on-windows/)!), much like shell.

[**Cygwin**](https://cygwin.com/index.html) is a free program that provides a unix/bash enviroment on a windows OS. There are some [good](http://wiki.rootzwiki.com/Step_by_step_guide_how_to_install_cygwin) [guides](http://www.mcclean-cooper.com/valentino/cygwin_install/) for [installing](https://cygwin.com/cygwin-ug-net/ov-ex-win.html) cygwin.
![alt text](https://github.com/andreakb/parallel-lines-workshop/raw/master/src/images/cygwin.gif "cygwin")

If you run **Windows 10**, you can actually run linux applications directly on windows through a bash shell! It's not available automatically, you'll have to [install](http://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/) it.
![alt text](https://github.com/andreakb/parallel-lines-workshop/raw/master/src/images/windows10bash.png)

## On Macs
Apple's OS X *is* unix, and Terminal, a program to interact with your system in a bash shell is built into your Mac. You'll find Terminal in your if you go to the utilities folder in the Applications directory. Clicking on the icon opens a terminal window and Bam! [Bash](http://blog.teamtreehouse.com/introduction-to-the-mac-os-x-command-line) [away](http://www.imore.com/how-use-terminal-mac-when-you-have-no-idea-where-start)!

![alt text](https://github.com/andreakb/parallel-lines-workshop/raw/master/src/images/Mac-Terminal-icon.png "terminal")

## Virtual Machines

Virtual Machines (VMs) allow you to run any operation system you want on your computer. Working in the government, running my favorite linux distro in a program called VMWare is my prefered way to work. Also, the VM uses Network settings
also gives you access to all your local files through the 'fake'
operating system's inteface, so you don't have to do the extra head banging work of say, setting up wifi on linux. You can also run as many VMs as you want! VMWare is powerful, but it's not free. [Virtual
Box](https://www.virtualbox.org/) is a good open source, free software that's available. After you install the virutalization software, your jobs not done. You'll have to install the OS you want to run. Micah Lee
at the Intercept wrote a really great [article](https://theintercept.com/2015/09/16/getting-hacked-doesnt-bad/) about how to install and running an [Ubuntu](http://www.ubuntu.com/) VM, a linux distro that
is pretty user friendly.
