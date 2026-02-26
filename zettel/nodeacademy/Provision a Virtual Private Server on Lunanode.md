Under _Virtual Machines_ on the left panel, we are going to _Create a new virtual machine_. At the moment, there is only one region to choose from, so we'll place our node in Ontario.

In the next step we'll first give it a hostname. If you plan to point a domain name at your server, then that would make for a good hostname. Otherwise, anything descriptive will do, such as _node_ or _lnd_.

The most difficult decision is what server we want to provision. The "memory optimized" servers tend to be a good choice, as a bitcoin and Lightning node consume disproportionately more RAM than CPU power. And for the CPU-intensive syncronization process we can choose to pay for acceleration later.

The **m.4** instance is probably a good minimum for a Lightning node. It is possible to run a node on an m.2 instance, but the node does not come with enough local storage to compile Bitcoin Core and LND.

Next, we are going to choose the operating system. **Ubuntu 24.04 64-bit** is what we are going to choose, but _Debian 12 64-bit_ is very similar and will work just as well. Another popular option for professionally run nodes is CentOS 8 64-bit. It's important we are choosing an 64-bit operating system, or else we might crash our node once it's channel.db reaches 2GB or more.

Finally we will select our SSH key or keys and provision our VPS by clicking on _Create virtual machine_.

[[Lunanode]]