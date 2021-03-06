nf-HiShape
==========

nf-HiShape is a kernel module for traffic shaping according to the source IP 
address. It limits the bandwidth usage of user-defined IP-address ranges and was implemented by the constraint of high-performance operation as well as easy usage.

The package includes the module itself and a user-land tool for its configuration.

The main purpose for development was the high performance bandwidth throttling for mitigating DDoS attacks.

Detailed Information
--------------------

nf-HiShape registers a definable netfilter hook (e.g. for forwarded packets).
For every packet that should be forwarded this hook is called. nf-HiShape
decides if the packet should be dropped, queued or accepted based on the network
input device and the entitled bandwith previously assigned to this IP address of
the packet. The device can be specified by the module parameter 'device' or
later using the userland tool. If no device is given, packets of all devices
will be filtered. 

Prerequisites
-------------

* Prepared linux kernel headers
     

Compilation & Installation
--------------------------

inside the source folder, type

    :~# make
    :~# sudo make install
    :~# sudo mknod /dev/nf-hishape c 100 0

Module load
-----------

    :~# modprobe nf-hishape <key=value ...>


Module unload
-------------

    :~# rmmod nf-hishape


Module parameters
-----------------

    device          the network device at which the filtering should be processed
                    (e.g. eth0)
                    if none is given, the filtering is done on all devices
                  
    hook            position in the netfilter stack where the shaping should be
                    processed
                    possible values are:
                       pre    for pre-routing
                       in     for input
                       for    for forward
                       out    for output
                       post   for post-routing
                    
    priority        priority of the whole packet filter module
                    small number indicates high priority


Userland tool
-------------

    Usage: ./nf-hishape [OPTION...]
    
     Options:
     
      -L, --list               List the ranges
      -F, --flush              Flush the ranges
      -S, --set=FILE           Load ranges from FILE
      -i, --interface=DEVICE   Set interface to DEVICE
      -a, --any_device         Unset interface
      -p, --print_interface    Print interface
      -f, --from               Start ip address for a new range (integer or dotted notation)
      -t, --to                 End ip address for a new range (integer or dotted notation)
      -l, --limit              Limit of the new range in kbyte/s
      -h, --help               Print this message and exit


Copyright/ License/ Credits
---------------------------

Copyright 2007-2008 Deutsches Forschungszentrum fuer Kuenstliche Intelligenz or its licensors, as applicable.  
Copyright 2009-2015 Markus Goldstein

You may not use this file except under the terms of the accompanying license.

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

This is free software. Licensed under the [GNU GPL, Version 3.0](LICENSE).  
There is NO WARRANTY, to the extent permitted by law.

![http://madm.dfki.de/lib/tpl/dfki/images/logo.jpg](http://madm.dfki.de/lib/tpl/dfki/images/logo.jpg)  
