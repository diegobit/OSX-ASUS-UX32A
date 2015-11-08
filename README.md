# Asus UX32A Hackintosh configuration
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
- Current OS X version: El Capitan 10.10.1
- Working: CPU steps, sleep, audio, wifi, bluetooth, multitouch, FN keys etc...
- Not working: Card reader
- Not working (not tested properly): HDMI, iMessage, Handoff, Instant Hotspot (even though in the bluetooth info section of OS X these are "ON"), hibernation

**What is inside this repo:**
- Clover config.plist and drivers
- DSDT and SSDT (SSDT generated with ssdtPRgen v13.2: "$ ./ssdtPRgen.sh -x 1 -lfm 900")
- Various kexts:
	- ACPIBatteryManager
	- ApplePS2SmartTouchPad: touchpad and keyboard [this is set to ISO and italian keyboard layout]
	- AsusNBFnKeys
	- Brcm\*: bluetooth
	- DummyHDA: to use Apple's audio driver
	- EAPDFix: to fix audio after sleep
	- FakePCIID\*: to make wifi and USB 3.0 work
	- FakeSMC: essential to boot OS X; no plugins installed
	- IntelBacklight: for display backlight
