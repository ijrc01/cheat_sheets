Whatmask v1.2
=====================================
Nov. 14, 2003

By: Joe Laffey <joe@laffeycomputer.com>
Updates: http://www.laffeycomputer.com/software.html
<c> 2000-2003 Joe Laffey.
Subject to the terms of the GPL.



WINDOWS NOTE:

Whatmask is a command-line (DOS Shell) program. You must run it
with arguments from within a Command Prompt window (and not by
double-clicking it from the desktop.)




========
Whatmask
========

Whatmask is a small C program that will help you with network settings.

Whatmask can work in two modes. The first mode (which is how prior versions
worked) is to invoke Whatmask with only a subnet mask as the argument. In 
this mode Whatmask will echo back the subnet mask in four formats, plus
the number of useable addresses in the range.

Netmask Notations supported:

 Name                  Example
---------------------------------
 CIDR                         /24
 Netmask            255.255.255.0
 Hex Netmask           0xffffff00
 Wilcard Bits           0.0.0.255


The above notations are all identical. CIDR notation commonly has a "/" in
front of the number (representing the number of bits). Whatmask can accept
these notations with or without a slash. This notation is used more and more
recently. A lot of popular routers and software support this notation.

Netmask notation is pretty much the standard old-school way of doing it. It 
is supported by most systems (Un*x, Win, Mac, etc.).

Netmasks are sometimes represented as hexadecimal values, especially in
the BSD, such as NetBSD (http://www.netbsd.org/), my favorite.

Wilcard bits are similar to the netmask, but they are the logical not of the
netmask. This notation is used by a number of popular routers (and nobody
knows why...).

To use Whatmask in the original mode simply type "whatmask <notation>" The
notation can be in any of the four formats, and Whatmask will automagically
figure out what it is and display all four notations.

To find out more about subnets and netmasks see the References section below.

To use Whatmask in its second mode execute Whatmask with any ip address
within the subnet, followed by a slash ('/'), followed by the subnet mask in
any format. (e.g. 192.168.0.23/255.255.255.224, or 192.168.0.23/27)

Whatmask will echo back the following:

- The netmask in the following formats: CIDR, Netmask, Hex, Wildcard Bits
- The Network Address
- The Broadcast Address
- The number of Usable IP Addresses
- The First Usable IP Address
- The Last Usable IP Address

(Whatnet assumes that the Broadcast address is the highest address in the
subnet. This is the most common configuration.)




Whatnet Examples
================

myhost> whatmask /26

---------------------------------------------
       TCP/IP SUBNET MASK EQUIVALENTS
---------------------------------------------
CIDR = .....................: /26
Netmask = ..................: 255.255.255.192
Netmask (hex) = ............: 0xffffffc0
Wildcard Bits = ............: 0.0.0.63
Usable IP Addresses = ......: 62


myhost> whatmask 255.255.192.0

---------------------------------------------
       TCP/IP SUBNET MASK EQUIVALENTS
---------------------------------------------
CIDR = .....................: /18
Netmask = ..................: 255.255.192.0
Netmask (hex) = ............: 0xffffc000
Wildcard Bits = ............: 0.0.63.255
Usable IP Addresses = ......: 16382


myhost> whatmask 0xffffffe0

---------------------------------------------
       TCP/IP SUBNET MASK EQUIVALENTS
---------------------------------------------
CIDR = .....................: /27
Netmask = ..................: 255.255.255.224
Netmask (hex) = ............: 0xffffffe0
Wildcard Bits = ............: 0.0.0.31
Usable IP Addresses = ......: 30


myhost> whatmask 0.0.0.31

---------------------------------------------
       TCP/IP SUBNET MASK EQUIVALENTS
---------------------------------------------
CIDR = .....................: /27
Netmask = ..................: 255.255.255.224
Netmask (hex) = ............: 0xffffffe0
Wildcard Bits = ............: 0.0.0.31
Usable IP Addresses = ......: 30



myhost> whatmask 192.168.165.23/19

------------------------------------------------
           TCP/IP NETWORK INFORMATION
------------------------------------------------
IP Entered = ..................: 192.168.165.23
CIDR = ........................: /19
Netmask = .....................: 255.255.224.0
Netmask (hex) = ...............: 0xffffe000
Wildcard Bits = ...............: 0.0.31.255
------------------------------------------------
Network Address = .............: 192.168.160.0
Broadcast Address = ...........: 192.168.191.255
Usable IP Addresses = .........: 8190
First Usable IP Address = .....: 192.168.160.1
Last Usable IP Address = ......: 192.168.191.254


myhost> whatmask 192.168.0.13/255.255.255.0

------------------------------------------------
           TCP/IP NETWORK INFORMATION
------------------------------------------------
IP Entered = ..................: 192.168.0.13
CIDR = ........................: /24
Netmask = .....................: 255.255.255.0
Netmask (hex) = ...............: 0xffffff00
Wildcard Bits = ...............: 0.0.0.255
------------------------------------------------
Network Address = .............: 192.168.0.0
Broadcast Address = ...........: 192.168.0.255
Usable IP Addresses = .........: 254
First Usable IP Address = .....: 192.168.0.1
Last Usable IP Address = ......: 192.168.0.254


myhost> whatmask 192.168.1.126/0xffffffe0

------------------------------------------------
           TCP/IP NETWORK INFORMATION
------------------------------------------------
IP Entered = ..................: 192.168.1.126
CIDR = ........................: /27
Netmask = .....................: 255.255.255.224
Netmask (hex) = ...............: 0xffffffe0
Wildcard Bits = ...............: 0.0.0.31
------------------------------------------------
Network Address = .............: 192.168.1.96
Broadcast Address = ...........: 192.168.1.127
Usable IP Addresses = .........: 30
First Usable IP Address = .....: 192.168.1.97
Last Usable IP Address = ......: 192.168.1.126


myhost> whatmask 192.168.0.169/0.0.0.127

------------------------------------------------
           TCP/IP NETWORK INFORMATION
------------------------------------------------
IP Entered = ..................: 192.168.0.169
CIDR = ........................: /25
Netmask = .....................: 255.255.255.128
Netmask (hex) = ...............: 0xffffff80
Wildcard Bits = ...............: 0.0.0.127
------------------------------------------------
Network Address = .............: 192.168.0.128
Broadcast Address = ...........: 192.168.0.255
Usable IP Addresses = .........: 126
First Usable IP Address = .....: 192.168.0.129
Last Usable IP Address = ......: 192.168.0.254



COMPILATION NOTE: Some users have reported problems with pre-release versions
of gcc. If you get "illegal instruction" errors please try compiling with an
official full release of your compiler. You may also try disabling the
optimizer by removing "-O2" from the Makefile after running configure.



References
==========

O'Reilly and Associates:
TCP/IP Network Administration, 2nd Edition
By Craig Hunt
2nd Edition December 1997
1-56592-322-7
http://www.ora.com/

Cisco - IP Addressing and Subnetting for New Users
http://www.cisco.com/warp/public/701/3.html

More info on Wilcard bits and Cisco routers.
http://www.delmar.edu/Courses/ITSC1391/Sem3/6ACLs.htm

Then of course you can do a net search... I like http://www.google.com/


That's all, folks!
