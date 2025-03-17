# Convert_Five_Ninjas_Slice_media_player_into_a_NAS

the Five Ninjas Slice media player is a device that was funded years ago on Kickstarter and I got mine somewhere in 2016. This device had a custom made PCB mainboard holding a Raspberry Pi Compute Module 1, ran a customized XBMC operating system and was able to hold either a 2.5 HDD or SSD inside the aluminum chassis. It was a great device based on Raspberry Pi and had the flexibility to change OS, wich AppleTV and Android Boxes didn't offered.

https://www.kickstarter.com/projects/fiveninjas/slice-a-media-player-and-more/

It served years in our living room and as technology advanced, so did our TV and the Slice media player eventually found itself sidelined since it became impractial to use since everything it offered, was build-in in our smart TV that ran on Android.

After some time I start wondering if there isn't a way to use this fine piece of technology in a different way and at the same time I was thinking about getting myself a NAS and that got me to the idea of converting this media player into just that!
So I started looking in what would be necessary to make this happen and found out that after a lot of tinkering and experminenting that it can be done! 

What is needed : 

- Slice including its power adapter
- Raspberry Pi Compute Module 3 (preferably already installed)
- Micro-USB cable
- UTP cable (type doesn’t matter, the Slice is limited by its 10/100 Ethernet port)
- Raspberry Pi Imager (I prefer version 1.6.1)
- HDD or SSD (installed)


Below you will find the links to get started for this fun little project and convert your Slice media player into a portable NAS. All needed software are linked to their official download locations except the files you’ll be needing later to make the Slice able to connect to your wired network, those are shared through this repository (link included for your convenience).

- https://downloads.raspberrypi.com/raspios_oldstable_lite_arm64/images/raspios_oldstable_lite_arm64-2023-10-10/2023-05-03-raspios-bullseye-arm64-lite.img.xz
- https://downloads.raspberrypi.org/imager/imager_1.6.1.exe
- https://github.com/raspberrypi/usbboot/raw/master/win32/rpiboot_setup.exe
- https://github.com/Runaque/Convert_Five_Ninjas_Slice_media_player_into_a_NAS/blob/main/Additional%20Files.zip

Install the Raspberry Pi Imager as well RPIboot! RPIboot can take a little while installing the right drivers! Don’t forget to unzip the files I provide, you’ll be needing them later!


Start preparing the Slice its operating system :

- Connect the Slice to your system with the micro-USB cable, but DON’T connect it to the power adapter just yet!!!
- When your Slice shows up as a storage device, safely eject the drive from your computer WITHOUT disconnecting the micro-USB cable!
- Now we will plug in the power adapter in the power socket as well as in the Slice player.
- Run RPIboot, you’ll see a CMD like window with some action going on, it’ll close out of itself.
- Run Raspberry Pi Imager and click “yes” when Windows asks for it! When the Imager is opened it will ask if you want to upgrade to a newer version, click “no”.
- Under Operating system we are going to click to select the Raspberry Pi build you have downloaded from the link above. You will be prompted with a selection screen where you will scroll down and select “Use custom” and select the RPi build you have downloaded earlier and then confirm.
- Now we are going to select the destination to where you want to install this OS, click under storage on “Choose storage”. If you only have your Slice connected and no other drives, then it will be easy to find, but usually It will be the drive that is around 4 GB.
- Now we are going to configure the SSH so you can access it through the Windows Command Prompt (or PowerShell). Press SHIFT Ctrl X at one and you’ll be provided with “Advanced Options”.
- Check boxes “Set hostname” and “Enable SSH”!
- Leave the hostname as it is, which should be just “pi”.
- At “Enable SSH” we are going to add a password, take an easy one to remember, for example “12345”, if not done, the generic password will be “raspberry”, but better set one yourself! Don’t worry about it being too easy, it’ll change later on when installing OpenMediaVault! When done, click “Save”.
- Now we are at the point where we are going to write the RPi OS to the Slice, click “Write” and let it do its work, after it is done, it will verify the build on the Slice and will prompt you when ready! Click to confirm and close the Imager and safely!
- Don’t disconnect anything just yet!


Just hold yourself, we aren’t quite there yet! Now we are going to make sure the Slice can be working with your network! The Slice is built with a custom PCB designed by Five Ninjas with a Raspberry Pi Compute Module 1 on it, but the OS we just installed doesn’t know how to communicate with everything yet. We are now going to merge the (additional) files into the Raspberry Pi Bullseye-lite OS so it can work on the network and the can communicate with the Compute Module 3 (pin layout). I left the files in the folder they eventually have to be copied in!

- Unplug only the power adapter!
- Plug the power adapter back in and it will show as a “boot” drive.
- Open this drive so you see a folder called “overlays” and a bunch of other files.
- We are going to copy the file called “Slice.dtbo” into the “overlays” folder.
- The remaining files you’ll be dropping into the “boot” section.
- Safely disconnect the drive, unplug micro-USB and power adapter.

At this point the Slice is ready to be connected to the network by an ethernet cable (UTP). I advice to give the device in your Router a static IP address so it will be easier to SSH into the device and flash OpenMediaVault onto it. For this you need your "hostname" and the "password" you've set before when you flashed Raspberry Pi Bullseye to the Slice.

From here on you can follow the steps in the manual you find with the link below.

https://pimylifeup.com/raspberry-pi-openmediavault/
