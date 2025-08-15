# HP mt43 Mobile Thin Client
An EFI I made for fun to see if I could do an AMD build on this 150 euro laptop. All the basics work but there are is a bug in the trackpad driver where it sometimes just freezes the cursor on boot. This happens very rarely and should be fixable. Either by debugging the current driver or trying some other driver for it.

A lot of hardware in this laptop will not work on macOS at all so it's disabled in the BIOS. You can use the BIOS configuration file from the repo to apply all BIOS settings in one go. It might be possible to get the mobile modem/simcard to work in macOS but I have no data simcards to test this with so I have disabled it in the BIOS. This should save more power than just leaving it enabled and maybe toggle power management. Battery life is decent and could be further improved by tweaking power management, but I do not know if there are such options for AMD on macOS. Graphics performance is good and more than good enough for browsing and consuming media.

By default these laptops come pretty bare bones. I picked up 3 of these for 150 euro a piece configured with 8gb and an msata ssd. I got the standard 1080p touch panel. There are other configurations available (see service manual in the stuff folder) with different screens but I don't see that being an issue for this EFI. I have upgraded the memory to 16gb without a problem and it also booted with a 16+8gb stick but I couldn't test 2x 16gb stick as I only got the one but I think it should work with 32gb too. I also upgraded the msata drive with nvme which further improves performance. Don't expect M4 performance though. Running older macOS verisons on it will be a snappier experience. Some tweaks might help speed it on all macOS versions, like disabling indexing/search for all disks, not using too many iServices and so on.

The touch panel works in macOS too, even gestures work on the touch 
screen. Like a 3 finger swipe to move to a new workspace. Pretty cool and 
could also be improved with driver tweaks. some models come with an 
Realtek wifi card, 2 out of 3 came with Intel for me. By default most 
Intel cards should work and boot times could be improved by recompiling 
the wifi and bluetooth drivers to only include the firmware that matches 
your Intel card. You will also need to downlaod the Heliport app to 
connect to wireless networks. I suggest downloading the 2.0 version. For 
Sonoma and older replace itlwm.kext with AirportItlwm and wireless will 
work as if it's part of macOS.

This EFI is provided as is and currently has only been tested with the latest public release of macOS being Sequoia. It is capable to run macOS 26 too but I will not get into that as long as it's in beta. I'm open for pull requests and improvements and regular issues too. Just don't expect step-by-step guides or support.

Another thing is that when using a T2 SMBIOS updates do not show unless RestrictEvents is used to force showing all updates, this shows updates but delta updates will error when out and macOS will then download the full installer which will install and update just fine. Just a bit of a waste of time and bandwith. If I understand correctly this is a side effect of using a T2 SMBIOS. It might be possible to use a different SMBIOS and have updates showing up and delta updates installing fine without the need for RestrictEvents.

I think the performance is on par with a 2018 Mac mini if you've upgraded to a fast nvme drive and 16GB of memory. Sleep works and clamshell mode works too.

# Quick setup
- Create installer and copy the EFI folder to its root
- Download HPSetup.txt form the stuff folder and copy it to the root of the EFI
- Use GenSMBIOS to populate the platform info section of the config file, do not use iCloud without changing these!
- Reset BIOS defaults and then select reproducible setup and ON the next screen select load from disk, it should find the config and apply it, save and quit
- Boot into the installer and install macOS, copy the EFI to the internal disk and thats it!

I'll make this README better in the future, for now I quickly wanted to share what I have for people who already know a bit about making a hackintosh.

To do list:
- Find bug in touchpad driver (need debug version for logs) and try other drivers, also need to find a way to reproduce this issue
- HiDPI tweaks for more resolution options, 1080p on a 14" is pretty small. In Linux I use 125% scaling on it
- Power management, already enabled it for the pci devices that support it and don't break sleep
- Try/use different SMBIOS with different max macOS version to stop upgrade prompts for staying on an older version
- Find a good solution for the T2 SMBIOS issue where delta updates do not work without using RestrictEvents
- Try out non-T2 SMBIOS to test delta updates and such too
- Ventura with Apple/Broadcom wifi/bluetooth with non T2 SMBIOS that does not nag about upgrading but ota updates working for all the iServices
- Make this README less of a mess
