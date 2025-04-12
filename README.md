# Release Notes for LINICS 1.01 (by [Hacktonics Ltd](https://hacktonics.io))

LINICS is a **Lin**ux <sup>:registered:</sup> based platform for **ICS** (Industrial Control Systems) security professionals. LIN+ICS = LINICS. Linux <sup>:registered:</sup> is the registered trademark of Linus Torvalds in the U.S. and other countries.

LINICS 1.01 is a Debian-based platform (specifically Debian 12 Bookworm). LINICS 1.01 is free software made available under the terms of the GNU General Public License 2.0. The license text is available at: [https://www.gnu.org/licenses/gpl-2.0.html](https://www.gnu.org/licenses/gpl-2.0.html) and under `/usr/share/common-licenses/GPL-2`. Under the GPL license, you can redistribute it and/or modify it under the terms of the license.

> Note: The GPL-2 license applies to the base operating system and a subset of the tools. Some of the included software has its own license terms which you should peruse before deciding to modify or redistribute it for any purpose.

LINICS 1.01 is distributed as a helpful resource for ICS security professionals but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details. As this software is for security researchers, it is to be used only for ethical research and investigations to support improvements in security of industrial control systems. 

> Users of LINICS 1.0 can update without the need to reinstall. See [Instructions](#whats-different-in-linics-101-vs-linics-10)

# Supported architectures

LINICS 1.01 is available for 64-bit PC (AMD64) architectures. Currently, no ARM version is available. The distribution is available in ISO format as well as virtual machines for KVM, VMWare and VirtualBox. [For downloads, visit: https://hacktonics.io/linics/](https://hacktonics.io/linics/) 

# System requirements

Recommended minimum system requirements: 4 GB RAM, 50 GB Hard Disk Space, 2 Processor Cores

LINICS 1.01 works well with the above minimum requirements. You can run it with 2 GB RAM and 1 CPU core but performance will take a hit. While 30 GB disk space will work, you are likely to fill it up quickly as tools collect data.

If your system has capacity, providing more RAM or cores is, of course, advised.

# How to install LINICS 1.01

You can install LINICS using the ISO image available at [https://hacktonics.io/linics/](https://hacktonics.io/linics/). It is a live image so you can boot it in a virtualisation platform of your choice. Once you reach the desktop of the live image, explore LINICS 1.01 (but do see [limitations of the live boot image](#dockerised-tools-and-live-boot)). On the desktop taskbar, there is a LINICS installer icon. This will take you to the Calamares installer which will guide you step-by-step. The installation is very straight forward especially if you are not manually partitioning disks.

You can also create a live boot USB stick using this ISO by using tools such as Etcher or Rufus. This can then be used to boot a machine where you are installing LINICS 1.01 and follow the same installation process above (but do see [bootloader issues](#bootloader-issues)).

Alternatively, you can download one of our pre-built VMs suitable for VMWare, Virtualbox or KVM. These are available at: [https://hacktonics.io/linics/](https://hacktonics.io/linics/).

# Tools included in LINICS 1.01

## Scanners

### ZathrICS by HacktonICS

#### About
> "Zathras warned Zathras, but Zathras never listens to Zathras." - Zathras

ZathrICS was built by HacktonICS specifically for LINICS, as a combined tool for performing active scanning of OT networks. ZathrICS provides a framework for performing active asset discovery, primarily using Nmap. The tool is configured to help reduce the risk of active scanning, for example by only allowing device idenitfication scripts to be run against devices which have appropriate network ports open. 

The tool is named after Zathras from Babylon 5. In Babylon 5, Zathras was the keeper of the great machine and knew all of its secrets.

#### Usage 

Launch ZathrICS through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "zathrics" in a new terminal. 

Further instructions on usage are provided within the tool.

### PLCScan


#### About
PLCScan is an older scanning tool which is able to scan for older Siemens S7 and Modbus devices. It is able to identify device details, such as model number and firmware versions, for Siemens devices, and unit/slave IDs for modbus devices. 

For newer devices, the equivalent nmap nse scripts should be used, such as s7-info  or modbus-discover, which are part of the base nmap install. You can use these directly in nmap, through the Zenmap graphical frontend for nmap, or through the ZathrICS scanning tool. 

PLCScan has been installed within a docker container for LINICS to maintain dependencies in newer Linux versions without Python 2.  

#### Usage 

PLCScan can be launched either graphically through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "plcscan" in a new terminal.

The launcher will display some instruction on how to use the tool, or the man page can be viewed by typing "man plcscan" in a new terminal. 

#### Acknowledgements
PLCScan was taken from Meeas' repository on Github [https://github.com/meeas/plcscan](https://github.com/meeas/plcscan), which is forked from code from Dmitry Efanov (Positive Research) originally posted to Google Code. 

### arp-scan


#### About

arp-scan is a network scanning tool that uses the ARP protocol to discover and fingerprint IPv4 hosts on the local network.

#### Usage 
arp-scan can be launched either graphically through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "arp-scan" in a new terminal.

The launcher will display some instruction on how to use the tool, or the man page can be viewed by typing "man arp-scan" in a new terminal. 

The arp-scan wiki on GitHub provides further instruction on using the tool [https://github.com/royhills/arp-scan/wiki/arp-scan-User-Guide](https://github.com/royhills/arp-scan/wiki/arp-scan-User-Guide).

#### Acknowledgements
arp-scan was created and is maintained by royhills on Github [https://github.com/royhills/arp-scan](https://github.com/royhills/arp-scan).

### netdiscover

#### About
netdiscover is a network address discovery tool, based on arp requests. The tool will reveal accessible IP addresses on the local network.  

#### Usage 
netdiscover can be launched either graphically through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "sudo netdiscover" in a new terminal (must be run as root).

The tool will scan the network. The list of accessible hosts will be updated as new hosts are discovered. 

The launcher will display some instruction on how to use the tool, or the man page can be viewed by typing "man netdiscover" in a new terminal. 

#### Acknowledgements
netdiscover was created and is maintained by Jaime Penalba on Github [https://github.com/netdiscover-scanner/netdiscover](https://github.com/netdiscover-scanner/netdiscover).

### nmap

#### About
nmap is a industry-standard network mapping tool. As well as a rich core feature set identifying and figerprinting network hosts, nmap features a large number of nse scripts for performing specialised functions. 
Some of these nse scripts are specifically designed for use against ICS devices. Some additonal ICS specific scripts have been included.

Note that nmap can perform intense scans against devices. This can potentially cause problems with legacy ICS devices, including triggering denial of service conditions. Therefore, nmap should be used with caution within OT networks. 

#### Usage 

Nmap can be launched either graphically through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "nmap" in a new terminal.

The Zenmap graphical interface for nmap is also provided, which can be easier to use for novice users. This can be launched either through the menu, or by typing "sudo zenmap" in a terminal.

The ZathrICS tool also provides an ICS specific front end for running nmap scans. 

#### Acknowledgements
nmap was created by Gordon Lyon. The nmap homepage is accessible at [https://nmap.org/](https://nmap.org/).

### DIRB


#### About
DIRB is a web content scanner. It looks for existing (and/or hidden) Web Objects. It  works by launching a dictionary based attack against a web server and analysing the responses.

#### Usage 

DIRB can be launched either graphically through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "dirb" in a new terminal.
A wordlist will need to be provided. DIRB provides a set of wordlists available in /usr/share/dirb/wordlists

The launcher will display some instruction on how to use the tool, or the man page can be viewed by typing "man dirb" in a new terminal. 

#### Acknowledgements

DIRB was created by The Dark Raver. The homepage of DIRB is available at [https://dirb.sourceforge.net/](https://dirb.sourceforge.net/)

### Grassmarlin

#### About
Grassmarlin is a passive asset discovery tool for OT networks. Grassmarlin can ingest network captures and will display the network topology that can be derived from the observed communication. 
The tool can also extract information about devices if observed in the network traffic. 

#### Usage 

Grassmarlin can be launched either graphically through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "grassmarlin" in a new terminal.

Grassmarlin can ingest data from pcap files. These can be collected by using Wireshark. When saving a file in Wireshark, you must save as a ".pcap" file rather than as ".pcapng". 

The user guide for Grassmarlin is available on Github [https://github.com/nsacyber/GRASSMARLIN/blob/master/GRASSMARLIN%20User%20Guide.pdf](https://github.com/nsacyber/GRASSMARLIN/blob/master/GRASSMARLIN%20User%20Guide.pdf)

#### Acknowledgements
Greasmarlin was created by the NSA, and is available on Github at [https://github.com/nsacyber/GRASSMARLIN](https://github.com/nsacyber/GRASSMARLIN).

## Exploitation

### Industrial Exploitation Framework - ISF

#### About
ISF (Industrial Exploitation Framework) is an exploitation framework based on Python. It is similar to the Metasploit framework. It features a number of modules for scanning and interacting with ICS devices. 

ISF has been installed within a docker container for LINICS to maintain dependencies in newer Linux versions without Python 2.

#### Usage

ISF can be launched either graphically through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "isf" in a new terminal.

Once launched, you can print the list of modules by typing "show all". Loading modules, setting options and running exploits works in the same way as Metasploit. 

For tools which require a network interface to be specified, you should manually specify the name of the interface of your machine, which may differ from the default eth0.

#### Acknowledgements

ISF is by dark-lbp and is available on GitHub at [https://github.com/dark-lbp/isf](https://github.com/dark-lbp/isf).

### Industrial Exploitation Framework - ISEF

#### About
ISF(Industrial Security Exploitation Framework) is an exploitation framework based on Python. It is based on NSA Equation Group Fuzzbunch toolkit which is released by Shadow Broker. It features a number of modules for scanning and interacting with ICS devices. 

ISEF has been installed within a docker container for LINICS to maintain dependencies in newer Linux versions without Python 2.

#### Usage 

ISEF can be launched either graphically through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "isef" in a new terminal.

#### Acknowledgements

ISEF is by w3h and developed by the ICSMASTER Security Team. It is available on GitHub at [https://github.com/w3h/isf](https://github.com/w3h/isf).

### Ethersploit-IP

#### About
EtherSploit/IP is an interactive shell with a bunch of helpful commands to exploit EtherNet/IP vulnerabilities. More specifically, this tool explores the way Rockwell Micrologix PLCs communicate using EtherNet/IP and abuse some of its original functionalities.

#### Usage 

Ethersploit-IP can be launched either graphically through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "ethersploit" in a new terminal.

A list of supported commands is available at the GitHub link below. 

#### Acknowledgements
EtherSploit-IP is by Thiago Alves and is available from GitHub at [https://github.com/thiagoralves/EtherSploit-IP](https://github.com/thiagoralves/EtherSploit-IP)

### Smod

#### About
Smod is a modular framework with every kind of diagnostic and offensive feature you could need in order to pentest the Modbus protocol. It is a full Modbus protocol implementation using Python and Scapy.

Smod has been installed within a docker container for LINICS to maintain dependencies in newer Linux versions without Python 2.

#### Usage 

Smod can be launched either graphically through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "smod" in a new terminal.

Once launched, type "show modules" to show a list of available modules. Loading modules, setting options and running exploits works in the same way as Metasploit. 

#### Acknowledgements
Smod is from Joshua1909 on GitHub [https://github.com/Joshua1909/smod](https://github.com/Joshua1909/smod)

### OPC-UA Exploitation Framework

#### About
The OPC-UA Exploitation Framwork includes a number of tools for interacting with OPC-UA servers. These tools can extract information, or perform attacks such as denial of service. 

A full list of features is available at the GitHub link below or by typing "man opcua-ef" in a terminal. 

The tool has been installed within a docker container for LINICS to maintain dependencies without relying on a virtual python environment. 

#### Usage 
The OPC-UA Exploitation Framework can be launched either graphically through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "opcua-ef" in a new terminal.

#### Acknowledgements

The OPC-UA Exploitation Framework is from Team82 at Claroty and is available on GitHub at [https://github.com/claroty/opcua-exploit-framework](https://github.com/claroty/opcua-exploit-framework)

### Metasploit

#### About
Metasploit is a penetration testing framework. It features a large number of modules for enumerating and exploiting hosts and devices. 
Metasploit includes a few ICS specific modules. Some additonal ICS specific modules have been included, visible in the LINICS release notes on GitHub. 

#### Usage 

Metasploit can be launched either graphically through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "msfconsole" in a new terminal.
Note that some modules require metasploit to be run as root. If so, run from the terminal using "sudo msfconsole". The graphical launcher, by default, launches with sudo.

The Metasploit documentaion is available at [https://docs.metasploit.com/](https://docs.metasploit.com/)

#### Warning

Metasploit will be updated with apt-update. Due to the nature of metasploit modules, updating metesploit may trigger alerts on monitored networks. 

#### Acknowledgements

Metasploit is developed by Rapid7 and is available from [https://www.metasploit.com/](https://www.metasploit.com/).

## Web Security

### Nikto

#### About
Nikto is a web server scanner, able to perform extensive fingerprinting and testing of web servers in order to identify potential vulnerabilities. 
Many OT devices and software now feature web servers, which can be scanned with Nikto. 

#### Usage 
Nikto can be launched either graphically through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "nikto" in a new terminal.

Nikto documentation is available as a GitHub wiki at [https://github.com/sullo/nikto/wiki](https://github.com/sullo/nikto/wiki)

The launcher will display some instruction on how to use the tool, or the man page can be viewed by typing "man nikto" in a new terminal. 

#### Acknowledgements

Nikto was developed by Chris Sullo and is available on GitHub at [https://github.com/sullo/nikto](https://github.com/sullo/nikto)

### BurpSuite Community Edition

#### About
Burpsuite is a powerful website testing tool for examining websites and web servers. The tool includes features such as a proxy which enables the user to modify web requests and responses.
The tool can be used to identify and exploit vulnerabilities on the web servers that appear on OT devices and software. 

#### Usage 

BurpSuite can be launched either graphically through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "BurpSuiteCommunity" in a new terminal.

The Burpsuite documentation is available at [https://portswigger.net/burp/documentation/desktop](https://portswigger.net/burp/documentation/desktop)

#### Acknowledgements
Burpsuite Community Edition is developed and maintained by PortSwigger, and available at [https://portswigger.net/burp/communitydownload](https://portswigger.net/burp/communitydownload)

## Password Cracking

### Hydra

#### About
Hydra is a powerful online and offline password cracking utility. It can perform online dictionary based password attacks against multiple protocols. 

#### Usage 
Hydra can be launched either graphically through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "hydra" in a new terminal.

A long list of example commands is available at the GitHub link below. A graphical front end is provided by Hydra Graphical (xhydra).

The launcher will display some instruction on how to use the tool, or the man page can be viewed by typing "man hydra" in a new terminal. 

#### Acknowledgements
Hydra is from Van Hauser / THC, with modules written by others, and is available on GitHub at [https://github.com/vanhauser-thc/thc-hydra](https://github.com/vanhauser-thc/thc-hydra)

### Hydra Graphical

#### About

Hydra Graphical is a graphical frontend for Hydra. 

#### Usage 

Hydra Graphical can be launched either graphically through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "xhydra" in a new terminal.

#### Acknowledgements
Hydra is from Van Hauser / THC, with modules written by others, and is available on GitHub at [https://github.com/vanhauser-thc/thc-hydra](https://github.com/vanhauser-thc/thc-hydra)

### John The Ripper

#### About
John the Ripper is an Open Source password security auditing and password recovery tool available for many operating systems.

#### Usage

John can be launched either graphically through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "john" in a new terminal.
 
Documentation on usage is available at [https://openwall.info/wiki/john/tutorials](https://openwall.info/wiki/john/tutorials)

The launcher will display some instruction on how to use the tool, or the man page can be viewed by typing "man john" in a new terminal. 

#### Acknowledgements

John is developed by OpenWall. The homepage is available at [https://www.openwall.com/john/](https://www.openwall.com/john/)
John is availabel on GitHub at [https://github.com/openwall/john](https://github.com/openwall/john)

## Person-in-the-Middle

### Ettercap

#### About

Ettercap is a person-in-the-middle framework for intercepting and modifying network communications, through techniques such as ARP spoofing.  
Ettercap can idenitify hosts on a network, and through user-provided filters, modify the traffic of the victims of arp spoofing. 
Many industrial protocols are susceptible to person-in-the-middle attacks. 

#### Usage 

Ettercap can be launched either graphically through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "ettercap -T" (for command line interface) or "ettercap -G" (for graphical interface)  in a new terminal.
 
#### Acknowledgements
Ettercap is originally developed by Alberto Ornaghi and Marco Valleri, now developed by a larger team. The homepage is available at [https://www.ettercap-project.org/](https://www.ettercap-project.org/)

### Bettercap

#### About
bettercap is a powerful, easily extensible and portable framework written in Go which aims to offer to security researchers, red teamers and reverse engineers an easy to use, all-in-one solution with all the features they might possibly need for performing reconnaissance and attacking WiFi networks, Bluetooth Low Energy devices, wireless HID devices, CAN-bus and IPv4/IPv6 networks

#### Usage 
Bettercap can be launched either graphically through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "sudo bettercap" (for command line interface) or "sudo bettercap_ui" (for web interface)  in a new terminal.

Note that in some cases, you may get an error message on start saying "Could not detect gateway.". If this happens, then run from the terminal as above with the addional parameter of "-gateway-override <ip>", replacing "<ip>" with your IP address on the interface you wish to use. 

Documentation is available at [https://www.bettercap.org/usage/](https://www.bettercap.org/usage/)

#### Acknowledgements
Bettercap is available at [https://www.bettercap.org/](https://www.bettercap.org/)

## Forensics

### Volatility

#### About
The Volatility Framework is a completely open collection of tools, implemented in Python under the GNU General Public License, for the extraction of digital artifacts from volatile memory (RAM) samples.

#### Acknowledgements
Volatility is maintianed by the Volatility Foundation and is available on GitHub at [https://github.com/volatilityfoundation/volatility](https://github.com/volatilityfoundation/volatility).

#### Usage 
Volatility can be launched either graphically through the Applications Menu, via the LINICS launcher on the taskbar, or by typing "volatility" in a new terminal.

Usage documentation is available on the GitHub wiki at [https://github.com/volatilityfoundation/volatility/wiki](https://github.com/volatilityfoundation/volatility/wiki) or by typing "man volatility" in a terminal.

# Python

A specific Python3 virtual environment has been set up under `/opt/venv`. Libraries such as `opcua`, `pycomm3`, `pymodbus`, `scapy`, `python-snap7` have been installed there. The PATH has been updated to look for Python there first. Shebangs of relevant scripts have been updated to specifically use that venv. So you will be able to work with these libraries directly without having to create your own virtual environment or activate this venv. You can, of course, activate it explicitly. You can also install additional libraries in that venv using sudo. Or you can use your own venv that you set up. However, do note that, for any scripts and libraries that any pre-installed software requires, the system will utilise /opt/venv. 

# What's different in LINICS 1.01 vs. LINICS 1.0

We have fixed some bugs in [ZathrICS](#zathrics-by-hacktonics), a tool included within LINICS. You do not need to reinstall LINICS 1.01 to update the system. You can download [this update script](https://www.hacktonics.io/linics-downloads/update-linics1.0.sh) and run it. It will download the fixed version of Zathrics and replace the previous version. Note that you will need to make the script executable: `chmod a+x update-linics1.0.sh`. The script will ask for you to authorise sudo privileges.

# Known Issues

> We advise to backup and make recovery media for any system where you are installing LINICS 1.01. We also advise running LINICS 1.01 in a hypervisor. VM downloads are provided for several virtualisation environments.

## Dockerised tools

### sudo for dockerised tools

Several of the older tools have been put into docker containers to cater for their dependencies. This is particularly an issue for tools that use different Python versions. This requires them to be run as sudo. Launching them will require you to elevate permissions whether you are using the desktop launchers or doing so from the command line on a terminal. We take the view that users should know when they are elevating permissions. If you find this frustrating, then you can create a `docker` group and add your user to that group as described in the docker documentation [Linux post-installation steps for Docker Engine](https://docs.docker.com/engine/install/linux-postinstall/). 

### Dockerised tools and Live Boot

LINICS 1.01 has a firstboot service that automatically loads all docker images ready for use. However, the Live Boot creates a RAM disk which is limited in size. So Live Boot will not load all images. The purpose of the Live Boot is to try out LINICS 1.01. So this is not a bug per se. For the full functionality, you should install LINICS 1.01, preferably in a VM environment.

## Bootloader issues

### Installing on a system that had another OS previously

If you are installing LINICS 1.01 on a machine as its only OS, some systems do not allow the Calamares installer to write to the EFI partition. As a result the system won't boot into LINICS 1.01. Resetting the BIOS to defaults and reinstalling LINICS 1.01 should fix this issue.

### Installing alongside existing operating systems

If you are installing LINICS 1.01 alongside other operating systems, GRUB's OS list sometimes does not update so you will not see LINICS 1.01 in the list of operating systems on GRUB. This is not fixed even if OS prober is on and is explicitly invoked. This can be fixed by adding a custom GRUB entry in `/etc/grub.d/40_custom` and regenerating the GRUB config. This will bring the LINICS 1.01 boot options into the GRUB menu.

## Severe issues 

### Live Boot and Bitlocker

Some issues have been reported whereby just using the Live Boot USB causes issues with Bitlocker on Windows-based System leading to an inability to boot. The issues are not fatal and systems are recoverable. However, this can be time consuming. *We, therefore, advise using LINICS 1.01 in a VM environment and only using the Live USB for initial exploration or as an installation medium.* 

# Reporting Bugs

You can report any issues via this Github page (using the *Issues* tab). We will endeavour to respond to the issues and add any fixes to our backlog as we develop LINICS further.

