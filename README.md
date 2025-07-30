# Hackintosh for Thinkpad X1 Carbon 20HQ

This EFI works on the 20HQ variant of the X1 Carbon just fine and on the LATEST version of MacOS (as of writting this, Sequoia). 
I don't guarentee that it works on older versions, mostly because I lazily threw this together from multiple resources. 

It is heavily recommended that you read through the [Dortania Hackintosh](https://dortania.github.io/OpenCore-Install-Guide) guide before you use this EFI willy nilly. You might have to fix a few things.

# NOTES

There are a few things that I have done in this EFI to allow me to install Sequoia on my Thinkpad. For one, it was an upgrade to the latest version, meaning that I had to install the whole installer. Secondly, because of this, my EFI relies on OCLP (OpenCore Legacy Patcher) to get my Wifi working without using regular Itlwm, I'm currently still waiting for the official AirportItlwm, but on the bright side, using either regular Itlwm or this current method allows you to use iServices.

This will assume that you have the full installer, if you don't you COULD install the previous version, Sonoma, so you can have wifi in the installer, but you'll have to disable the following kexts:
- IO80211FamilyLegacy.kext
- IOSkywalkFamily.kext
- AMFIPass.kext

And then you'll have to replace the existing AirportItlwm with the Sonoma version (it uses the Ventura version), I would keep a note on the order if you plan to upgrade to Sequoia.

Another thing is that I have the YogaSMC kext installed as well, it just allows for fan control and stuff, so if you want, you can install the [application](https://github.com/zhen-zen/YogaSMC) for it.

# Installation

First of all, get your own SMBIOS, UUID, and ROM, follow the [dortania guide](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/kaby-lake.html#platforminfo) on this 

Installing Sonoma, if you followed the NOTES above, should be as simple as plug and play.

However, if you plan to install Sequoia, you can upgrade via the MacOS updates, to fix the wifi you'll have to re-enable all the kexts, and reinstall the Ventura AirportItlwm (ORDER IS IMPORTANT!). Next, you'll then have to uncomment the spoof, which is under Device Properties (it'll have a # infront of the name of the PCI name), also you'll need to get OCLP app ready to run aswell, my EFI should already have SIP enabled, but make sure the csr-active-config in the NVRAM is `03080000`.

Once you are in, you will need to run the OCLP patcher, select `Post-Install Root Patch`, and then `Start Root Patching`, once you are done reboot. After you reboot, wifi won't work, you'll need to recomment the spoof, and then reboot once again. After doing that, it SHOULD work.

# Afterword

I've been daily driving this Hackintosh for a good while now, I consider this complete and very stable. I plan to attempt a Tohoe Hackintosh once it's stable since it's a bit scary to Hackintosh a Beta before it actually releases, one update can actually break anything. For now, I'm very happy with my Sequoia Hackintosh, it's a bit laggy, but it works.
