# Alfa
 Linux Alfa AWUS036ACH Driver

Install ALFA AWUS036ACH driver on Mint
By elektron
 07/04/2019

Like many others, I bought myself an Alfa AWUS036ACH, only to find its drivers are not set up by default on the latest version of Kali (despite many if its more recent reviews pointing out this fact). I found that there are few guides on how to get this sexy dual-band interface going, so I made a quick shell script to do everything in one shot. A few things to note before we begin:

# You need an internet connection for this to work
This script works great on a fresh installation of the latest version of Kali Linux (2018.1). I tried running the script on a live boot, but the kernel yelled at me when I was modprobe-ing. If you want this to work with live boot, you will probably need to set up persistence or a custom image. Neither of those options are that difficult.

Some of the commands towards the end are not necessary for installation, but I used them while I was figuring out how to set everything up, so I left them in there in case anything breaks.

If you are anything like me, you may have a few broken drivers polluting your /usr/src folder from previous failed attempts. Delete them before attempting.
Once script has run, I recommend you add the following lines to your *NetworkManager.conf*
```
[keyfile]
unmanaged-devices=interface-name:wlan1;interface-name:wlan2
```
This prevents NetworkManager from trying to resolve the interface using its own stuff when you reboot again (real men keep NetworkManager disabled anyway, but whatever). If your PC already has a wlan0 assigned by default (i.e. is a laptop with built-in wifi),  the keyfile above should work fine. Otherwise, just add interface-name:wlan0; before interface-name:wlan1; The reason I also disabled a second, nonexistent wlan2 at the end is because sometimes, if I unplug the interface and replug it into a different USB port, it will be assigned one number up. This measure adds one get-out-of-NetworkManager-free card to your hand, increasing your chance to pass go and collect that sweet $200.

- Once you have gotten the interface set up, I would recommend using ifconfig to put it into monitor mode, instead of airmon-ng. I’ve found that airmon-ng tends to have issues with manually installed drivers on occasion. In case you don’t know, here is how its done (assuming your Alfa is assigned wlan1):

```
ifconfig wlan1 down
iwconfig wlan1 mode monitor
ifconfig wlan1 up
```
Anyway, here is the script in question. As you probably already know, you can copy it to a text file called coolfilename.sh, set it to executable, and give that baby a run from the terminal. Or you could always just manually run the following commands one at a time.
