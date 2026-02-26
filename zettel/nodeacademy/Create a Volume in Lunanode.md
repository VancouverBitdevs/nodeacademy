First, we will power off our node. We are going to do that through the Lunanode dashboard. Under _Virtual Machines_ we will select _Manage_, then _Shut Down_. We can verify that it is shut down by its status changing to _Offline_.

On the left of the screen, we find the option _Volumes_. We select our region (Toronto), give it a name (for example `bitcoin`) and decide on a size. For a Bitcoin node that is used as a backend to our node, 50GB is a good size for a small node. That's about 24 weeks worth of blocks. For a more performant node, 80GB or even 120GB might be a decent choice too. The entire blockchain takes up about 600GB today, and growing by about 2GB per week, so running a full archival node on a VPS might not be economical, as Lunanode will charge us US$36 per month for a 600GB large SSD.

We will leave the volume empty (_Source_) and create it.

The volume should appear instantly in our volume list. We will click on _Manage_ and then _Attach to VM_ where we select our node under _Virtual Machine_ and _virtio_ as a driver. This won't work if our server isn't shut down. Only once our volume reads _Attached to_ our node we can go back into _Virtual Machines_, then _Manage_, then _Start Up_ our node. Once we can see _Status_ changed to _Online_ we can log back into our node with SSH.

[[Connect to your node]]
