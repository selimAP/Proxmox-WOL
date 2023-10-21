# Proxmox-WakeOnLan

## Step 1

To start your Proxmox server with Wake On LAN, you first have to access your Proxmox shell.

First, you need to install a tool with the following command:

`apt Install ethtool`

![image](https://github.com/selimAP/Proxmox-WOL/assets/91083639/911c1141-5cb3-40b6-9589-03ba21afb3bc)


After you have installed the tool, use the command `ip address` to see which port is your main adapter (Normally the main adapter is called eno1)

![image](https://github.com/selimAP/Proxmox-WOL/assets/91083639/b67220a4-7a4f-43ad-af20-c656e31bccfe)

You can also find your main port at the point network.

![image](https://github.com/selimAP/Proxmox-WOL/assets/91083639/f32bcb18-13e6-4ab8-a5b2-304dbe84a87b)

There must be a g at wake-on

![Screenshot from 2023-10-21 22-47-54_cleanup](https://github.com/selimAP/Proxmox-WOL/assets/91083639/2a22ddd4-3bca-4a66-8da9-fb62eb1c935b)

If there is a d in it it means that it is disabled, if it is disabled for you enter the following command 
(if your main port is different replace eno1):

`ethtool -s eno1 wol g`

Next you need to open the network configuration with the command:

`nano /etc/network/interfaces`

after opening it write this command `post-up /usr/sbin/ethtool -s enol wol g` under the command `iface enol inet manual` 

After you have written the command into the document save it with `ctrl x` and then with `Y`. with `enter` you come back to the main command line

![image](https://github.com/selimAP/Proxmox-WOL/assets/91083639/7f8348fc-dfc3-49f3-a00c-b9a0615fd760)

It may happen that Proxmox does not take the steps described above smoothly. If you encounter such an error, you can perform the following steps:

1. Go to the network settings in Proxmox again.

2.  Select the appropriate network element. Usually this is the "Linux Bridge".

3. Click "Edit" at the top to open the settings for the network element.

4. Check if the "Autostart" option is enabled. If this option is not enabled, set it to "enable".

5. Save the changes to ensure that the network element starts properly at system startup.

## How to use WakeOnLan

After all the steps WOL is set up now I show you how to use the whole thing 

First you have to install wakeonlan on your terminal with this command: sudo apt install wakeonlan after you have done it you can run it from your terminal. 

Now you need the mac-address from your server

to find out enter `ip address` again in the proxmox shell

As at the beginning you have to look what your main port is. In the 2nd place your mac address is shown between link/ether and brd. Copy out your mac address.

now you can send your magic packet to your server in the terminal with the command `wakeonlan your mac address` and it will start.

I hope it has helped you further.




























