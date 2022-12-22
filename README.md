# Dell 5750 Hackintosh

A collection of all files needed to run Monterey on a Dell Precision 17 5750-6251 laptop.

## Software

| Name  | Version |
| ------------- | ------------- |
| MacOS  | Monterey 12.6.2  |
| BIOS  | 1.18.0  |
| OpenCore  | 0.8.7  |

## Hardware

Replaced:
* SSD: Micron 2200S NVMe 512GB (193727601E9F) replaced by two WD Black SN750 
* RAM: Micron DDR4 16GB replaced by 2x16GB HyperX DDR4 SODIMM PC4-23400

<details>
  <summary>OCSysInfo dump and grep of Linux input</summary>

```
─ CPU
  └── Intel(R) Core(TM) i7-10850H CPU @ 2.70GHz
      ├── Cores: 6
      ├── Threads: 12
      ├── SSE: SSE4.2
      ├── SSSE3: Supported
      └── Codename: Comet Lake

─ Motherboard
  ├── Model: 0DHP00
  └── Manufacturer: Dell Inc.

─ GPU
  ├── NVIDIA Quadro RTX 3000 with Max-Q Design
  │   ├── Device ID: 0x1F36
  │   ├── Vendor: 0x10DE
  │   ├── PCI Path: PciRoot(0x0)/Pci(0x1,0x0)/Pci(0x0,0x0)
  │   └── ACPI Path: \_SB.PCI0.PEG0.PEGP
  └── Intel(R) UHD Graphics
      ├── Device ID: 0x9BC4
      ├── Vendor: 0x8086
      ├── PCI Path: PciRoot(0x0)/Pci(0x2,0x0)
      └── ACPI Path: \_SB.PCI0.GFX0

─ Memory
  ├── KHX2933C17S4/16G (Part-Number)
  │   ├── Type: DDR4
  │   ├── Slot
  │   │   ├── Bank: 
  │   │   └── Channel: DIMM A
  │   ├── Frequency (MHz): 2933 MHz
  │   ├── Manufacturer: 019800000000
  │   └── Capacity: 16384MB
  └── KHX2933C17S4/16G (Part-Number)
      ├── Type: DDR4
      ├── Slot
      │   ├── Bank: 
      │   └── Channel: DIMM B
      ├── Frequency (MHz): 2933 MHz
      ├── Manufacturer: 019800000000
      └── Capacity: 16384MB

─ Network
  ├── Comet Lake PCH CNVi WiFi
  │   ├── Device ID: 0x06F0
  │   ├── Vendor: 0x8086
  │   ├── PCI Path: PciRoot(0x0)/Pci(0x14,0x3)
  │   └── ACPI Path: \_SB.PCI0.CNVW
  └── Unknown Network Controller
      ├── Device ID: 0x8153
      └── Vendor: 0x0BDA

─ Audio
  ├── Intel(R) Display Audio
  │   ├── Device ID: 0x280B
  │   └── Vendor: 0x8086
  ├── G70 [GeForce 7800 GS]
  │   ├── Device ID: 0x0093
  │   └── Vendor: 0x10DE
  └── Unknown Sound Device
      ├── Device ID: 0xAE35
      └── Vendor: 0x8086

─ Input
  ├── USB Input Device (USB)
  │   ├── Product ID: 0x301D
  │   └── Vendor ID: 0x413C
  └── HID-compliant mouse
      ├── Product ID: 0x301D
      └── Vendor ID: 0x413C

─ Storage
  ├── WDS250G3X0C-00SJG0
  │   ├── Type: NVMe
  │   ├── Connector: PCI Express
  │   └── Location: Internal
  └── WDS100T3X0C-00SJG0
      ├── Type: NVMe
      ├── Connector: PCI Express
      └── Location: Internal

```

```
$ dmesg | grep -i input
[    0.473883] input: Lid Switch as /devices/LNXSYSTM:00/LNXSYBUS:00/PNP0C0D:00/input/input0
[    0.473931] input: Power Button as /devices/LNXSYSTM:00/LNXSYBUS:00/PNP0C0C:00/input/input1
[    0.473972] input: Sleep Button as /devices/LNXSYSTM:00/LNXSYBUS:00/PNP0C0E:00/input/input2
[    0.511167] input: AT Translated Set 2 keyboard as /devices/platform/i8042/serio0/input/input3
[    1.053653] input: ELAN2097:00 04F3:2A15 Touchscreen as /devices/pci0000:00/0000:00:15.0/i2c_designware.0/i2c-2/i2c-ELAN2097:00/0018:04F3:2A15.0001/input/input6
[    1.053718] input: ELAN2097:00 04F3:2A15 as /devices/pci0000:00/0000:00:15.0/i2c_designware.0/i2c-2/i2c-ELAN2097:00/0018:04F3:2A15.0001/input/input7
[    1.053748] input: ELAN2097:00 04F3:2A15 as /devices/pci0000:00/0000:00:15.0/i2c_designware.0/i2c-2/i2c-ELAN2097:00/0018:04F3:2A15.0001/input/input8
[    1.053793] hid-generic 0018:04F3:2A15.0001: input,hidraw0: I2C HID v1.00 Device [ELAN2097:00 04F3:2A15] on i2c-ELAN2097:00
[    1.083513] input: DELL0990:00 04F3:311C Mouse as /devices/pci0000:00/0000:00:15.1/i2c_designware.1/i2c-3/i2c-DELL0990:00/0018:04F3:311C.0002/input/input10
[    1.083587] input: DELL0990:00 04F3:311C Touchpad as /devices/pci0000:00/0000:00:15.1/i2c_designware.1/i2c-3/i2c-DELL0990:00/0018:04F3:311C.0002/input/input11
[    1.083655] hid-generic 0018:04F3:311C.0002: input,hidraw1: I2C HID v1.00 Mouse [DELL0990:00 04F3:311C] on i2c-DELL0990:00
[    1.693895] input: PS/2 Generic Mouse as /devices/platform/i8042/serio1/input/input5
[    2.877895] input: Intel HID events as /devices/platform/INT33D5:00/input/input13
[    2.958626] input: Dell Dell Universal Receiver as /devices/pci0000:00/0000:00:14.0/usb1/1-8/1-8.2/1-8.2:1.0/0003:413C:301D.0005/input/input14
[    3.032075] input: Integrated_Webcam_HD: Integrate as /devices/pci0000:00/0000:00:14.0/usb1/1-5/1-5:1.0/input/input15
[    3.079884] hid-generic 0003:413C:301D.0005: input,hidraw2: USB HID v1.11 Keyboard [Dell Dell Universal Receiver] on usb-0000:00:14.0-8.2/input0
[    3.082025] input: Dell Dell Universal Receiver Mouse as /devices/pci0000:00/0000:00:14.0/usb1/1-8/1-8.2/1-8.2:1.1/0003:413C:301D.0006/input/input16
[    3.391806] input: Dell Dell Universal Receiver Consumer Control as /devices/pci0000:00/0000:00:14.0/usb1/1-8/1-8.2/1-8.2:1.1/0003:413C:301D.0006/input/input17
[    3.399622] input: ELAN2097:00 04F3:2A15 as /devices/pci0000:00/0000:00:15.0/i2c_designware.0/i2c-2/i2c-ELAN2097:00/0018:04F3:2A15.0001/input/input19
[    3.401266] input: Integrated_Webcam_HD: Integrate as /devices/pci0000:00/0000:00:14.0/usb1/1-5/1-5:1.2/input/input23
[    3.451696] input: Dell Dell Universal Receiver System Control as /devices/pci0000:00/0000:00:14.0/usb1/1-8/1-8.2/1-8.2:1.1/0003:413C:301D.0006/input/input18
[    3.451738] hid-generic 0003:413C:301D.0006: input,hidraw0: USB HID v1.11 Mouse [Dell Dell Universal Receiver] on usb-0000:00:14.0-8.2/input1
[    3.451787] input: ELAN2097:00 04F3:2A15 UNKNOWN as /devices/pci0000:00/0000:00:15.0/i2c_designware.0/i2c-2/i2c-ELAN2097:00/0018:04F3:2A15.0001/input/input20
[    3.452009] input: ELAN2097:00 04F3:2A15 UNKNOWN as /devices/pci0000:00/0000:00:15.0/i2c_designware.0/i2c-2/i2c-ELAN2097:00/0018:04F3:2A15.0001/input/input21
[    3.452344] hid-multitouch 0018:04F3:2A15.0001: input,hidraw3: I2C HID v1.00 Device [ELAN2097:00 04F3:2A15] on i2c-ELAN2097:00
[    3.453162] hid-generic 0003:413C:301D.0007: hiddev0,hidraw4: USB HID v1.11 Device [Dell Dell Universal Receiver] on usb-0000:00:14.0-8.2/input2
[    3.590826] input: Dell WMI hotkeys as /devices/platform/PNP0C14:03/wmi_bus/wmi_bus-PNP0C14:03/9DBB5994-A997-11DA-B012-B622A1EF5492/input/input24
[    3.670479] input: HDA NVidia HDMI/DP,pcm=3 as /devices/pci0000:00/0000:00:01.0/0000:01:00.1/sound/card0/input25
[    3.801055] input: HDA NVidia HDMI/DP,pcm=7 as /devices/pci0000:00/0000:00:01.0/0000:01:00.1/sound/card0/input26
[    3.801117] input: HDA NVidia HDMI/DP,pcm=8 as /devices/pci0000:00/0000:00:01.0/0000:01:00.1/sound/card0/input27
[    3.801166] input: HDA NVidia HDMI/DP,pcm=9 as /devices/pci0000:00/0000:00:01.0/0000:01:00.1/sound/card0/input28
[    3.801203] input: HDA NVidia HDMI/DP,pcm=10 as /devices/pci0000:00/0000:00:01.0/0000:01:00.1/sound/card0/input29
[    3.801252] input: HDA NVidia HDMI/DP,pcm=11 as /devices/pci0000:00/0000:00:01.0/0000:01:00.1/sound/card0/input30
[    3.801299] input: HDA NVidia HDMI/DP,pcm=12 as /devices/pci0000:00/0000:00:01.0/0000:01:00.1/sound/card0/input31
[    3.809030] input: DELL0990:00 04F3:311C Mouse as /devices/pci0000:00/0000:00:15.1/i2c_designware.1/i2c-3/i2c-DELL0990:00/0018:04F3:311C.0002/input/input32
[    3.809098] input: DELL0990:00 04F3:311C Touchpad as /devices/pci0000:00/0000:00:15.1/i2c_designware.1/i2c-3/i2c-DELL0990:00/0018:04F3:311C.0002/input/input33
[    3.809148] hid-multitouch 0018:04F3:311C.0002: input,hidraw1: I2C HID v1.00 Mouse [DELL0990:00 04F3:311C] on i2c-DELL0990:00
[    4.503940] input: Video Bus as /devices/LNXSYSTM:00/LNXSYBUS:00/PNP0A08:00/device:00/LNXVIDEO:00/input/input35
[    4.534681] input: Video Bus as /devices/LNXSYSTM:00/LNXSYBUS:00/PNP0A08:00/LNXVIDEO:01/input/input36
[    5.435866] input: sof-soundwire Headset Jack as /devices/pci0000:00/0000:00:1f.3/sof_sdw/sound/card1/input37
[    5.435956] input: sof-soundwire HDMI/DP,pcm=5 as /devices/pci0000:00/0000:00:1f.3/sof_sdw/sound/card1/input38
[    5.435989] input: sof-soundwire HDMI/DP,pcm=6 as /devices/pci0000:00/0000:00:1f.3/sof_sdw/sound/card1/input39
[    5.436034] input: sof-soundwire HDMI/DP,pcm=7 as /devices/pci0000:00/0000:00:1f.3/sof_sdw/sound/card1/input40
[   12.243060] rfkill: input handler disabled
[  912.641166] input: Dell Dell Universal Receiver as /devices/pci0000:00/0000:00:14.0/usb1/1-8/1-8.2/1-8.2:1.0/0003:413C:301D.0008/input/input41
[  912.698389] hid-generic 0003:413C:301D.0008: input,hidraw0: USB HID v1.11 Keyboard [Dell Dell Universal Receiver] on usb-0000:00:14.0-8.2/input0
[  912.700621] input: Dell Dell Universal Receiver Mouse as /devices/pci0000:00/0000:00:14.0/usb1/1-8/1-8.2/1-8.2:1.1/0003:413C:301D.0009/input/input42
[  912.700815] input: Dell Dell Universal Receiver Consumer Control as /devices/pci0000:00/0000:00:14.0/usb1/1-8/1-8.2/1-8.2:1.1/0003:413C:301D.0009/input/input43
[  912.758348] input: Dell Dell Universal Receiver System Control as /devices/pci0000:00/0000:00:14.0/usb1/1-8/1-8.2/1-8.2:1.1/0003:413C:301D.0009/input/input44
[  912.758709] hid-generic 0003:413C:301D.0009: input,hidraw2: USB HID v1.11 Mouse [Dell Dell Universal Receiver] on usb-0000:00:14.0-8.2/input1
[  912.760513] hid-generic 0003:413C:301D.000A: hiddev0,hidraw4: USB HID v1.11 Device [Dell Dell Universal Receiver] on usb-0000:00:14.0-8.2/input2
```

</details>


## ✔️ Status
| Hardware | Model | Status | Comments |
| ------------- | ------------- | ------------- | ------------- |
| **CPU** | Intel Core i7-10850H, Model: 165, Processor ID: A0652 | ✅ Working | It seems power management working. I didn't use CPUFriend kext and left default LFM value (1300Mhz) although BIOS states that min clock speed is 800 mhz. |
| **iGPU** | Intel CometLake-H GT2 [UHD Graphics] | ✅ Working | 1536 Mb of VRAM |
| **Internal Display** | 3840x2400 (WQUXGA) UI looks like 1920x1200@60.00Hz | ✅ Working | Internal eDP display fully working including Touchscreen (ELAN?) and Backlight control. Automatically Adjust Brightness (NO)|
| **External Display(s)** | DP 1.4, HDMI 2.0 via USB-C adapter Dell DA310 | ❌ Not Working | |
| **SSD** | SSD WD Black SN750 1TB + 250GB | ✅ Working |
| **Trackpad** | DELL0990??? | ✅ Working | Working with full gesture support (5 fingers) but the hardware buttons are not working. You can use left/right click with touch tap (change in settings). |
| **Wi-Fi/ BT** | Intel(R) Wi-Fi 6 AX201 160MHz | ✅ Working | |
| **LAN** | Realtek USB GbE Family Controller via USB-C adapter Dell DA310, HardwareID: USB\VID_0BDA&PID_8153&REV_3100 | ✅ Working | |
| **Thunderbolt/ USB-C** | Intel JHL7540 (Titan Ridge 4C 2018) | ✅ Working | USB-C charging works. Thunderbolt and USB-C devices are working. Tested with a Dell DA310 Thunderbolt Dock and an USB-C storage. |
| **USB** | | ✅ Working | All Ports fully working with USB 2.0, 3.0 and 3.1 (Gen1) speed |
| **Internal Speakers** | PCI\VEN_8086&DEV_06C8&SUBSYS_09901028&REV_00 | ❌ Not Working | 0x06C8 Not supported by AppleALC |
| **Internal Microphone array** | | ❌ Not Working |
| **Headphone Jack** | | ❌ Not Working | |
| **Webcam** | | ✅ Working |
| **SDXC reader** | Realtek RTS5260 | ✅ Working |
| **Fingerprint reader** | | ❌ Not working | Will never work, because of MacBooks with TouchID and T2 chip and proprietary Windows drivers for Dell. |


## 🖥 Installation

macOS Installer: Drives you wish to install macOS on must be both of GUID partition Scheme and APFS !!!!

### BIOS/UEFI settings

[Enable BIOS settings optimal for macOS](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#intel-bios-settings)

### Adjust UEFI variables to enable 4K@60Hz and disable CFG lock

Needed tools:

* **modGRUBShell.efi** on a FAT32 USB-Stick or on the OpenCore EFI  
* **Dell_PFS_Extract**
* **UEFITool_NE_A58**
* **Ifrextractor**

<details>
  <summary>Click to see detailed instructions</summary>

#### Increase DVMT Pre-Allocated up to 64Mb

1. Download your BIOS flash program via Dell (search for your model, then click `Drivers and Downloads` and filter for `BIOS`)
2. Dell_PFS_Extract: Select folder containing your Dell .exe file (This will extract the raw BIOS .bin file)
  ```
  $ Dell_PFS_Extract.py XPS_17_9700_Precision_5750_1.18.0.exe

  Dell PFS Update Extractor v5.1

  *** XPS_17_9700_Precision_5750_1.18.0.exe

      Extracted Dell PFS 1 > XPS_17_9700_Precision_5750_1.18.0 > Utilities section!

      Extracted Dell PFS 1 > XPS_17_9700_Precision_5750_1.18.0 > Firmware section!

  Done!
  ```   
3. UEFITool_NE_A58: Open `1 System BIOS with BIOS Guard vx.x.x.bin` and export the `Setup` IFR section
  ```
  $ UEFITool ./XPS_17_9700_Precision_5750_1.18.0.exe_extracted/Firmware/1\ XPS_17_9700_Precision_5750_1.18.0\ --\ 1\ System\ BIOS\ with\ BiosGuard\ v1.18.0.bin

  CTRL+F -> Text (Unicode  checked) : "CFG Lock" or "DVMT"

  right click on "PE32 image section" > Extract as is > Section_PE32_image_E6A7A1CE-5881-4B49-80BE-69C91811685C_Setup.sct
  ```

4. Ifrextractor: Use `Section_PE32_image_E6A7A1CE-5881-4B49-80BE-69C91811685C_Setup.sct` as input file and write output to `Section_PE32_image_Setup IFR.txt`
  ```
  $ ifrextract Section_PE32_image_E6A7A1CE-5881-4B49-80BE-69C91811685C_Setup.sct Section_PE32_image_Setup IFR.txt

  find "CFG Lock" or "DVMT Pre-Allocated" inside setup.txt
  ```

5. Find variables by their name in the .txt file via Ctrl + F (e.g. DVMT or CFG)

  The line should be something like this for "DVMT Pre-Allocated":

  ```
  One Of: DVMT Pre-Allocated, VarStoreInfo (VarOffset/VarName): 0xF5, VarStore: 0x2, QuestionId: 0x29C, Size: 1, Min: 0x0, Max 0xFE, Step: 0x0 {05 91 96 12 A9 12 9C 02 02 00 F5 00 10 10 00 FE 00}
  
Default: DefaultId: 0x0, Value (8 bit): 0x1 {5B 06 00 00 00 01}                                                                                                                     
One Of Option: 0M, Value (8 bit): 0x0 {09 07 97 12 00 00 00}                                                                                                                        
One Of Option: 32M, Value (8 bit): 0x1 {09 07 98 12 00 00 01}                                                                                                                       
One Of Option: 64M, Value (8 bit): 0x2 {09 07 99 12 00 00 02}                                                                                                                       
One Of Option: 4M, Value (8 bit): 0xF0 {09 07 9A 12 00 00 F0}                                                                                                                       
One Of Option: 8M, Value (8 bit): 0xF1 {09 07 9B 12 00 00 F1}                                                                                                                       
One Of Option: 12M, Value (8 bit): 0xF2 {09 07 9C 12 00 00 F2}                                                                                                                      
One Of Option: 16M, Value (8 bit): 0xF3 {09 07 9D 12 00 00 F3}                                                                                                                      
One Of Option: 20M, Value (8 bit): 0xF4 {09 07 9E 12 00 00 F4}                                                                                                                      
One Of Option: 24M, Value (8 bit): 0xF5 {09 07 9F 12 00 00 F5}                                                                                                                      
One Of Option: 28M, Value (8 bit): 0xF6 {09 07 A0 12 00 00 F6}                                                                                                                      
One Of Option: 32M/F7, Value (8 bit): 0xF7 {09 07 A1 12 00 00 F7}                                                                                                                   
One Of Option: 36M, Value (8 bit): 0xF8 {09 07 A2 12 00 00 F8}                                                                                                                      
One Of Option: 40M, Value (8 bit): 0xF9 {09 07 A3 12 00 00 F9}                                                                                                                      
One Of Option: 44M, Value (8 bit): 0xFA {09 07 A4 12 00 00 FA}                                                                                                                      
One Of Option: 48M, Value (8 bit): 0xFB {09 07 A5 12 00 00 FB}                                                                                                                      
One Of Option: 52M, Value (8 bit): 0xFC {09 07 A6 12 00 00 FC}                                                                                                                      
One Of Option: 56M, Value (8 bit): 0xFD {09 07 A7 12 00 00 FD}                                                                                                                      
One Of Option: 60M, Value (8 bit): 0xFE {09 07 A8 12 00 00 FE}               
  ```
    
Important data (you may have different values):
  * **VarStore: 0x2** - ID of VarStore name
  * **VarStoreInfo (VarOffset/VarName): 0xF5** - Offset in VarStore
  * **Size: 1** - variable size ???
  * One Of Option: 64M, Value (8 bit): **0x2** {09 07 99 12 00 00 02} - value for 64Mb (default = 32M)

For some BIOS versions (including mine) it is needed to find correct VarStore name by ID taken from above important data. In my case search line is "VarStoreId: 0x2":

```
VarStoreEFI: VarStoreId: 0x2 [72C5E28C-7783-43A1-8767-FAD73FCCAFA4], Attrubutes: 7, Size: 30F, Name: SaSetup {26 22 02 00 8C E2 C5 72 83 77 A1 43 87 67 FA D7 3F CC AF A4 07 00 00 00 0F 03 53 61 53 65 74 75 70 00}
```

**SaSetup** - name of 0xF5 variable found by "VarStoreId: 0x2" search line

6. Run the Modified GRUB Shell and write the following command (setup_var_cv): **setup_var_cv SaSetup 0xF5 0x01 0x2**

  ```
  setup_var_cv nameOfVarStore offsetInVarStore [optional variable size] [optional value to write]
  ```
  Reboot your computer and check.

#### Do the same to disable CFG lock

The line should be something like this for "CFG Lock":

```
One Of: CFG Lock, VarStoreInfo (VarOffset/VarName): 0x3E, VarStore: 0x3, QuestionId: 0x166, Size: 1, Min: 0x0, Max 0x1, Step: 0x0 {05 91 AD 03 AE 03 66 01 03 00 3E 00 10 10 00 01 00}
	One Of Option: Disabled, Value (8 bit): 0x0 {09 07 04 00 00 00 00}
	One Of Option: Enabled, Value (8 bit): 0x1 (default) {09 07 03 00 30 00 01}
End One Of {29 02}
```

Important data (you may have different values):
  * **VarStore: 0x3** - ID of VarStore name
  * **VarStoreInfo (VarOffset/VarName): 0x3E** - Offset in VarStore
  * **Size: 1** - variable size ???
  * One Of Option: Disabled, Value (8 bit): **0x0** {09 07 04 00 00 00 00} - value to disable CFG Lock

Find correct VarStore name by ID from above important data. In my case search line is "VarStoreId: 0x3":

```
VarStoreEFI: VarStoreId: 0x3 [B08F97FF-E6E8-4193-A997-5E9E9B0ADB32], Attrubutes: 7, Size: 334, Name: CpuSetup {26 23 03 00 FF 97 8F B0 E8 E6 93 41 A9 97 5E 9E 9B 0A DB 32 07 00 00 00 34 03 43 70 75 53 65 74 75 70 00}
```

**CpuSetup** - name of 0x3E variable found by "VarStoreId: 0x3" search line

Run the Modified GRUB Shell and write the following command: **setup_var_cv CpuSetup 0x3E 0x01 0x0**

Reboot your computer and check.

</details>

### Create a bootable installer
Grab a free USB stick with at least 16GiB and format it with HFS+ file system and GUID table.

[It is highly recommended to create offline installer](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)

### Configuring EFI
Clone this repository to get the base EFI folder. Copy the folder into the EFI partition you have mounted in the previous step.


## 🛠 Configuration
This section talks about configuring the EFI folder for your exact hardware.
Almost all changes are done inside the OpenCore configuration file. Use the provided version of [ProperTree](https://github.com/corpnewt/ProperTree) to edit `EFI/OC/config.plist`.

**DO NOT USE `EFI/OC/config.plist` CONFIG FILE AS IS!!!**

**[YOU HAVE TO SET UNIQUE SMBIOS SERIAL/UUID BY GenSMBIOS APPLICATION](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/coffee-lake-plus.html#platforminfo)**

## Known Issues:

- Audio not working
- Trackpad physical buttons not working
- Blank screen with Dell logo if trying to sleep

## Useful Links
- [GUIDE: Easy USB Mapping with USBToolbox on Windows](https://www.reddit.com/r/hackintosh/comments/ta1ef4/guide_easy_usb_mapping_with_usbtoolbox_on_windows/)
- [Discussing Dell 5750 on tonymacx86.com](https://www.tonymacx86.com/threads/help-dell-5750-i7-10850h-comet-lake-10th-generation.319861/)
