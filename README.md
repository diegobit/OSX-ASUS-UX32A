# OS X on Asus UX32A
This is a working set of kexts and configurations for running OS X on an ASUS UX32A laptop. The purpose of this repo is to help improving an already booting system, not to help installing it: I have OS X for some time, so and I don't remember the problems occurred to me during the installation. [Here](http://www.insanelymac.com/forum/topic/298027-guide-aio-guides-for-hackintosh/)'s a good All-in-one guide and [here](http://www.insanelymac.com/forum/forum/137-osx86-installation/)'s a specialized forum.

### System information
- Model: UX32A-R3028H
- UEFI firmware version: 216
- CPU: Intel i3-3217U
- GPU: Intel HD4000
- Audio: ALC269VB (Device: 0x80861E20, CodecID: 0x10EC0269)
- Wireless chip: Azurewave aw-ce123h (the original wireless card doesn't work, it *must* be replaced):
  - Wifi: Broadcom BCM4352 (IDs: 14e4, 43b1)
  - Bluetooth: Broadcom 20702A3 (BCM20702A0) (IDs: 0x3404, 0x13d3)

Some detailed system information gathered from Linux: [System Hardware/](https://github.com/diegobit/OSX-ASUS-UX32A/tree/master/System%20Hardware).
You can also check under OS X with the preinstalled System Information.app, DCPImanager or IORegistryExplorer.

### Status
- Current OS X version: El Capitan 10.11.6
- Bootloader: [Clover](http://sourceforge.net/projects/cloverefiboot/) EFI
- Working: CPU steps, sleep, audio, wifi, bluetooth, multitouch, FN keys, USB ports<sup>1</sup>, HDMI, HDMI audio...
- Not working: Card reader, VGA port, iMessage
- Not working (or not tested properly): Handoff, Instant Hotspot (even though in the bluetooth info section of OS X these are "ON"), hibernation

### What's inside this repo
- [Clover](http://sourceforge.net/projects/cloverefiboot/) config.plist and drivers (see section *How to install Clover*)
- DSDT and SSDT (SSDT generated with [ssdtPRgen](https://github.com/Piker-Alpha/ssdtPRGen.sh) v13.2: "$ ./ssdtPRgen.sh -x 1 -lfm 900")
- Various kexts:
  - [ACPIBatteryManager](https://bitbucket.org/RehabMan/os-x-acpi-battery-driver)
  - [ApplePS2SmartTouchPad](http://forum.osxlatitude.com/index.php?/topic/1948-elan-focaltech-and-synaptics-smart-touchpad-driver-mac-os-x/): touchpad and keyboard (this is set to ISO and italian keyboard layout)
  - [AsusNBFnKeys](http://forum.osxlatitude.com/index.php?/topic/1968-fn-hotkey-and-als-sensor-driver-for-asus-notebooks/)
  - [Brcm\*](https://bitbucket.org/RehabMan/os-x-brcmpatchram): bluetooth (If you have a different wireless card download *BrcmFirmwareRepo.kext* from the official repo, NOT from here, because this one only works on this wireless card)
  - DummyHDA: to use Apple's audio driver (If you have issues: a [complete Audio guide](http://forum.osxlatitude.com/index.php?/topic/1946-complete-applehda-patching-guide/), a [very good automatic patcher](http://www.insanelymac.com/forum/files/file/496-applehda-patcher/))
  - [EAPDFix](http://forum.osxlatitude.com/index.php?/topic/3084-eapdjack-sense-fix-no-audiojack-sense-issue-after-sleep/): to fix audio after sleep. As an alternative, try [CodecCommander](https://bitbucket.org/RehabMan/os-x-eapd-codec-commander/overview)
  - [FakePCIID\*](https://bitbucket.org/RehabMan/os-x-fake-pci-id): to make wifi and USB 3.0 work
  - [FakeSMC](http://www.hwsensors.com): essential to boot OS X; no plugins installed. I added a key (*ACID*) to its Info.plist to fix this: https://github.com/RehabMan/OS-X-ACPI-Battery-Driver/issues/8
  - [IntelBacklight](https://bitbucket.org/RehabMan/os-x-intel-backlight): for display backlight

### How to install Clover
- (The drivers included in *EFI/CLOVER/drivers64UEFI* are only the ones *not* bundled with the installer of Clover)
- I install Clover with these configuration:

![Clover configuration screenshot](/screenshots/clover-setup-info.png)


### Current trackpad gestures ([ApplePS2SmartTouchPad](http://forum.osxlatitude.com/index.php?/topic/1948-elan-focaltech-and-synaptics-smart-touchpad-driver-mac-os-x/))

| Gesture       | details                   | Action                                  |
| ------------- | ------------------------- | --------------------------------------- |
| *Tap*         | Two fingers               | Right mouse click                       |
|               | Three fingers             | Middle mouse click                      |
|               | Four fingers              | Show desktop                            |
|               | Five fingers              | Launchpad                               |
| *Click*       | One finger everywhere     | Left mouse click                        |
| *Swipe*       | Two fingers               | Scrolling                               |
|               | Three fingers left/right  | Desktop switch                          |
|               | Three fingers up					|	Mission control                         |
|               | Three fingers down				|	App window list                         |
|               | Four fingers up					  | Fullscreen                              |
|               | Four fingers down				  | SHIFT CMD T ("Show all tabs" in Safari) |
|               | Four fingers left/right		| Go back/forward (histories)             |
| *Pinch*       | Four fingers in           | Mission Control                         |
| *Long tap*    | Three fingers             | CMD W (close window)                    |
|               | Four fingers			        |	Force close apps window                 |

---

**1:** *In this repo I said the left port didn't work, it was Android File Transfer's fault. It causes MANY problems with USB ports.
