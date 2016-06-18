Title: Routing subnets behind a Asus RT-N56U with Padavan firmware
Date: 2016-05-31 8:30
Category: Networking
Tags: asus, padavan, networking, cisco

Sometimes, I like to play with routing (no really) and for me, it is often
desirable to route subnets to subrouters (like a Cisco box) behind a WLAN
router that does NAT. In my case, the WLAN router is a
[Asus RT-N56U](https://www.asus.com/us/Networking/RTN56U/) running
[Padavan](https://bitbucket.org/padavan/rt-n56u). Unlike Tomato, which provides
NAT for all subnets in internal interfaces, Padavan only provides NAT for
`192.168.1.0/24` (or the subnet you set for your LAN). This can be a good thing
if you want to route public IP addresses in your LAN, but this isn't in the
scope of the article.

Getting back to routing internal subnets, the magic command you need is listed
below:

	iptables -t nat -A POSTROUTING -s 10.20.30.0/24 -o eth3 -j MASQUERADE

Replace `10.20.30.0/24` with the subnet ID and mask you will use.

But to do that, you will have to log in to your router configuration page
(often `192.168.1.1`). Once you are there, the next step is to provide NAT for
the subnets. To do this, go to **Advanced Settings** > **Administration** >
**Console** and type in the "magic" command we have (with replacing the values
with the ones you want) and press **Refresh**. Repeat the steps for all subnets
you want.

To make the changes permanent, you will need to go to **Advanced Settings** >
**Customization** > **Scripts**, click on **Run After WAN Up/Down Events**
and type in a list of your "magic" commands for all the subnets you want. This
will ensure that NAT will be configured for the subnets you want when the
interface goes up, but not if `iptables` is reloaded. To fix this, you need to
copy the "magic" commands you typed in, and paste it into the
**Run After Firewall Rules Restarted** section. Finally, you click **Apply**
and the changes will be permanent through reboots and reloads.

**Update:** At least on my RT-N56U, the changes don't persist through reboots.
You will need to go back to **Advanced Settings** > **Administration** >
**Console** and run this command to make the changes permanent.:

	mtd_storage.sh save

This command applies to any changes made to the scripts in the router, not just
the ones I mentioned above.

But we also need to do one last thing: add routes. To do this, go to **Advanced
Settings** > **LAN** > **Route** and from here, you can add routes. The
**Network or Host IP** section is the subnet ID you used in the "magic"
commands earlier, the **Netmask** section holds a IP form of the subnet length
(e.g. `/24` will be `255.255.255.0`, `/16` will be `255.255.0.0`, etc.), and
the **Gateway** section holds the static IP address the subrouter uses. The
**Metric** section is usually used for route precedence, but in a simple
network, it can be anything. The **Interface** section should be set to **LAN**
if you are assigning subnets inside your home.

Now, you will need to configure your subrouters. This will vary from router to
router, so I won't be covering this, but a simple Google search can help you
find information for your router. A few things to keep in mind is:

 * You do not need NAT on the subrouter
 * On the subrouter, assign an IP in the subnet you delegated to the LAN-facing
   interface, and the static IP address to the WAN facing interface (which
   connects to the network the RT-N56U is in) with the IP address you put in
   the **Route** section
 * If the subrouter is PC-based (e.g. Linux, FreeBSD, etc), enable forwarding
   in the operating system

I hope you enjoy this article and find my solution useful.
