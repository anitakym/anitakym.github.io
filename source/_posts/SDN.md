---
title: SDN
date: 2015-12-15 11:24:24
tags:
    - ComputerNetwork
    - 很久以前系列
---
> Let's define some terminology(术语), starting with terminal types(终端类型):

- VirtualBox console terminal: connects to OpenFlowTutorial. This is the one created when you started up the VM. You can't copy and paste from this tutorial page to the console terminal, so it's a bit of a pain.Minimize this NOW, if you haven't already done so. Once you've used it to set up networking, it won't be needed.

- SSH terminal: connects to OpenFlowTutorial. Created by using putty on Windows or SSH on OS X / Linux, as described in the previous section. Copy and paste should work on this terminal.

- xterm terminal: connects to a host in the virtual network. Created in the next section when you start up the virtual network. Will be labeled at the top with the name of the host.

- The OpenFlowTutorial VM includes a number of OpenFlow-specific and general networking utilities pre-installed. Please read the short descriptions:

- OpenFlow Controller: sits above the OpenFlow interface. The OpenFlow reference distribution includes a controller that acts as an Ethernet learning switch in combination with an OpenFlow switch. You'll run it and look at messages being sent. Then, in the next section, you'll write our own controller on top of NOX or Beacon (platforms for writing controller applications).

- OpenFlow Switch: sits below the OpenFlow interface. The OpenFlow reference distribution includes a user-space software switch. Open vSwitch is another software but kernel-based switch, while there is a number of hardware switches available from Broadcom (Stanford Indigo release), HP, NEC, and others.

- dpctl: command-line utility that sends quick OpenFlow messages, useful for viewing switch port and flow stats, plus manually inserting flow entries.

- Wireshark: general (non-OF-specific) graphical utility for viewing packets. The OpenFlow reference distribution includes a Wireshark dissector, which parses OpenFlow messages sent to the OpenFlow default port (6633) in a conveniently readable way.

- iperf: general command-line utility for testing the speed of a single TCP connection.

- Mininet: network emulation platform. Mininet creates a virtual OpenFlow network - controller, switches, hosts, and links - on a single real or virtual machine. More Mininet details can be found at the Mininet web page.

- cbench: utility for testing the flow setup rate of OpenFlow controllers.

#### mininet指路：
- https://github.com/mininet/mininet/
- http://mininet.org/walkthrough

#### mininet 的命令:
注意:
Cleanup —— If Mininet crashes for some reason, clean it up:
```
$ sudo mn -c
```