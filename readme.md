

#  Setting up a VNC Server on the Debian

![Raspberry Pi VNC Server](https://lh3.googleusercontent.com/MgYbfR6gHgGFcaEempgLqvpJAaXZ1-XbDUcS2PVvIxTIPnATuPeiER3JjGtb9Dev7w)


VNC is a special protocol that is designed to allow one device to control another remotely. This protocol works differently to the  Remote Desktop Protocol  that Windows uses.

Using VNC on your machine has a variety of uses. For example, you can use it to view your Pi’s desktop without having a monitor attached to it. This removes the need to use SSH as the only way of accessing your machine.

Setting up a VNC server on your machine is relatively straightforward and requires us to install and setup a single package called  `tightvncserver`.
## Installation

#### Installing the VNC Server Software
By following this guide, you will find out how easy it is to install and configure a VNC server on your machine.


**1.**  Before we install the VNC software to our machine, we need to make sure our operating system is up to date.

To update the packages running on our device, we need to run the following two commands.

```
apt update -y && apt upgrade -y
```
or
```
sudo apt update
sudo apt upgrade
```

**2.**  Once your machine has finished installing all of the updates, we can move on to installing the VNC Server.

As the  `tightvncserver`  package is available through the linux repository, all we need to do is run the following command.

```
sudo apt install tightvncserver
```
#### Configuring the VNC Server
Now that you have the VNC server installed to your machine, we can now learn how to configure it so that it is ready for connections.

**1.**  With the VNC server now installed to our machine, let us now proceed to configure it.

To start the configuration process, we need to run the command below.

```
vncserver :1
```

**2.**  You will now need to set up a password for when you connect to the machine remotely via a VNC client.

Make sure the password that you set is no longer than 8 characters long. Any password that is longer than 8 characters will be truncated (Meaning any letters after the eighth will be removed).

```
You will require a password to access your desktops.

Password:
```

As this password will give someone access to your machine’s desktop, make sure you set this to something secure.

**3.**  You will next be asked to re-enter the password again to verify it.

```
Verify:
```

**4.**  Next, you will be asked if you want to set up a separate view-only password.

A view-only password means that a user will be able to view the desktop using VNC but not interact with it.

For our tutorial, we will be skipping this step by typing in  n  and pressing the  ENTER  key.

```
Would you like to enter a view-only password (y/n)?
```

**5.**  Your VNC server should now be up and running on your machine.

However, whenever you restart your machine, you will need to restart the software by rerunning the following command.

```
vncserver :1
```

If you want to have the software startup automatically at bootup, then simply follow the next couple of steps. Otherwise, we are ready to set up the client-side of things.

####  Starting the VNC Server at Startup

Once we have verified that the VNC service is now functioning, we can tell it to start at boot. We have to edit rc.local located at `/etc`

**1.**  Edit file with text editor. In this step we use nano
```
nano /etc/rc.local
```

**2.** Insert this script to rc.local

Copy this script before `exit 0`
```
_IP=$(hostname -I) || true
if [ "$_IP" ]; then
  printf "My IP address is %s\n" "$_IP"
fi
su - root -c '/usr/bin/tightvncserver :1 -geometry 800x550 -depth 24'
```
As this script we use resolution `800x550` and user `root`

#### Setting up a VNC client on your PC
**1.**  Input ip address your machine linux to VNC client.
**2.**  Connect and input data with your data from when you setup.
![realvnc connect screen](https://bit.ly/2WK2R4m)  
## Source
[pimylifeup.com](https://pimylifeup.com/raspberry-pi-vnc-server/)