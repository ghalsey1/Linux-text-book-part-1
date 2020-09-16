# Desktop Linux and GUIs

![*GUIs??? NIH*](images/Chapter-Header/Chapter-04/supported_features2.png "GUIs NIH")

## Objectives

* Learn about the different types of desktop Linux
* Understand the nature and use of X, Wayland, and other GUI compositors
* Understand the purpose of window managers and the nature of desktop environments
* Know the major features of GNOME 3 desktop environments
* Understand GUI package managers and application stores
* Understand theming on the Linux Desktop

## Outcomes

At the conclusion of this chapter you will have a strong knowledge of the X Windows system and why it is the foundation of Desktop Linux.  You will be able to implement various window managers and desktop environments, selecting the proper environment to utilize and suit your hardware needs.  You will be comfortable using and recognizing the features of GNOME 3 desktop environment.

## From Paper Tape to CLI to GUIs to 4K

When you think about how we use computers today the one thing we take for granted is a *GUI*, __Graphical User Interface__.  The GUI is intricately tied to the way computers are used, why do think Microsoft calls its operating system Windows? Unix however, had its start in the late 1960s and 1970s--there was vastly different technology available at that time.  The PDP-7s that Thompson and Ritchie used were called [*Teletypes*](https://en.wikipedia.org/wiki/Teleprinter "TTYs") or *TTYs* that had punch card readers for data entry and paper tape for output connected to a PDP-7 via a modem. You will notice that even today in Unix screen outputs are still referred to as TTYs. By the mid 1970s we begin to see what are called *dumb terminals* appear which could be considered primitive monitors.

The [Datapoint 3300](https://en.wikipedia.org/wiki/Datapoint_3300 "Datapoint 3300") was one of the more common models representing the era.  It supported control codes to move the cursor up, down, left and right, to the top left of the screen, or to the start of the bottom line and displayed a whopping 72 by 25 rows of characters in the days before microprocessors and ram were part of terminals. By 1978 Digital Equipment Corporation (DEC) had released something akin to an upgrade for the dumb terminal called a *smart terminal*.

The [DEC VT-100](https://en.wikipedia.org/wiki/VT100 "VT-100") was the most popular model: it had character and cursor positioning and was connected to the Unix system via serial ports and a modem.  The VT-100 set the standard for 80 by 24 rows and columns still in use today.  These terminals had the backing of DRAM and an Intel 8080 processor.  Open up any terminal emulator in Linux and see its default size.  Open up cmd.exe in Windows and you will notice the same default dimensions.  Why? Sociologists always talk about nature vs. nurture. Nature plays a huge part in software development.  All the developers who built Terminal emulators and cmd.exe for Windows "grew up" using Unix systems on a DEC VT-100 screen in college and at work.  It was a natural fit.  The VT-100 and VT-220 continued with wide deployment and success but the concept of color or being able to draw any shapes to the screen was in the hands of a few expensive and proprietary companies; everything was still [ASCII](https://en.wikipedia.org/wiki/ASCII "ASCII") or character based.

### VT-100

![*VT-100*](images/Chapter-04/Terminals/DEC_VT100_terminal.jpg "VT-100")[^25]

This screenshot is a file listing from the ```/dev``` (devices) folder on a Fedora 22 system

![*TTY Alive Today*](images/Chapter-04/tty.png "TTYs")

![*Windows cmd.exe eerily similar to the VT-100*](images/Chapter-04/cmd-399-by-200.png "cmd.exe")

![*Ubuntu's GNOME Terminal emulates the VT-100 directly*](images/Chapter-04/linux-terminal-299-by-200.png "Linux Terminal")

### Virtual Consoles

With the X system the idea of having discrete terminals went away.  Now you could have multiple *virtual terminals* on one system that emulated the features of a DEC VT-100 or VT-220 terminal.  If you hit the  ```ctrl + alt + F1-F7``` within your Linux distro you will jump to 1 of 7 different virtual terminals enabled by default.  Usually F7 is the default GUI but it can vary from operating system to operating system.

## Along Comes an X

Beyond the simple green screen terminals by the mid 1980s we began to see proprietary primitive UNIX GUIs from commercial vendors, especially from Sun. These GUI interfaces were placed on high-end workstations sold at premium prices for the day. One may wonder why you would even bother to create a GUI in the first place. Computing at that time was beginning to take less of an iterative/batch processing approach to computing and a more of an interactive approach. GUIs were in the hand of the privileged few vendors but not of anyone else.  By 1985 MIT opensourced a project called X.  This project was after Richard Stallman had left the school but continued in his spirit.  X was a continuation of a primitive GUI called "*W*". As Unix originally had no concept of a GUI, one had to be bolted on.  But the spirit of X was not to enforce any standards on the user.

X uses a client–server model: an X server communicates with various client programs. The server accepts requests for graphical output (windows) and sends back user input (from keyboard, mouse, or touchscreen). The server may function as:

* An application displaying to a window of another display system
* A system program controlling the video output of a PC
* A dedicated piece of hardware.

### X

![*X Diagram*](images/Chapter-04/X/X_client_server_example.svg-3.png "X diagram")

Even in the mid 1980s the dream of having your own desktop PC was a bit of a ways off.  Large single Unix systems were still the nature of computing so the X system fit in, especially in the idea of remote terminals or underpowered system connecting remotely to a central server and running their own *X Window* remotely. X is often misnamed as X Windows, but the name for the project is *"X"*.

> *"...in 1987-1988 X established itself as the standard graphics engine for Unix machines, a hardware-independent neutral platform on top of which to build GUIs"* [Eric S. Raymond writings](http://www.catb.org/~esr/writings/taouu/html/ch02s06.html "Early history of Unix").

> *"X provides the basic framework for a GUI environment: drawing and moving windows on the display device and interacting with a mouse and keyboard. X does not mandate the user interface — this is handled by individual programs."*  [https://en.wikipedia.org/wiki/X_Window_System](https://en.wikipedia.org/wiki/X_Window_System "X Windows")

By 1987 version 11 of the protocol had been released, being commonly referred to as X11.  The industry wanted to prevent fragmentation and they asked MIT to form a steering consortium for the project.  The MIT X Consortium became the X Consortium Inc. in 1993.  By 1996 the X Consortium, with vendor input, released one of the first standard Unix GUIs called the __CDE__ *Common Desktop Environment*. By 1997 the X Consortium transformed into the Open Group.  The Open Group angered many people by relicensing the project under stricter commercial terms in an effort to make some money to support the project--but this action backfired.  By 1999 the Open Group had ceased functioning and ceased really developing X. The Open Group created *X.Org* to maintain the X11 standard.

At the same time a parallel implementation base on X11R5 was being developed by IBM for their PCs.  The project was started in 1992 as XFree86.  This code was donated to the X Consortium and the code has been part of the larger code base that the X Consortium managed.  So while the X Consortium/Open Group/[X.Org](http://www.x.org "X") was in charge of X development, they actually weren't innovating or developing anything.  It was the group at XFree86 that was doing all the innovation.

The story gets more complicated.  As the userbase of Linux surges in the early 2000s as desktop Linux and GUIs grow, X use would naturally follow that growth curve as well.  You have two problems: [X.Org](http://www.x.org "X"), a vendor controlled stewardship organization, was not doing any development on X, and XFree86 was starting to narrow its *openness* just like the OpenGroup did in 1997, expelling some of the original X creators who had joined the XFree86 project and changing open licenses to be non-GPL compliant (non-Linux compatible license.)

This led to the founding of the X.Org Foundation merging the two groups.  This was a breakthrough event.  It basically reconciled the two groups under one new foundation, [X.Org Foundation](http://www.x.org "X.Org Foundation"), it also ensured that the creators of the X project were once again the stewards, and finally it insured that there was a GPL based and protected X project that developers and companies could contribute to as well. The X.Org Foundation continues to innovate and foster the project to this day.

A final GUI note that in parallel the most breakthrough commercial GUI available in the early 80s was released by Apple in 1984[^23].  Here is a [link to an article](http://www.folklore.org/StoryView.py?story=Busy_Being_Born.txt "Mac") from the developers about how it came to be.

![*Apple Macintosh 1984*](images/Chapter-04/Terminals/205px-Macintosh_128k_transparency.png "Apple Macintosh")

X has a definite advantage in that it is very mature and very stable for better or worse.  In the diagram earlier in the chapter you can see one of X's major faults.  It was designed not with a desktop GUI in mind, those didn't exist at the time. Every desktop element is a client that has to make calls to the X server in order to render any changes to the screen.  This adds extra layers of overhead and also becomes a [security issue](http://www.windowsecurity.com/whitepapers/unix_security/Securing_X_Windows.html#3.0 "Security Issues") with an X client being able to connect unauthenticated in some cases to other X servers remotely on the network.

### Project Wayland

In the late part of the 2000s, then Red Hat engineer Kristian Høgsberg, began to reimagine the nature of the Linux GUI compositor with a simpler desktop driven protocol.  With the help of other senior X.Org developers they began to create a successor project to the X project.  By 2012 they had their first code release usable for beta testing. This project was called [Wayland](http://wayland.freedesktop.org "Wayland").  The famous architect of the City of Chicago Daniel Burnham once said, *"Make no little plans. They have no magic to stir men's blood and probably will not themselves be realized."*  Every single desktop environment and window manager runs on X--this means rewriting or extending every single graphical toolkit and graphical development environment out there. The Wayland project had that just in mind. What is Wayland then?

> *"Wayland is a protocol for a compositor to talk to its clients as well as a C library implementation of that protocol. The compositor can be a standalone display server running on Linux kernel modesetting and evdev input devices, an X application, or a wayland client itself. The clients can be traditional applications, X servers (rootless or fullscreen) or other display servers."* [Wayland Project](http://wayland.freedesktop.org/ "Wayland Project")

![*Wayland Rendering Model*](images/Chapter-04/wayland-architecture.png "Wayland Architecture")

* The kernel gets an event and sends it to the compositor. This is similar to the X case, which is great, since we get to reuse all the input drivers in the kernel.
* The compositor looks through its scenegraph to determine which window should receive the event. The scenegraph corresponds to what's on screen and the compositor understands the transformations that it may have applied to the elements in the scenegraph. Thus, the compositor can pick the right window and transform the screen coordinates to window local coordinates, by applying the inverse transformations. The types of transformation that can be applied to a window is only restricted to what the compositor can do, as long as it can compute the inverse transformation for the input events.
* As in the X case, when the client receives the event, it updates the UI in response. But in the Wayland case, the rendering happens in the client, and the client just sends a request to the compositor to indicate the region that was updated.
* The compositor collects damage requests from its clients and then recomposites the screen. The compositor can then directly issue an ioctl to schedule a pageflip with KMS.

At one time it was thought that X is too deep into the bones of Linux and may never be ever fully replaced. But we are seeing massive amounts of work from industry to make Wayland a reality. With Intel, Nvidia, the X.Org Foundation and Red Hat leading the way, Fedora 25 was one of the first distros to run Wayland natively.  

![*X on Wayland*](images/Chapter-04/x-on-wayland.png "X on Wayland")

### Ubuntu Mir

Not to be outdone Ubuntu saw an opportunity to come up with an X replacement and announced the Mir project in early 2013.  Unfortunately this has met with serious opposition from the X and Wayland communities seeing this as an outside effort to *"corner the market"*, even to the point in 2013 of Intel, who supports Wayland, [rejecting XMir support](http://arstechnica.com/information-technology/2013/09/intel-rejection-of-ubuntus-mir-patch-forces-canonical-to-go-own-way/ "Intel Rejects XMir") in its Linux opensource graphic driver package.

Ubuntu is the only Linux operating system to support Mir and development has been delayed as the project has taken on the monumental task of replacing X.  Ubuntu was criticized for not joining the Wayland group's work but I think that may have been somewhat without warrant.  Ubuntu has a business use case--they are looking to make a compositor that could adapt based on form factor, something not unlike how Android works.  This would enable them to make Ubuntu for tablets, phones, TVs, even smaller devices electronic devices.  Mir would be customizable to Ubuntu's hardware dreams and they could sell hardware and perhaps make some money.

> *"In March 2014, Mark Shuttleworth confirmed that Mir development had been delayed and that it was now forecast to be default for desktop use in Ubuntu 16.04 LTS, expected to be released in April 2016."* [^27]

As of [April 5th 2017](https://arstechnica.com/information-technology/2017/04/ubuntu-unity-is-dead-desktop-will-switch-back-to-gnome-next-year/ "Unity Dead"), Mark Shuttleworth announced that in Ubuntu 18.04 the UNITY interface and the Mir compositing engine would be deprecated in favor of GNOME 3 and Wayland.  But the Mir Project and Unity lives on in the Ubuntu Touch port maintained for phones and tablets by the [Ubuntu-Touch.io](https://ubuntu-touch.io/ "Ubuntu Touch webpage") project.  The Mir display server is now gaining popularity running Ubuntu Touch on the [Librem 5](https://fossbytes.com/librem-5-ubuntu-touch-support/ "librem 5 ubuntu touch web page") and the [Pinephone](https://devices.ubuntu-touch.io/device/pinephone/ "pinephone running ubuntu touch") Linux based cell phones.

## Window Managers

X will let you display a window and let you capture mouse and keyboard commands.  But what if you want to render multiple windows on one machine and manage their state as well (open and close them?) How about arranging them?  Do you need them tiled or overlapping? Then you need a window manager to sit on top of X and handle that rendering.  Thankfully window managers are essentially common in Desktop Linux and almost inseparable from X in this case. Window Managers are not the full GUIs you might be used to. They are one step below a full blown desktop environment but window managers are very fast because they render simple windows and simple sets of icons.  Their job is to render content inside of particular windows and manage that window's state. Since Linux and X were developed independent of a central product, you will see a depth and breadth of different window managers serving different functions and features.  Some are very simple, some serve direct purposes, some are tied to full blown desktop environments.  Window Managers can be changed and swapped as needed because they are not a central part of the operating system.  As opposed to Windows and Mac where all you can do is change themes, you can't change window managers.  Some of the minimalistic window managers can be used to help older laptops and PCs remain useful and very usable with modern Linux, where modern commercial operating systems like the Mac for instance intentionally deprecates older hardware. You can break window managers into 3 categories based on their window behavior.

### Compositing

* [Compiz](http://www.compiz.org/ "Compiz") - Fusion Adds more functionality to Compiz with more plugins, tools and libraries. Allows for OpenGL use in windows and compositing
* [Metacity](https://blogs.gnome.org/metacity/ "metacity") - Small window manager, using GTK+ 2 to do everything
* [evilwm](http://www.6809.org.uk/evilwm/ "evilwm") - Maximizes screen real estate and provides good keyboard control
* [KWin](https://en.wikipedia.org/wiki/KWin "KWin") - Window manager for the KDE Desktop Environment
* [Mutter](https://en.wikipedia.org/wiki/Mutter_%28software%29 "Mutter") - Window manager for the GNOME Desktop Environment

### Stacking

* [Blackbox](http://blackboxwm.sourceforge.net/ "Blackbox Wiki") - Similar to the NeXT interface and Window Maker
* [Fluxbox](http://fluxbox.org/ "Fluxbox") - Highly configurable and low resource
* [FVWM](http://www.fvwm.org/ "FVWM") - Minimize memory consumption, provide a 3D look to windows, and a virtual desktop
* [Enlightenment](https://www.enlightenment.org/ "Enlightenment") - Focuses on pushing the limits of existing technologies
* [Openbox](http://openbox.org/wiki/Main_Page "Openbox") - Standards compliant, fast, light-weight, extensible window manager
* [Sawfish](http://sawfish.tuxfamily.org/ "Sawfish") - Extensible window manager using an Emacs Lisp-like scripting language
* [Motif - mwm](http://motif.ics.com/ "Motif") - Originally the libraries contained in the CDE -- now opensource
* [IceWM](http://www.icewm.org/ "ICEWM") - Win95-OS/2-Motif-like window manager
* [Afterstep](http://afterstep.org/ "Afterstep") - NEXTSTEP look and feel
* [Window Maker](http://windowmaker.org/ "wmaker") - NeXTSTEP-like window manager
* [FLWM](https://en.wikipedia.org/wiki/FLWM "Fast and Light Window Manager") Fast and Light Window Manager

### Tiling

* [Awesome](https://en.wikipedia.org/wiki/Awesome_(window_manager) "Awesome") - mouse optional
* [Xmonad](http://xmonad.org/ "Xmonad") - Minimalist, tiling window manager written in Haskell
* [ratpoison](http://www.nongnu.org/ratpoison/shot2.png "ratpoison") - Keyboard-only window manager no mouse support.
* [StumpWM](https://stumpwm.github.io/ "Stumpwm") - Built in Common Lisp window manager and Keyboard-only
* [dwm](http://dwm.suckless.org/ "dwm") - Dynamic window manager
* [tinywm](http://incise.org/tinywm.html "tiny wm") - Very very minimalistic window manager
* [i3](http://i3wm.org/ "i3") - Good documentation, reasonable defaults, and good multi-monitor support.

## Desktop Environments

About the time that the OSI movement was launching in late 1990s a growing need for more than just window managers was growing too.  x86 Intel and AMD CPUs at that time were gaining in processing power and processor based multimedia extensions began to appear by 1997, [collectively called MMX](https://en.wikipedia.org/wiki/MMX_(instruction_set) "MMX"). What is the difference between a desktop environment and a window manager? Simple things that you may take for granted such as as a clock, or a text editor, office suite or an email client, even a web browser.  Also a desktop environment provides an IPC method for inter-window communication.  Most important, a desktop environment includes a file manager application, a start or action menu feature and a login manager (display manager) such as GDM, KDM, or SDDM [^32].  On top of that all the elements of the desktop have a changeable but consistent usage pattern and look-and-feel.  Let us look first at the development history of the two main desktop environments followed by a few other desktop environments.

### KDE [^33]

The KDE project (originally the K Desktop Environment) was the first opensource Linux desktop environment project.  Started by Matthias Ettrich at the university of Tübingen in Germany in 1996. The first release of the __K Desktop Environment__ was in 1998 and the name was a *"clever hack"* of the CDE--Common Desktop Environment--developed for Unix by Sun, HP, and IBM. KDE focused on the lack of perceived usability in Linux window managers.  You and I may take desktop environments for granted based on our experience with Mac and Windows respectively. Unix and Linux in 1998, did not have the same capabilities--just a mix of window managers and independent applications.  At the time of development there were only a few toolkits available that could be used for creating desktop environments in Linux.  One of them was [Qt](https://www.qt.io/ "Qt"), pronounced *"cute-ee"*. Qt was a good choice for developers because at the time was the only toolkit that had C++ language bindings. GTK was C only at this point. Matthias Ettrich chose the best technology at the time for developing GUIs. Qt was initially developed by a company called Trolltech.

In 1998 Qt was not available under a completely *"free software"* license. It had a modified license called the QPL, stating that non-commercial software projects for Unix/Linux were allowable. By 2000 Trolltech relicensed Qt to be GPL compliant. This fact still upset Richard Stallman who never forgave KDE for initially using a non-GPL compatible license. As an aside, Nokia bought Trolltech in 2008 but Qt remained under GPL license. [^34] Qt was used by Nokia to power their Symbian OS which dominated the cellular market as the predominant OS until Android unseated it by 2010.

KDE is unique because although Qt has vendor input to the project, KDE itself is not vendor owned. KDE is also not tied to a single Linux distro in the way that GNOME and Red Hat are intricately tied together now. Distros such as  [openSUSE](opensuse.org "opensuse"), [Mageia](mageia.org "Mageia"), [Chakra](www.chakralinux.org "Chakra Linux"), [Kubuntu](www.kubuntu.org "Kubuntu"), [PCLinuxOS](www.pclinuxos.com "PC Linux OS") and even FreeBSD are using KDE by default or have it available in software repositories. Qt recently split itself during the 5.0 release from one entire library into [three separate sub-components](https://en.wikipedia.org/wiki/KDE_Software_Compilation#Post-fourth_series "KDE 5 split"):

* KDE Desktop - Desktop called [Plasma 5](https://www.kde.org/workspaces/plasmadesktop/ "Plasma") released every three months
* KDE Applications - [KDE applications](https://en.wikipedia.org/wiki/KDE_Applications "KDE applications") updated and released every four months
* KDE Frameworks - [Common file, os, and services](https://en.wikipedia.org/wiki/KDE_Frameworks_5 "KDE Frameworks")

### GNOME [^33]

Shortly after the initial release of KDE and its licensing confusion, an enterprising opensource advocate saw the need for a truly open and free desktop environment.  His name is [Miguel De Icaza](https://en.wikipedia.org/wiki/Miguel_de_Icaza "Miguel")

#### Miguel de Icaza

![*Miguel de Icaza*](images/Chapter-04/People/351px-Miguel_de_Icaza.jpg "Miguel de Icaza")

GNOME initially stood for GNU Network Object Model Environment but the acronym is no longer used[^28].  GNOME was a GNU project directly created under the GPL.  The first major GNOME release was done by Miguel in March of 1999. This project used the [*GTK+*](http://www.gtk.org/ "GTK+"), commonly mistaken as the *Gnome Tool Kit*, actually stands for the GIMP Tool Kit.  [GIMP](https://en.wikipedia.org/wiki/GIMP "GIMP") is the GNU Image Manipulation Program similar to Photoshop or Paint.Net in feature set.  GTK or now known as GTK+ is a library useful for creating standalone applications with multiple development language bindings as well.

In an interesting development Miguel ended up forming the company that became Xamarin, a cross development mobile platform company using C# to develop for Android and iOS--shortly after Microsoft began opensourcing the C# language.   Recently Xamarin was purchased by Microsoft and Miguel is now a Microsoft VP. Miguel has always been a software pragmatist - always chasing the best technology and open sourcing it.  He took much criticism because he started the Mono project in bringing Microsoft's C# and .NET platform to Linux, because he saw C# as the best language to develop in cross platform.   This brought about the condemnation of Richard Stallman, calling Miguel, "*A traitor to free software.*" [^30]  Miguel's response to Stallman was a beautiful example of how to diffuse an inflammatory situation:

> *"I want to say that God loves all creatures. From the formidable elephant to the tiniest ant. And that includes Richard Stallman.
>
> As for me, I think that there is a world of possibility, and if Richard wants to discuss how we can improve the pool of open source/free software in the world he has my email address.
>
> Love, Miguel."* [^35]

In the early 2000s Sun and HP adopted the GNOME desktop as the replacement for CDE for their Unix distros.  Red Hat and Debian adopted GNOME as well. With the release of Ubuntu 18.04, Ubuntu returned to the Gnome desktop.

GNOME 2 was released in early 2002 and the last GNOME 3 release was in 2010.  Over this 8 years GNOME developed itself as a mature desktop by using the traditional desktop metaphor: start menu, task managers, and toolbars.  But like all things that change, in early 2011 GNOME 3 was released, and there was a mighty backlash.  Even Linus Torvalds, who is a Red Hat and GNOME user came out against GNOME 3 hard, calling it a *"total UX disaster"* [^36]. What made GNOME 3 so different is that it took on a different metaphor, called the GNOME shell.  Think of the GNOME shell as a way to manage or view multiple tasks and applications happening at once.  Instead of a single desktop, think of the new metaphor as a table top using the shell as a magnifying glass to view all tasks.

#### GNOME Forks: Unity, Mate, and Cinnamon

Linus Torvalds was quoted as saying:

> "People don't want Gnome 2 because it was a pinnacle of some GUI design. They want it because Gnome 3 removed features they used, and made it harder to get their work done,"  [^38]

GNOME 3 led to the creation of alternatives in 2012. When GNOME moved from version 2 to version 3 the amount change was seen by some GNOME users as treason. The MATE project (pronounced *"ma-tay"* not *"may-tuh"*) was a fork and continuation of the GNOME 2 code base.  The Cinnamon desktop was a fork of GNOME 3 with an added features set for the Linux Mint distro. Unity was Ubuntu's reimplementation of the GNOME shell with the Unity shell on top of GNOME 3.  These desktops, with the exception of Unity, can be deployed or installed on most Linux distributions. As a final thought Linus Torvalds has since reconciled with GNOME 3 as of 2013 based on some additional 3rd party tools that allow the GNOME 3 experience to be customized to his liking. [^37]

Which is better GNOME or KDE?  With all major Linux systems that are using systemd now have no choice but to adopt GNOME 3 as the default desktop.  Both have had great set backs and great feature advancements over the years. In the end it is up to you based on your usage patterns, development environment preferences, even which distro you use or prefer.  Try them both and choose the best one for your needs.

### Xfce

Seeing as KDE and GNOME focused on features and usability, many people who were using older hardware felt left out or unable to run these environments as the resources required were growing.  So a movement to create a lightweight desktop environment sprung up.  The first was Xfce and was developed in parallel to KDE and GNOME by Olivier Fourdan. Xfce wrote all of its [components](https://en.wikipedia.org/wiki/Xfce#Software_components "Xfce components") by itself not relying on or forking any of GNOME. This environment had a focus on simplicity and running with lower end hardware requirements. Originally based on a proprietary toolkit, when Xfce was rejected for inclusion in Red Hat Linux because of this license, Xfce moved to GTK+ 2 toolkit by 1999.  At one point Debian was considering it as an alternative to GNOME 3, but dropped it because of adopting systemd--forcing Debian to take GNOME 3 as their default desktop.  Xubuntu is a common derivative distro made up of Ubuntu using Xfce instead of GNOME or Unity.  Xfce until recently was using the GTK2 toolkit but is in the process of being rewritten in GTK3 conversion started with version 4.12 in 2015.  As of 2018, most of the major components have been re-written in GTK3.  When version 4.14 is released all major components will be converted to GTK3.

### LXQT

The LXQT project was started as the LXDE project in 2006 by Hong Jen Yee.  This desktop environment is even more spartan than Xfce but is one step above a window manager. LXDE's focus is on making pretty much any laptop or PC made in the last decade still usable for modern Linux.  Recently the lead developer Hong Jen Yee had disagreements with the direction GTK+ 3 was taking and has made a parallel design port called LXQT.  LXQT involved LXDE porting their desktop applications to Qt and merging with a defunct project called Razor-Qt to produce LXQT.

### Enlightenment

This project started in 1997 and intended to be a virtual desktop window manager.  This would involve a grid of desktops a user could move windows around and onto.  The initial release was in 1999 called E16.  The second release E17 took 12 years.  But E17 had grown from just a window manager into a full-fledged desktop environment using its own libraries called Enlightenment Foundation Libraries.  Enlightenment can also be a shell that can sit on top of KDE and GNOME.

### Lumina

A distro of FreeBSD, called TrueOS, created their own native desktop environment for their GUI based FreeBSD distro.  They had previously relied on GNOME and KDE but the amount of work needed to remove the Linux specific parts prevented new research from being done. Now they have independent development that doesn't rely on them back-porting and changing all the Linux-based dependencies in GNOME and KDE and allows Lumina to run on BSD based systems and Linux.

Lumina has been written from scratch in C++/Qt5 and is not based on any existing desktop’s code-base, and does not use any of the Linux-based desktop frameworks (ConsoleKit, PolicyKit, D-Bus, systemd, etc..) and is now available for Linux as well as VSD in the Project Trident distro based on Void Linux.

### Android

Android runs on the Linux Kernel and is in a sense a custom Linux Distro itself.  It has a custom rendering layer that does not use X or Wayland.

![*https://source.android.com/devices/graphics/*](images/Chapter-04/Android/ape_fwk_graphics-400-by-367.png "Android Rendering Layers")

### Who Uses What

----------------------------------------------------- ------------------------ -------------------------------
[KDE 5](https://www.kde.org/ "KDE") [^31]             Qt 5                     https://www.kde.org/
[GNOME 3](https://www.GNome.org/ "GNOME")             GTK+ 3                   https://GNome.org/
[Xfce](http://www.xfce.org/ "Xfce")                   GTK+ 3                   https://www.xfce.org/
[LXQT](http://lxqt.org/about/ "LXQT")                 Qt 5                     https://lxqt.org/about/
[MATE](http://mate-desktop.org/ "Ma-tay")             GTK+ 3                   https://mate-desktop.org/
[Cinnamon](http://cinnamon.linuxmint.com/ "Cinnamon") GTK+ 3                   https://cinnamon.linuxmint.com/
[Unity](https://unity8.io/ "unity 8 web page")        GTK+ 3                   https://unity8.io/
[Enlightenment](https://www.enlightenment.org/ "E24") EFL                      https://www.enlightenment.org/
[Lumina](https://lumina-desktop.org/ "lumina")        C++/Qt5                  https://lumina-desktop.org/
----------------------------------------------------- ------------------------ -------------------------------

Wikipedia has a sample gallery of all these desktop environments and more at [https://en.wikipedia.org/wiki/Desktop_environment#Gallery](https://en.wikipedia.org/wiki/Desktop_environment#Gallery "sample gallery").  As always there are many other desktops we couldn't cover.  Also keep in mind that most of these have been ported to work on the various BSDs as well.

### GNOME 3 Lockin Question

By 2012 the GNOME project was considered pretty mature opensource project. It was a complete desktop environment and had accomplished what it had set out to do back in 1999.  So much so that GNOME community contributed development began to wane [^29]. By that time there was one community developer working on GNOME full time and the other 10 were Red Hat Employees coincidentally. By the end 2012 the GNOME project voted to include Lennart Poettering's systemd as a hard dependency in GNOME. This had a two-fold effect.  This made GNOME 3 the default desktop of any system using the systemd init system, which is all of the two major families of Linux operating systems except for the Devuan/Debian fork. When you compare Debian, Fedora (Red Hat), and Ubuntu you see very little differentiation desktop-wise now.

Some people in the Free and Opensource world think that this amounts to a Linux coup d'etat and some would argue that it is just good business sense.  One wonders if there are clear signs or if this is the natural evolution of Linux.  Can Linux survive as an opensource project at this scale or will it have to become a commercially sponsored project?  For arguments sake, imagine if Red Hat could co-opt all of the Linux desktop market and even the Linux kernel.  What would that mean financially?  As of Ubuntu's 18.04 Bionic Beaver edition release, they have dropped the custom Unity shell and returned to using GNOME3.

### Theming

Each desktop environment has the ability to modify and display a theme on top of its shell.  GNOME 3 has been notoriously hard to modify. The GNOME Tweak Tool allows for the adjustment of several advanced GNOME options that can't be configured in gnome-control-center. This includes things like:

* fonts used in user interface elements and titlebar
* font hinting and aliasing
* alternative user interface themes
* changes in window management behavior
* behavior on laptop lid close
* file manager desktop icons
* icons in menus and buttons

Various [custom themes](http://www.noobslab.com/p/themes-icons.html "Themes") exist for Ubuntu. Some Ubuntu users went beyond changing the standard theme and implemented a copy of the Mac OSX theme called [MacBuntu](http://www.noobslab.com/2015/05/mbuntu-y-macbuntu-transformation-pack.html "MacBunutu") and also Windows 7 & 8 themes called [Mindows](http://www.noobslab.com/2015/06/do-you-like-windows-look-and-feel-but.html "Mindows"). Additional Ubuntu Icons matching the [Windows 7 & 8 icons](http://www.noobslab.com/2014/04/make-your-ubuntulinux-mint-look-like.html "Icons") can be installed as well.  Also themes touch on issues of usability.  [Ubuntu Touch theme](http://www.noobslab.com/2015/01/ubuntu-touch-theme-released-for-ubuntu.html "Ubuntu Touch") re-aligns Ubuntu to work on a tablet or phone and considers touch points more important then mouse and keyboard actions, but recent development on the Ubuntu Touch project has sadly ended.

### Gnome 3.3.x Features

![*GNOME 3*](images/Chapter-04/activities-overview-3.16-711x400.png "GNOME 3")

Everything in [GNOME 3](https://www.gnome.org/gnome-3/ "GNOME 3") starts with the __Activities__ button in the upper left hand corner.  There is no traditional "Start Button."  Just this sense of activities to be launched.  There is also a __Find__ box for searching everything in GNOME 3 from documents to applications to even suggested software. There is also a __favorites bar__ on the left hand side of the screen.  You will see preinstalled icons for FireFox Web Browser, Evolution E-mail client, Rhythm Box music player, Shotwell for picture management, the file manager is named Nautilus, the Software Store application, and finally a grid launcher for everything else.  Note there are no *"categories"* such as system tools or office software.  This is a design feature of GNOME 3.

![firefox](images/Chapter-04/ff.png "FF") ![Evolution](images/Chapter-04/evolution.png "Evolution") ![Rhythm Box](images/Chapter-04/rythembox.png "Rhythem Box") ![Shotwell](images/Chapter-04/shotwell.png "Shotwell") ![Nautilus](images/Chapter-04/files.png "File Manager") ![Software](images/Chapter-04/software.png "Software") ![Application Launcher](images/Chapter-04/application.png "Application")

You will notice a few other system designs or features.  For instance there is no logout button.  The little white triangle in the upper right hand corner next to the battery and sound icon controls poweroff and restart, but by default there is no logout button.  Once again this is a GNOME 3 design.  

Each application has a preferences and content menu area in GNOME 3.  It is located right next to the Activities button.  You will see the application name with a small white drop down arrow.

![*GNOME 3 Taskbar*](images/Chapter-04/taskbar.png "Taskbar")

In order to find the window commands for open, close, resize, tiling, and so forth you just need to right click on the gray toolbar on top of the window that has the focus.

![*GNOME 3 Toolbar*](images/Chapter-04/toolbar.png "Toolbar")

#### GNOME Extensions

To extend the functionality of GNOME 3 there is a [GNOME 3 extensions website](https://extensions.gnome.org "GNOME 3 extensions").  This site allows you to add on additional features to GNOME that you may want.  If visit the site while using Fedora or any GNOME 3 enabled site and you allow the GNOME plugin to run in your FireFox browser, then the website will allow you to interactively install plugins.  Try it.  Go to the second page and choose a plugin called *Caffeine*.  This is handy because it allows you to disable the screensaver and system suspend and is very handy if you are working on a virtual machine.  Note how the caffeine plugin simply places a coffee cup icon in the top toolbar? A few others you may want to try are the [Drop Down Terminal](https://extensions.gnome.org/extension/442/drop-down-terminal/ "Drop Down Terminal"), [Logout Button on Panel](https://extensions.gnome.org/extension/944/logout-button-on-panel/ "Add Logout button"), or the [System Monitor](https://extensions.gnome.org/extension/9/systemmonitor/ "System Monitor")

![*GNOME 3 Extensions*](images/Chapter-04/extensions.png "Extensions")

### Installing Windows Managers and Desktop Environments

Previously Linux distributions had made an effort to build in Software Stores, much like we saw in iOS and Android.   The issue with a software store became the ability to make money, charge money, and distribute money.  All though the distributions still support Software Stores, their heart is not in this manner of software installation.  The original way to install software was via a package manager, which the stores were a front for anyway.  There are two competing standards to replace packages or more appropriately bring "app" like functionality to Linux.  These are called [Flatpak](https://flatpak.org "Flatpak") on Fedora and [Snaps](https://www.ubuntu.com/desktop/snappy "Snaps").

To access the terminal on a GNOME3 desktop, click the **Activities** button at the top and in the **find** box type: *terminal*.
  
#### Ubuntu

> ```sudo apt-get update```  then ```sudo apt-get install i3 icewm fvwm flwm evilwm fluxbox dwm xmonad mwm xfce4```  
  
#### Fedora

> ```sudo dnf install i3 icewm xmonad mwm @xfce```

#### GNOME Software Store

![*GNOME Software Store*](images/Chapter-04/software-store.png "Software Store")

This is a feature added by Red Hat to improve upon Gnome Packages, which is the default package manager in GNOME 3. The package manager is called **Software**. There is a wide selection of free and opensource software to choose from.   In the meantime you can use the Software store to install the good old __GNOME Packages__ and __GNOME Update__ package manager and updater which will default to the old style and let you install pretty much everything.

### Ubuntu Unity Desktop - Deprecated

**As of April 2018 Ubuntu released Unity has been deprecated in favor of GNOME3, this section is kept for historical reference.**

[Unity](https://unity.ubuntu.com/ "Unity") is Ubuntu's GNOME 3 shell augmentation/replacement.  This means that Unity sits on top of GNOME 3 but has its interface drastically reimagined.  Unity focuses on two parts, the Application Launcher and the top panel.  Everything else is dedicated to screen space.  This is part of Ubuntu's goal to make their interface perform and scale on multiple screen sizes and devices not unlike Windows 10.  Unity services this day as part of the [Ubuntu Touch](https://ubports.com/ "Ubuntu Touch") mobile phone operating system.

## Conclusion

In this chapter we learned about the creation and evolution of the desktop GUI.  From ttys to X to Wayland and a modern compositor.  We also learned about window managers and the four major desktop environments.  Finally we learned about the major GUI desktop environment development kits and how each major DE uses them.

### Review Questions

Linux Desktop and GUI
Chapter 04 review questions

1) What was the original and most popular Unix “Smart Terminal?”
  a. VIC-100
  b. VT-100
  c. VT-220
  d. VC-100
2) What is the three letter abbreviation still in use today in modern Linux to refer to “terminal
devices?”
  a. TCY
  b. TTY
  c. VT-100
  d. Virtual Terminal
3) Why is the GNOME terminal and Windows cmd.exe terminal emulator screens 80 by 25 by
default?
  a. The technology cannot process any larger size
  b. The technology doesn’t need to have any larger screen size
  c. The developers of these technologies were seeking to emulate the popular VT-100 and
VT-220 terminals they used prior.
  d. Hey it's Windows, do they need a reason?
4) What is the key combo sequence you can hit to switch to a new virtual terminal in Linux?
  a. Alt + Ctrl + Del
  b. Alt + Ctrl + F1 - F7
  c. Right Ctrl
  d. Shift 5 times
5) What is the name of the original Unix based GUI that came out of MIT in ~1984?
  a. W
  b. X
  c. Y
  d. Z
6) True or False – X was originally not opensourced by MIT in 1984

7) For Ubuntu 18.04 what is the default desktop environment being used?

8) What is the name of the successor GUI compositor to X being created by the X.org foundation?
  a. KDE
  b. Y
  c. Wayland Project
  d. Jennings Project
9) What is the name of Ubuntu’s, now deprecated, GUI compositor replacement for X? (Just the name)

10) What are the 3 types of Linux window managers?

11) There are 4 major Linux desktop environments in use today: which grouping is correct?
  a. KDE, GNOME, CDE, LXDE
  b. KDE, GNOME, E17, GNUSTEP
  c. KDE, GNOME, X, LXDE
  d. KDE, GNOME, Xfce, LXDE
12) What is the name of the windowing toolkit that KDE uses?

13) What is the name of the windowing toolkit that GNOME uses?

14) What is the name of the founder of the GNOME project?

15) When the GNOME 3 desktop environment was released in early 2012, many people were
unhappy that many changes were made.  There were 3 major projects started to either preserve
GNOME 2 or to modify GNOME 3 significantly – what are the names of those projects?
  a. Enlightenment, LXDE, Xfce
  b. Mint, Unity, Mate
  c. Unity, Mate, Cinnamon
  d. Cinnamon, Mint, Mate
16) When released in 2006, what was the main development goal of the LXDE desktop environment?
  a. GUI desktop features
  b. Multi-desktop paradigm
  c. Energy saving and extremely fast
  d. Made for high end gaming systems
17) Which of these statements are true in regards to Linux desktop environments? (choose all that
apply)
  a. Desktop environments have a File Manager
  b. Desktop Environments have start or action buttons and task and notification bars
  c. Desktop environments have a changeable but consistent look-and-feel
  d. Desktop environments have system configuration tools and user applications built in
  e. Desktop environments have lower memory requirements than window managers
18) What is the default desktop environment for Fedora 32? (Name and versions)

19) What is the name of the button on the upper left hand corner of the GNOME 3 desktop that you use to “launch applications?”

20) What is the name of the default Ubuntu desktop environment as of April 2018?

### Podcast Questions

Please answer these questions from the Fedora Project podcast on [FLOSS - http://twit.tv/floss/71](http://twit.tv/floss/71 "Fedora Project")

* ~9:11 What is the Fedora Project?
* ~11:35 How does Red Hat make money on Fedora if it is free?
* ~12:30 What is the Fedora release cycle and can businesses use this release cycle?
* ~13:30 What is the relationship between Fedora and Red Hat Enterprise Linux (RHEL)?
* ~25:00 What percentage of the Fedora Project is open source?
* ~35:00 On further inspection is Fedora Project really opened source according to the Free Software Foundation?
* ~36:20 Does Fedora include proprietary Nvidia drivers? Why or why not?
* ~46:10 Who is the most famous Fedora user?
* ~1:01:00 What is the difference between CentOS and RHEL?

### Lab

Using the virtual machines you installed in the previous chapter, you will now install additional software, themes, desktop environments, and window managers. You will combine screenshots of this newly installed software into a single document for submission.

#### Package based install

**Deliverable:** Take screenshots of all successful installs of the software listed.  

#### GNOME 3 Extensions

You will need to install two GNOME 3 extensions from [https://extensions.gnome.org](https://extensions.gnome.org "Gnome extensions").  The first one is the example in the book called *Caffeine*. Make sure you have the Gnome Shell integration installed to configure and install plugins directly from the browser.

1) Caffeine
1) Dash to Dock
1) Freon by Ushakov Vasilii (Requires you to install the package ```lm_sensors```)
1) Screenshot Tool

#### Snaps Install

To install and configure snaps, reference chapter 3.  To show these packages are installed take a screenshot of the output of the command: `sudo snap list`. Install these packages via Snap on Ubuntu 18.04 desktop:

1) Android Studio
1) Blender
1) Slack
1) Skype
1) Visual Studio Code

#### Flatpak Install

To install and configure flatpak and flathub, reference chapter 3.  To show these packages are installed take a screenshot of the output of the command: `sudo flatpak list`. Install these packages via flatpak on the Fedora virtual machine:

1) Kdenlive
1) Visual Studio Code
1) Discord
1) Remmina
1) GtkStressTesting

#### Ubuntu 18.04 Flatpak Install

To install and configure flatpak and flathub, reference chapter 3.  To show these packages are installed take a screenshot of the output of the command: `sudo flatpak list`. Install these packages via flatpak:

1) Microsoft Teams
1) Shotcut
1) LibrePCB
1) OpenBoard

#### AppImage Install

Find 3 [AppImage install packages](https://appimage.org/ "AppImages install"), follow the instructions to install and run these AppImages on both Ubuntu 18.04 and Fedora 32.  Take a screenshot of the command needed to run the AppImage and the corresponding first screen of that application from the [AppImage GitHub repo](https://appimage.github.io/apps "AppImage GitHub Repo").

1) Poddr
1) Archipelago
1) LibrePCB

#### Python Packages

From Chapter 3, you need to install software packages using the Python pip3 installer and the Rust Language using their cargo package manager.

You can see an example of how to install Python language packages (eggs). Drone kit is an API for controlling [3D Robotics](https://www.3drobotics.com "drones") drones located at [dronekit.io](http://dronekit.io "drone kit").  To [install their Python development packages](https://dronekit-python.readthedocs.io/en/latest/guide/quick_start.html "Python packages") you need to use ```pip3``` the Python Package Installer.

```sudo apt-get install python3-pip python3-dev python3-setuptools```

```bash
pip3 install dronekit
pip3 install dronekit-sitl
```

From the command line, run the ```dronekit-sitl --version``` command and take a screenshot of the output.

Using the the ```pip3``` command install the Amazon Web Services Command Line toolkit from [https://aws.amazon.com/cli/](https://aws.amazon.com/cli/ "AWS CLI Install"). From the command line take a screenshot of the command ```aws --version```

#### Rust Packages

Using [Rust](https://www.rust-lang.org/ "Rust-lang"), follow the install instructions to install a Rust based version of the GNU coretools. Follow the tutorial to help you download and compile these tools with Rust, [https://github.com/uutils/coreutils](https://github.com/uutils/coreutils "Build Core-utils"); use the ```cargo build``` and ```cargo install``` commands. This will compile Rust based versions of all of the GNU C based coreutils.

To install the Rust-lang ```curl https://sh.rustup.rs -sSf | sh```

Run the command ```who --version``` and then ```uutils who --version``` and take a screenshot of the successful output.

#### Installing Window Managers

You will chose 1 of the window managers from the categories listed earlier in the chapter and install them.  Once installed you need to log out and restart your session.  In order to change the default window manager on GNOME3 desktop environment you need to click on the user name and select the little gear below the password field.  In your screenshot open a terminal window, you might need to do some research to understand how to operate in a window manager.

![*Change Window Managers*](images/Chapter-04/GNOME3/window-manager.png "Change")

1) Compositing window manager
1) Stacking window manager
1) Tiling window manager
1) Install Enlightenment (E17) on Ubuntu 18.04

**Note:** the names of packages are not always obvious so you can use search features of package managers.  For example here would be how to search for the i3 package.

* ```sudo apt-cache search i3```
* ```sudo dnf search i3```

#### Desktop Environment Installs

Install these desktops, restart your system and as you login switch your desktop environment and take a screenshot of the new environment.

1) Install the Xfce Desktop on Fedora 32
1) Install the Ubuntu Mate Desktop on Ubuntu 18.04
1) Install the Xfce4 Desktop on Ubuntu 18.04 (not xubuntu-desktop but just xfce4 package)
1) Download the KDE Neon Desktop distro (Ubuntu based) from [https://neon.kde.org/download](https://neon.kde.org/download "KDE desktop Neon")

#### Ubuntu Theme Tweaking

We will use the tutorial at Noobslab to transform our Ubuntu 18.04 Desktop into a MacBuntu.
Following the instructions here: [http://www.noobslab.com/2018/08/macbuntu-1804-transformation-pack-ready.html](http://www.noobslab.com/2018/08/macbuntu-1804-transformation-pack-ready.html "macbuntu")

The *Tweak tool* referred in the tutorial is the GNOME tweak tool:

![*GNOME Tweak Tool*](images/Chapter-04/gnome-tweak-tool.png "Tweak Tool")

**Deliverable:** Take screenshots of all successful installs of software.  See Blackboard for submission details.

#### Footnotes

 [^23]: <a href="http://www.allaboutapple.com/" rel="nofollow">http://www.allaboutapple.com/</a>
     <a  href="http://creativecommons.org/licenses/by-sa/2.5/it/deed.en">CC BY-SA 2.5 it</a>,
     <a href="http://creativecommons.org/licenses/by-sa/2.5/it/deed.en">CC BY-SA 2.5 it</a>,
     <a href="www.gnu.org/copyleft/fdl.html">GFDL</a> or
     <a href="http://creativecommons.org/licenses/by-sa/3.0/">CC-BY-SA-3.0</a>,
     <a href="https://commons.wikimedia.org/wiki/File%3AMacintosh_128k_transparency.png">via Wikimedia Commons</a>

 [^24]: By Original by David Gerard, recreated by Efitu (Wikimedia Commons)
     <a href="http://www.gnu.org/copyleft/fdl.html">GFDL</a> or
     <a href="http://creativecommons.org/licenses/by-sa/3.0/">CC-BY-SA-3.0</a>,
     <a href="https://commons.wikimedia.org/wiki/File%3AX_client_server_example.svg">via Wikimedia Commons</a>

  [^25]: By Jason Scott (Flickr: IMG_9976) <a href="http://creativecommons.org/licenses/by/2.0">CC BY 2.0</a>,
    <a href="https://commons.wikimedia.org/wiki/File%3ADEC_VT100_terminal.jpg">via Wikimedia Commons</a>

  [^26]: Diagram provided by: <a href="http://wayland.freedesktop.org/architecture.html">http://wayland.freedesktop.org/architecture.html</a>

  [^27]: [http://www.omgubuntu.co.uk/2014/03/mir-default-display-server-ubuntu-2016](http://www.omgubuntu.co.uk/2014/03/mir-default-display-server-ubuntu-2016)

  [^28]: <a href="https://commons.wikimedia.org/wiki/File:Miguel_de_Icaza.jpg#/media/File:Miguel_de_Icaza.jpg">Miguel de Icaza</a>
     Licensed under <a title="Creative Commons Attribution 2.0" href="http://creativecommons.org/licenses/by/2.0">CC BY 2.0</a>
     via <a href="https://commons.wikimedia.org/wiki/">Commons</a>.

  [^29]: <a href="https://blogs.gnome.org/otte/2012/07/27/staring-into-the-abyss/">https://blogs.gnome.org/otte/2012/07/27/staring-into-the-abyss/</a>

  [^30]: <a href="http://www.osnews.com/story/22225/RMS_De_Icaza_Traitor_to_Free_Software_Community/">http://www.osnews.com/story/22225/RMS_De_Icaza_Traitor_to_Free_Software_Community/</a>

  [^31]: Qt 5 / KDE 5 split into three separate components <a href="https://en.wikipedia.org/wiki/Qt_%28software%29#Qt_5">https://en.wikipedia.org/wiki/Qt_%28software%29#Qt_5</a>

  [^32]: KDE Plasma 5 retired KDM as the default display manager in favor of SDDM.  
     <a href="http://www.phoronix.com/scan.php?page=news_item&px=MTgyOTU">http://www.phoronix.com/scan.php?page=news_item&px=MTgyOTU</a>

  [^33]: Comparison of X Windows Desktop Environments
    <a  href="https://en.wikipedia.org/wiki/Comparison_of_X_Window_System_desktop_environments">https://en.wikipedia.org/wiki/Comparison_of_X_Window_System_desktop_environments</a>

  [^34]:  [http://arstechnica.com/information-technology/2008/01/nokia-buys-trolltech-will-become-a-patron-of-kde/](http://arstechnica.com/information-technology/2008/01/nokia-buys-trolltech-will-become-a-patron-of-kde/)

  [^35]: Miguel's response to Stallman's accusation <a href="http://tirania.org/blog/archive/2009/Sep-23.html">http://tirania.org/blog/archive/2009/Sep-23.html</a>

   [^36]: <a href="http://www.zdnet.com/article/linus-torvalds-finds-gnome-3-4-to-be-a-total-user-experience-design-failure/#!">http://www.zdnet.com/article/linus-torvalds-finds-gnome-3-4-to-be-a-total-user-experience-design-failure/#!</a>

   [^37]: <a href="http://www.zdnet.com/article/linus-torvalds-switches-back-to-gnome-3-x-desktop/">http://www.zdnet.com/article/linus-torvalds-switches-back-to-gnome-3-x-desktop/</a>

   [^38]: [https://plus.google.com/115250422803614415116/posts/KygiWsQc4Wm](https://plus.google.com/115250422803614415116/posts/KygiWsQc4Wm)

   [^39]: <a href="http://lxde.org/lxde/index.html">http://lxde.org/lxde/index.html</a>

   [^40]: <a href="http://unity.ubuntu.com/projects/unity">http://unity.ubuntu.com/projects/unity</a>

   [^41]: <a href="https://wiki.ubuntu.com/UnityNextSpec">https://wiki.ubuntu.com/UnityNextSpec</a>

   [^42]: <a href="http://unity.ubuntu.com/projects/appindicators">http://unity.ubuntu.com/projects/appindicators</a>

   [^43]: <a href="http://unity.ubuntu.com/projects/system-indicators/">http://unity.ubuntu.com/projects/system-indicators/</a>

   [^44]: <a href="http://unity.ubuntu.com/projects/notifyosd">http://unity.ubuntu.com/projects/notifyosd</a>
