# windows-installer
This project provides an "Inno Setup"-ready Windows installer construction, simplifying Mind tools deployment.

## What the installer does

It contains all Mind tools and their requirements for any Windows type, be it 32-bit or 64-bit. It will unpack and install every necessary resource and dependency. It also adds user Path entries for the tools to be available from command line, and associates the ".gv" graph files with our mindot-viewer.

## Note: Required target folder

To this day we strongly advise the user to use the "C:\MINDWorkshop" folder as a destination, so that all our manually pre-configured folders (mostly for Eclipse) match directly and everything works "out of the box". Otherwise the user needs a few additional configuration steps.

## Pre-requisite configuration

Your machine must run a 64-bit Windows version.

## Pre-requisite downloads

You need to install the Inno Setup (free of charge) tool :
http://www.jrsoftware.org/isinfo.php

You must download:

- The Oracle JDK 8u31 for Windows 32-bit and 64-bit

Available at: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
Respectively jdk-8u31-windows-i586.exe and jdk-8u31-windows-x64.exe

- Eclipse C/C++ Development Tooling (CDT) for Windows 32-bit and 64-bit (here, Luna SR1a)

https://www.eclipse.org/downloads/packages/eclipse-ide-cc-developers/lunasr1a

- MinGW

http://sourceforge.net/projects/mingw/files/latest/download

- GraphViz 2.28.0 (recommended, or more)

http://www.graphviz.org/Download.php

- Python 2.7+ (3 still to be validated in our case)

https://www.python.org/downloads/

- PyGTK All-in-one 2.24.0

http://www.pygtk.org/downloads.html
http://ftp.gnome.org/pub/GNOME/binaries/win32/pygtk/2.24/

- A pre-built full Mind Tools release folder

## Pre-requisite configuration steps

You need to make files available in certain places, according to the Workshop.iss file, for them to be packaged and ran correctly by the constructed installer.

- In the "Windows" folder

Copy:
* graphviz-2.28.0.msi
* pygtk-all-in-one-2.24.0.win32-py2.7.msi
* python-2.7.2.msi

- In the "Windows/32" folder

Copy:
* jdk-8u31-windows-i586.exe

- In the "Windows/64" folder

Copy:
* jdk-8u31-windows-x64.exe

- In the "Windows/mind" folder

Unzip the pre-built Mind release directly in the folder, so that the "bin", "bundle", "doc", "examples", "ext", "lib", "manifest", "resources", "runtime", LICENSES.txt and README.txt are immediately available in the folder.

- In the "Windows/MinGW" folder

You need to provide a pre-installed and configured MinGW there.
An internet connection is mandatory in this step.
To do so, run the mingw-get-setup.exe package, make it install MinGW in the target Windows/MinGW folder, so that "bin", "doc" ... "var" are directly available at the root of this folder.

You must install the following packages:
* mingw32-base
* mingw32-gcc (bin)
* mingw32-gcc-g++ (bin)
* msys-base
* msys-mintty (bin) (an alternative bash-like shell, allowing resizing and lots of user-friendliness)

You should install the following packages:
* mingw32-binutils (bin)
* mingw32-gdb (bin)

Don't worry if you forget anything, you can run the installer later (even from the target installation "bin/mingw-get-setup.exe") to install/update/remove packages later.

- In the "Windows/32/minded" folder

Unzip eclipse-cpp-luna-SR1a-win32.zip "eclipse/" subfolder content in the Windows/32/minded folder, so as for "configuration" ... "eclipse.exe" ... "notice.html" to be directly available.

Configuration steps:
You must remove your machine's pre-existing JDK (if it exists) from your Windows configuration panel, and run the jdk-8u31-windows-i586.exe installer. This will install the 32-bit JDK on your machine (even if 64).

Then run the "eclipse.exe".
Configure the workspace to be "C:\MINDWorkshop\workspace" (this will be persisted).
Install the MindEd plugin via Help -> Install New Software... , "Add..." the following update site: "MindEd OW2 Devel" with URL "http://mind.ow2.org/mindEd-site-devel/"
Check the "MindEd" plugin (not "Dependencies"), go through the Next steps, validate everything, restart.
Then configure the Window -> Preferences -> Mindc Preferences, set the Mindc location to "C:\MINDWorkshop\mind" (this will be persisted as well).

- In the "Windows/64/minded" folder

Unzip eclipse-cpp-luna-SR1a-win32-x86_64.zip "eclipse/" subfolder content in the Windows/64/minded folder, so as for "configuration" ... "eclipse.exe" ... "notice.html" to be directly available.

Configuration steps:
You must remove your machine's pre-existing JDK (the 32-bit one from the previous step...) from your Windows configuration panel,and run the jdk-8u31-windows-x64.exe installer. This will install the 64-bit JDK on your machine (even if 64).

Then run the "eclipse.exe".
Configure the workspace to be "C:\MINDWorkshop\workspace" (this will be persisted).
Install the MindEd plugin via Help -> Install New Software... , "Add..." the following update site: "MindEd OW2 Devel" with URL "http://mind.ow2.org/mindEd-site-devel/"
Check the "MindEd" plugin (not "Dependencies"), go through the Next steps, validate everything, restart.
Then configure the Window -> Preferences -> Mindc Preferences, set the Mindc location to "C:\MINDWorkshop\mind" (this will be persisted as well).

## Building the installer

Open the "Workshop.iss" file in Inno Setup (that you should have installed in the first steps), and simply use the top menu "Build" -> "Compile". It will take some time and a "setup.exe" file will be generated at the base of your folder, containing all the previous tools.

Congratulations, you're ready to deploy an All In One Mind Tools release installer !

## Customization

You can replace any content in the installer, simply modify the Workshop.iss accordingly so that the right resources are packaged and ran at each expected steps.
