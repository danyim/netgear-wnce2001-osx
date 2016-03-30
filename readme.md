# Netgear WNCE2001 Reimaging for OSX

Recently my Netgear WNCE2001 that I used to connect my home theater receiver to the internet suddenly stopped working. It wasn't responding to pings or anything. The biggest indicator was the blinking green "Power" LED, which I've found to mean that the firmware has been corrupted. Great.

There's a [great thread](https://community.netgear.com/t5/WiFi-Range-Extenders-Repeaters/WNCE2001-power-led-blinking-green-and-no-connection/td-p/383081/page/2) about `tftp`ing into the unit and upgrading its firmware, but the instructions are for Windows users.

After combing through DD-WRT's [TFTP flashing method for OSX](https://www.dd-wrt.com/wiki/index.php/TFTP_flash#Mac_OS_X), I found the following to work for OSX.

1. Connect directly to the WNCE2001
2. In System Preferences > Network, set the network adapter to configure IPv4 **Manually** with 192.168.1.1 as your IP and the subnet mask as-is
3. Download this repo and navigate to it
4. Open up your terminal, cd into the folder where you downloaded the repo
5. Type in `tftp` to begin the TFTP prompt
6. Paste the below
        connect 192.168.1.251
        binary
        rexmt 1
        timeout 100
        trace
        put WNCE2001-V1.0.0.26NA.img
7. You're done!

Note: All WNCE2001s identify as 192.168.1.251, so that should be static. The IP address you assign yourself (192.168.1.1) doesn't really matter. If 192.168.1.251 doesn't work, I suggest using a tool like Wireshark to see the IP the device identifies as.