# Distributed Systems
A distributed system is a collection of processors that do not share memory or
a clock. Instead, each node has its own local memory. The nodes communicate
with one another through various networks, such as high-speed buses.

## Advantages of Distributed Systems
A distributed system is a collection of loosely coupled nodes interconnected by
a communication network. From the point of view of a specific node in a distributed
system, the rest of the nodes and their respective resources are remote, whereas
its own resources are local.

Nodes can exist in a client-server configuration, a peer-to-peer configuration,
or a hybrid of these. In the common client-server configuration, one node at one
site, the server, has a resource that another node, the client (or user), would 
like to use. In a peer-to-peer configuration,  there are no servers or clients.
Instead, the nodes share equal responsibilities and can act as both clients and
servers.

### Resource Sharing
If a number of different sites are connected to one another, then a user at one
site may be able to use the resources available at another. For example, a user
at site A may query a database located at site B. Much like a user at site B may
access a file that resides at site A.

### Computation Speedup
If a particular computation can be partitioned into sub-computations that can 
run concurrently, then a distributed system allows us to distribute the sub-computations
among the various sites. The sub-computations can be run concurrently and thus 
provide computation speedup.

In addition, if a particular site is currently overloaded with requests, some
of them can be moved or re-routed to other, more lighly loaded sites. This movement
of jobs is called load balancing and is common among distributed systems and other
services provided on the internet.

### Reliability
If one site fails in a distributed system, the remaining sites can continue operating,
giving the system better reliability. If the system is composed of multiple large
autonomous installations, the failure of one of them should not affect the rest. 
If, however, the system is composed of diversified machines, each of which is
responsible for some crucial system function, then a single failure may halt the
operation of the whole system.

The failure of a node or site must be detected by the system, and appropriate
action may be needed to recover from the failure. The system must no longer use
the services of that site. In addition, if the function of the failed site can 
be taken over by another site, the system must ensure that the transfer of function
occurs correctly. Finally, when the failed site recovers or is repaired, mechanisms
must be available to integrate it back into the system smoothly.

## Network Structure
There are two types of networks: local-area networks (LAN) and wide-area networks 
(WAN). The main difference between the two is the way in which they are geographically
distributed. Local-area networks are composed of hosts distributed over small areas,
whereas wide-area networks are composed of systems distributed over a large arrea.

### Local-Area Networks
LANs are usually designed to cover a small geographical area, and they are generally
used in an office or home environment. All the sites in such systems are close
to one another, so the communication links tend to have higher speed and lower
error rate than their counterparts in wide-area networks.

A typical LAN may consist of a number of different computers, various shared
peripheral devices, and one or more routers that provide access to other networks.
Ethernet and WiFi are commonly used to construct LANs. Wireless access points connect
devices to the LAN wirelessly, and they may or may not be routers themselves.

Ethernet networks use coaxial, twisted pair, and/or fiber optic cables to send
signals. An Ethernet network has no central controller, because it is a multiaccess
bus, so new hosts can be added easily into the network. The Ethernet protocol is
defined by the IEEE 802.3 standard. Typical Ethernet speeds using common twisted-pair
cabling can vary from 10Mbps to over 10Gbps, with other types of cabling reaching
speeds of 100Gbps.

WiFi is now ubiquitous and either supplements traditional Ethernet networks or
exist by itself. Specifically, WiFi allows us to construct a network without
using physical cables. Each host has a wireless transmitter and receiver that
it uses to participate in the network. WiFi is defined by the IEEE 802.11 standard.
WiFi speeds can vary from 11Mbps to over 400Mbps.

### Wide-Area Networks
Sites in WAN are physically distributed over a large geographical area. Typical
links are telephone lines, leased lines, optical cable, microwave links, radio
waves, and satellite channels. These communication links are controlled by routers
that are responisble for directing traffic to other routers and networks and transferring
information among the various sites. 

The first WAN to be designed and developed was the ARPANET. The ARPANET has grown 
from a four-site experimental network to a worldwide network of networks, the Internet, 
comprising millions of computer systems. There are, of course, other WANs besides 
the Internet. A company may, for example, create its own private WAN for increased 
security, performance, or reliability.

WANs are generally slower than LANs, although backbone WAN connections that link
major cities may have very fast transfer rates through fiber optic cables.

Frequently, WANs and LANs interconnect, and it is difficult to tell where one
ends and the other start. Consider the cellular phone data network. Cell phones
are used for both voice and data communications. Cell phones in a given area
connect via radio waves to a cell tower that contains receivers and transmitters.
This part of the network is similar to a LAN except that the cell phones do not
communicate with each other. Rather, the towers are connected to other towers
and to hubs that connect the tower communications to land lines or other communication
media and route the packets towards their destination. This part of the network
is more WAN-like.

## Communication Structure
### Naming and Name Resolution
The first issue in network communication involves the naming of the systems in
the network. For a process at site A to exchange information with a process at
site B, each must be able to specify the other. Within a computer system, each
process has a process identifier, and messages may be addressed with the process
identifier. Because networked systems share no memory, however, a host within
the system initially has no knowledge about the processes on other hosts.

To solve this problem, processes on remote systems are generally identified by
the pair <host name, identifier>, where host name is a name unique within the
network and identifier is a process idntifier or other unique number within that
host. A host name is usually an alphanumeric identifier, rather than a number,
to make it easier for users to specify. For instance, site A might have hosts 
named "program", "student", "faculty", and "cs". The host name "program" is certianly
easier to remember than the numeric host address 128.148.31.100.

Names are convenient for humans to use, but computers prefer numbers for speed
and simplicity. For this reason, there must be a mechanism to resolve the host
name into a host-id that describes the destination system to the networking 
hardware. The internet uses a domain-name system (DNS) for host-name resolution.

DNS specifies the naming structure of the hosts, as well as name-to-address resolution.
Hosts on the Internet are logically addressed with multipart names known as IP 
addresses. The parts of the IP address progress form most specific to the most
general, with periods separating the fields. For instance, _eric.cs.yale.edu_ refers
to the host _eric_ in the Department of Computer Science at Yale University within
the top-level domain _edu_. Each component has a name server - simply a process
on a system - that accepts a name and returns the address of the name server responsible
for that name.

### Routing stategies
- **Fixed routing**: A path from A to B is specified in advance; The path then
only changes if a hardware failure disables it. Since the shortest path is usually 
chosen, communication costs are minimized. Fixed routing cannot adapt to load changes
however. Fixed routing ensures that messages will be delivered in the order in 
which they were sent.
- **Virtual routing**: A path from A to B is fixed for the duration of one session. 
Different sessions involving messages from A to B may have different paths. This 
is a partial remedy to adapting to load changes. Virtual routing ensures that 
messages will be delivered in the order in which they were sent.
- **Dynamic routing**: The path used to send a message from site A to site B is 
chosen only when a message is sent. Usually a site sends a message to another 
site on the link least used at that particular time. This method adapts to load 
changes by avoiding routing messages on heavily used path. One downside to dynamic
routing is that messages may arrive out of order. This problem can be remedied 
by appending a sequence number to each message. Dynamic routing is also the most
complex of the three to setup.

### Connection stategies
- **Circuit switching**: A permanent physical link is established for the duration 
of the communication (i.e., telephone system).
- **Message switching**: A temporary link is established for the duration of one 
message transfer (i.e., post-office mailing system).
- **Packet switching**: Messages of variable length are divided into fixed-length 
packets which are sent to the destination. Each packet may take a different path 
through the network. The packets must be reassembled into messages as they arrive.

Circuit switching requires setup time, but incurs less overhead for shipping each 
message. Circuit switching may waste network bandwidth however. Message and packet 
switching require less setup time, but incur more overhead per message.

## Network and Distributed Operating Systems
### Network Operating System
A network operating system provides an environment in which users can access remote
resources by either logging in to the appropriate remote machine or transferring
data form the remote machine to their own machines.

There are two major functions of a network operating system:
1. **Remote login**: Users can remotely login to a machine. This can be done via the
`ssh` facility. for example, suppose that a user at Westminster College wishes
to compute on `kristen.cs.yale.edu`, a computer located at Yale University. To
do so, the user must have a valid account on that machine. To log in remotely, 
the user can issue the command `ssh kristen.cs.yale.edu`.
2. **Remote file transfer**: A way for users to transfer files from one machine
to another remotely. The Internet provides a mechanism for such a transfer with
the file transfer protocol (FTP) and the more private secure file transfer protocol
(SFTP).

### Distributed Operating System
In a distributed operating system, users access remote resources in the same way
they access local resources. Data and process migration from one site to another
is under the control of the distributed operating system.

#### Data Migration
The system can transfer data by one of two basic methods. The first approach to
data migration is ot transfer the entire file to site A. From that point on, 
all access to the file is local. When the user no longer needs access to the file, 
a copy of the file is sent back to site B.

#### Computation Migration
In some circumstances, we may want to transfer the computation, rather than the 
data, across the system; this process is called computation migation. For example,
consider a job that needs to access various large files that reside at different
sites, to obtain a summary of those files. It would be more efficient to access
the files at the sites where they reside and return the desired results to the
site that initated the computation. This can be achieved via remote procedure 
calls (RPCs) or via a messaging system.

#### Process Migration
When a process is submitted for execution, it is not always executed at the site
at which it is initiated. The entire process, or parts of it, may be executed at
different sites. This scheme may be used for several reasons:
- **Load balancing**: The processes (or subprocesses) may be distributed across
the sites to even the workload.
- **Computation speedup**: If a single process can be divided into a number of 
subprocesses that can run concurrently on different sites or nodes, then the total
process turnaround time can be reduced.
- **Hardware preference**: The process may have characteristics that make it more 
suitable for execution on some specialized processor (such as matrix inversion 
on a GPU) than on a microprocessor.
- **Software preference**: Th eprocess may require software that is availableat 
only a particular site, and either the software cannot be moved, or it is less 
expensive to move the process.
- **Data access**: Just as in computation migration, if the data being used in 
the computation are numerous, it may be more efficient to have a process run 
remotely (say, on a server that hosts a large database) than to transfer all the 
data and run the process locally.

## Design Issues in Distributed Systems
The designers of distributed systems must take a number of design challenges into
account. The system should be robust so that it can withstand failures. The system
should also be transparent to users in terms of both file location and user mobility.
Finally, the system should be scalable to allow the addition of more computation
power, more storage, more users.

- **Transparency**: The distributed system should appear as a conventional, 
centralized system to the user.
- **Fault tolerance**: The distributed system should continue to function in
the face of failure.
- **Scalability**: As demands increase, the system should easily accept
the addition of new resources to accommodate the increased demand.
