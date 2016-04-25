# OS X on Asus UX32A
This is a working set of kexts and configurations for running OS X on an ASUS UX32A laptop.

**System:**
- UEFI firmware version: 216
- CPU: Intel i3-3217U
- GPU: Intel HD4000
- Audio: ALC269VB
- Wireless chip: Azurewave aw-ce123h:
  - Wifi: Broadcom BCM4352 (IDs: 14e4, 43b1)
  - Bluetooth: Broadcom 20702A3 (BCM20702A0) (IDs: 0x3404, 0x13d3)

**Status:**
- Current OS X version: El Capitan 10.11.4
- Bootloader: [Clover](http://sourceforge.net/projects/cloverefiboot/) EFI v3469
- Working: CPU steps, sleep, audio, wifi, bluetooth, multitouch, FN keys, USB ports etc, HDMI...
- Not working: Card reader, left USB port (devices gets attached to the USB 2.0 bus), VGA port, iMessage
- Not working (or not tested properly): Handoff, Instant Hotspot (even though in the bluetooth info section of OS X these are "ON"), hibernation

**What is inside this repo:**
- [Clover](http://sourceforge.net/projects/cloverefiboot/) config.plist and drivers (please see the "*How to install Clover* section"
- DSDT and SSDT (SSDT generated with [ssdtPRgen](https://github.com/Piker-Alpha/ssdtPRGen.sh) v13.2: "$ ./ssdtPRgen.sh -x 1 -lfm 900")
- Various kexts:
  - [ACPIBatteryManager](https://bitbucket.org/RehabMan/os-x-acpi-battery-driver)
  - [ApplePS2SmartTouchPad](http://forum.osxlatitude.com/index.php?/topic/1948-elan-focaltech-and-synaptics-smart-touchpad-driver-mac-os-x/): touchpad and keyboard (this is set to ISO and italian keyboard layout)
  - [AsusNBFnKeys](http://forum.osxlatitude.com/index.php?/topic/1968-fn-hotkey-and-als-sensor-driver-for-asus-notebooks/)
  - [Brcm\*](https://bitbucket.org/RehabMan/os-x-brcmpatchram): bluetooth
  - DummyHDA: to use Apple's audio driver
  - [EAPDFix](http://forum.osxlatitude.com/index.php?/topic/3084-eapdjack-sense-fix-no-audiojack-sense-issue-after-sleep/): to fix audio after sleep
  - [FakePCIID\*](https://bitbucket.org/RehabMan/os-x-fake-pci-id): to make wifi and USB 3.0 work
  - [FakeSMC](http://www.hwsensors.com): essential to boot OS X; no plugins installed
  - [IntelBacklight](https://bitbucket.org/RehabMan/os-x-intel-backlight): for display backlight

**How to install Clover:**
- I install Clover with these configuration (sorry for the Italian screenshot):
![Clover configuration screenshot](/screenshots/cloverConfigurations.png)
- The drivers included in *EFI/CLOVER/drivers64UEFI* are only the ones *not* bundled with the installer of Clover.