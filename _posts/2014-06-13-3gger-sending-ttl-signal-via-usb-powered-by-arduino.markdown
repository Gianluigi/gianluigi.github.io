---
layout: post
title: "3gger: sending TTL trigger signals via USB, powered by Arduino"
date: 2014-06-08 17:41:51 +0200
comments: true
tagline: High accuracy TTL triggering via Arduino
tags: [c++, arduino, qt] 
image:
  feature: texture-home.jpg
---

Sending TTL trigger with a high temporal resolution (< 0.1 ms) required me
to design a simple device controlled by a PC via a USB connection. The
result is a small Open Source project I called [3gger] and licensed under
the [MIT license]. 

## The problem

Working with different devices in the [Neuroscience] field, one common
application I faced is to synchronize different devices by means of [TTL]
signals with a high temporal accuracy. One possible solution is to use
a PC's [parallel port] to send signals via the 8 pins available on its
data port address either using [custom
software](http://retired.beyondlogic.org/porttalk/porttalk.htm), or, as it
is more common, by a stimulus delivery software ([e-Prime],
[Presentation], [Matlab PsychToolbox], [PsychoPy]), just to name a few. 

Using a PC usually means using a non-realtime OS, either Windows/Linux/Mac
OS X, so the latency achieved by these solutions is in the range of a few
milliseconds. That's perfectly fine for a lot of applications, leading to
to a vast ecosystem of applications and devices that make use of this
technique with success. The problem arises for studies that requires
a really low latency, usually under 1 ms, there's really  the need to find
alternate solutions, application that could take advantage of a high
resolution synchronization is the Paired Associative Stimulation ([PAS]),
or the [Triple stimulation].


## The project 

Now it is the time to introduce the [3gger] project, a simple solution
based on the [Arduino] board and available on [GitHub] as an open source
problem released under the [MIT license].

The use of an [Arduino] board allowed me to build a reliable and realtime
platform for the TTL trigger generation, while keeping the implementation
very simple.
When I started, The objectives of the project were:

* Deliver variable interval TTL pulsesi with a resolution of 0.1 ms 
* Easy to use GUI software to design simple protocols 
* Protocols saved in XML files 
* Device powered directly by the USB port
* Possibility to set a repetition rate for the protocol 
* Cross platform control software: available on Windows, Linux and Mac OS X
  
## Building the system

The latest version of the software is *[available on
Github](https://github.com/gianluigi/3gger)*.  In order to build the
software you need the [QT library] 5.x and the [Arduino] enviroment. You
can refer to the QT Project page for your platform's installation
instructions, here I'll cover the compilation of the project.

### Building the PC software

Once the dependencies are satisfied, you can choose between two
alternatives to build the software: 

1. Use the [Qt Creator] IDE: just open qmake project file 3gger.pro in the
   /src directory, and select Build -> Build All from the menu 
2. The command line: here's a simple command line, the commands described
   here should be "platform indipendent", alas, they should work on every
   platform supported by the project:

~~~ sh
git clone git@github.com:Gianluigi/3gger.git
cd 3gger
cd src
qmake
make release
~~~

The main application window looks like this (under KDE): 

![Application main window]({{ site.url }}/images/3gger_main.png)


### Building the firmware

The firmware has been tested on a [Arduino Uno] and [Arduino duemilanove]
boards. The easiest way to build the firmware is via the [Arduino IDE].
Just load the sketch *rtstim.pde* in the */firmware* directory and build
and upload the code to the arduino board.  If you feel _advanced_ you can
use the provided Makefile in the firmware directory to build via command
line the firmware. The makefile is provided by the [Arduino-Makefile]
project.

## What's next

In the next posts I'll cover the board assembly, providing a simple
circuit design  in order to illustrate the connections needed by the
system. 

I hope you may find the project useful, since the idea behind it is really
simple but opens to lots of applications. Any feedback is really
appreciated, since I'm starting to make some major addition to the
software, and it's actively developed again.  

[Neuroscience]: http://en.wikipedia.org/wiki/Neuroscience
[TTL]: http://en.wikipedia.org/wiki/Transistor%E2%80%93transistor_logic
[e-Prime]: http://www.pstnet.com
[Presentation]: http://www.neurobs.com
[PsychoPy]: http://psychopy.org
[Matlab PsychToolbox]: http://psychtoolbox.org
[PAS]: http://www.ncbi.nlm.nih.gov/pubmed/16106657
[3gger]: https://github.com/gianluigi/3gger
[GitHub]: https://github.com
[Arduino]: http://arduino.cc 
[parallel port]: http://en.wikipedia.org/wiki/Parallel_port 
[MIT license]: https://github.com/Gianluigi/3gger/blob/master/LICENSE.txt
[Triple stimulation]: http://brain.oxfordjournals.org/content/122/2/265.long 
[Qt library]: http://qt-project.orgo  
[Arduino Uno]: http://arduino.cc/en/Main/ArduinoBoardUno
[Arduino duemilanove]: http://arduino.cc/en/Main/ArduinoBoardDuemilanove
[Arduino IDE]: http://arduino.cc/en/Main/Software
[Arduino-Makefile]: https://github.com/sudar/Arduino-Makefile
