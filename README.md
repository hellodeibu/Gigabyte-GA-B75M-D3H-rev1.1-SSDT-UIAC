
**Note:** I realized after creating this file that it is actually incomplete. As my current PC case only had two extra USB2.0 ports in the front, I did not realize this motherboard actually does support two additional USB3 ports through an internal connector. If you have these connected in your PC, this file will be missing this connector. I apologize for this. If I ever replace the PC case with one that has additional USB3 ports, I might update this file, although [there seems to be a better way to do this now](https://www.tonymacx86.com/threads/guide-intel-framebuffer-patching-using-whatevergreen.256490/) that does not require a custom SSDT file at all.

# Gigabyte GA-B75M-D3H rev1.1 SSDT-UIAC
Custom SSDT UIAC for the Gigabyte GA-B75M-D3H rev1.1 motherboard.

Made by following [RehabMan’s guide](https://www.tonymacx86.com/threads/guide-creating-a-custom-ssdt-for-usbinjectall-kext.211311/), saved for future reference and in case anyone else uses this motherboard and is somewhat confused by the guide (as I was, initially).

I have included the `SSDT-UIAC.dsl` file in case you want to make further changes or use this as a template. You can use [MaciASL](https://bitbucket.org/RehabMan/os-x-maciasl-patchmatic) to open and edit the file. Be sure to check **MaciASL » Preferences » iASL » Compiler Options** is set to `ACPI 6.2a` when using the application.

## Note
This is specifically made for the aforementioned motherboard. It might work with other, similar motherboards, but this is untested on my part. If it does end up working, please post an issue so others can know, too. 

The remainder of this README assumes you’re using Clover Configurator. If you use Xcode or something else to modify your Clover config file, replace Clover Configurator specific references with whatever manual step you need to make to get the same result. 

# Installation
This assumes you already have a working Clover setup using [USBInjectAll](https://bitbucket.org/RehabMan/os-x-usb-inject-all).

- Mount your EFI partition (e.g. using Clover Configurator)
- Locate the `EFI/ACPI/patched` folder
- Copy `SSDT-UIAC.aml` into this folder
- Open your config file (`EFI/CLOVER/config.plist`) in Clover Configurator
- In the `Acpi` section, add the `change EHC1 to EH01` and `change EHC2 to EH02` patches (use the `List Of Patches` dropdown menu)
- Check if `SortedOrder` in the bottom-right hand corner of the SSDT section is empty

### In case SSDT SortedOrder is not empty
By default your `config.plist` likely has no SSDT `SortedOrder` set, but in case something is listed there, you’ll have to either empty it, or ensure `SSDT-UIAC` is added to the list.

## Reboot
Reboot and make sure all your USB ports work. You can test this simply by plugging in a USB device in each port and see if it works as expected. [IORegistryExplorer](https://www.tonymacx86.com/index.php?threads/guide-how-make-copy-ioreg.58368/) can be useful for this, too, but it’s not required.

## In case it didn’t work
You might end up with a computer without any working USB ports. If that happens, reboot and when you get to the Clover boot, hit the spacebar having selected your usual boot option and add the `-uia_ignore_rmcf` boot argument. This will ignore all custom SSDT options, which should help you get to a booted machine with working USB ports, after which you can make whatever changes are necessary to fix the issue.

# Screenshot
![IORegistryExplorer](https://github.com/hellodeibu/Gigabyte-GA-B75M-D3H-rev1.1-SSDT-UIAC/blob/master/Screenshots/IORegistryExplorer.png)

