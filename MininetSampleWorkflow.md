<!-- %META:TOPICINFO{author="BobLantz" date="1305074654" format="1.1" reprev="1.1" version="1.1"}% -->
<!-- %META:TOPICPARENT{name="MininetViewTemplate"}% -->
<!-- Use our custom page layout:
* Set VIEW_TEMPLATE = [MininetView](MininetView)
-->


Sample Workflow
================

Mininet is designed you to quickly [create](#Creating_a_Network), [interact with](#Interacting_with_a_Network), [customize](#Customizing_a_Network) and [share](#Sharing_a_Network) a software defined network prototype, and provides a smooth path to [running on hardware](#Running_on_Hardware). This page illustrates the basic Mininet workflow, and many additional details are available in the Mininet [walkthrough](MininetWalkthrough), the !OpenFlow [tutorial](http://www.openflow.org/wk/index.php/OpenFlow_Tutorial), and Mininet [documentation](MininetDocumentation).


### Creating a Network

You can create a network with a single command. For example,

<code>mn --switch ovsk --controller nox --topo tree,depth</code>2,fanout=8 --test pingAll=

starts a network with a tree topology of depth 2 and fanout 8 (i.e. 9 switches connecting 64 hosts), using Open vSwitch switches under the control of NOX, and runs the pingAll test to check connectivity between every pair of nodes.


### Interacting with a Network

Mininet's CLI allows you to control and manage your entire virtual network from a single console. For example, the CLI command

<code>mininet&gt; h2 ping h3</code>

tells host <code>h2</code> to ping host <code>h3</code> 's IP address.


### Customizing a Network

Mininet's API allows you to create custom networks with a few lines of Python. For example, the following script

<verbatim>
from mininet.net import Mininet
from mininet.topolib import [TreeTopo](TreeTopo)
tree4 = [TreeTopo](TreeTopo)(depth=2,fanout=2)
net = Mininet(topo=tree4)
net.start()
h1, h4  = net.hosts[0], net.hosts[3]
print h1.('ping -c1 %s' % h4.IP())
net.stop()</verbatim>

creates a small network (4 hosts, 3 switches), and pings one host from another (in about 4 seconds with the current version.)

The Mininet distribution includes several text-based and graphical (see above) applications which we hope will be instructive and inspire you to create cool and useful apps for your own network designs.


### Sharing a Network

Mininet is distributed as a virtual machine (VM) image with all dependencies pre-installed, runnable on common virtual machine monitors such as VMware, Xen and !VirtualBox. This provides a convenient container for distribution; once a prototype has been developed, the VM image may be distributed to others to run, examine and modify. A complete, compressed Mininet VM is about 800 MB. (Mininet can also be installed natively on Linux distributions that ship with <code>CONFIG_NET_NS</code> enabled, such as Ubuntu 10.04+, without replacing the kernel.) If you are reading a great SIGCOMM (or other) paper about a Software-Defined Network, wouldn't you like to be able to click, download and run a living, breathing example of the system? If so, consider developing a Mininet version of your own system that you can share with others. (Alternately, if you fear others reproducing - and possibly contradicting - your published results, an easily shared and downloaded version of your system may not be desirable!)


### Running on Hardware

Once a design works on Mininet, it can be deployed on hardware for real-world use, testing and measurement.

To successfully port to hardware on the first try, every Mininet-emulated component must act in the same way as its corresponding physical one. The virtual topology should match the physical one; virtual Ethernet pairs must be replaced by link-level Ethernet connectivity. Hosts emulated as processes should be replaced by hosts with their own OS image. In addition, each emulated !OpenFlow switch should be replaced by a physical one configured to point to the controller. However, the controller does not need to change. When Mininet is running, the controller ``sees" a physical network of switches, made possible by an interface with well-defined state semantics.