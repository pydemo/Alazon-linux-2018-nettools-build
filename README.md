# Amazon-linux-2018-nettools-build

build: http://www.linuxfromscratch.org/blfs/view/svn/basicnet/net-tools.html

## SSH port
```
 sudo netstat -tnlp | grep :22
```

Package Information
Download (HTTP): http://anduin.linuxfromscratch.org/BLFS/net-tools/net-tools-CVS_20101030.tar.gz

Download (FTP): ftp://anduin.linuxfromscratch.org/BLFS/net-tools/net-tools-CVS_20101030.tar.gz

Download MD5 sum: 6be14ed473cacdd68edeaa9605adc469

Download size: 288 KB

Estimated disk space required: 7.0 MB

Estimated build time: less than 0.1 SBU

Additional Downloads
Required patch: http://www.linuxfromscratch.org/patches/blfs/svn/net-tools-CVS_20101030-remove_dups-1.patch

User Notes: http://wiki.linuxfromscratch.org/blfs/wiki/net-tools

Installation of Net-tools
The instructions below automate the configuration process by piping yes to the make config command. If you wish to run the interactive configuration process (by changing the instruction to just make config), but you are not sure how to answer all the questions, then just accept the defaults. This will be just fine in the majority of cases. What you're asked here is a bunch of questions about which network protocols you've enabled in your kernel. The default answers will enable the tools from this package to work with the most common protocols: TCP, PPP, and several others. You still need to actually enable these protocols in the kernel—what you do here is merely tell the package to include support for those protocols in its programs, but it's up to the kernel to make the protocols available.

[Note] Note
This package has several unneeded protocols and hardware device specific functions that are obsolete. To only build the minimum needed for your system, skip the yes command and answer each question interactively. The minimum needed options are 'UNIX protocol family' and 'INET (TCP/IP) protocol family'.

The patch below cleans up the installation so that it does not overwrite the ifconfig and hostname programs that were installed in LFS.

Install Net-tools by running the following commands:

patch -Np1 -i ../net-tools-CVS_20101030-remove_dups-1.patch &&
sed -i '/#include <netinet\/ip.h>/d'  iptunnel.c &&

yes "" | make config &&
make
This package does not come with a test suite.

Now, as the root user:

make update
Command Explanations
sed -i '/#include <netinet\/ip.h>/d' iptunnel.c: This fixes build breakage with linux-4.8 headers.

yes "" | make config: Piping yes to make config skips the interactive configuration and accepts the defaults.

Contents
Installed Programs:
arp, ipmaddr, iptunnel, mii-tool, nameif, netstat, plipconfig, rarp, route, and slattach
Installed Libraries:
None
Installed Directories:
None
Short Descriptions
arp

is used to manipulate the kernel's ARP cache, usually to add or delete an entry, or to dump the entire cache.

ipmaddr

adds, deletes and shows an interface's multicast addresses.

iptunnel

adds, changes, deletes and shows an interface's tunnels.

mii-tool

checks or sets the status of a network interface's Media Independent Interface (MII) unit.

nameif

names network interfaces based on MAC addresses.

netstat

is used to report network connections, routing tables, and interface statistics.

plipconfig

is used to fine tune the PLIP device parameters, to improve its performance.

rarp

is used to manipulate the kernel's RARP table.

route

is used to manipulate the IP routing table.

slattach

attaches a network interface to a serial line. This allows you to use normal terminal lines for point-to-point links to others computers.
