# HP 15s-FQ1034NL
This repository contains the necessary files and information to successfully boot macOS on this laptop. 


 ### BIOS offsets (F21)
 
- **CFG Lock** = setup_var 0x43 0x0 (Disabled)
 
- **DVMT Pre-Allocated** = setup_var 0xA4 0x5 (160MB)
 
- **DVMT Total Gfx Mem** = setup_var 0xA5 0x3 (MAX)
 
- **SATA Controller(s)** = 0xB78 0x1 (Enabled) - if you have the cable inside 0x5B
 
- **SATA Mode** = setup_var 0xB79 0x0 (AHCI) - this should be on zero by default

- **GPIO Interrupt** = setup_var 0x2CA 0x0

One Of: SATA Controller(s), VarStoreInfo (VarOffset/VarName): 0x5B,

One Of: SATA Mode Selection, VarStoreInfo (VarOffset/VarName): 0x5C


 ### Sleep and `AAPL,ig-platform-id`
 
 It works with:
 - platform-id = 0200518A and default device-id = 528A0000 (cursor problem even with stolenmem set to 00003001
 - platform-id = 01005C8A and device-id = 528A0000


### Wi-Fi speed with AirportItlwm

For compatibility reasons, I chose to use the Intel 8260ac Wireless wifi card 8086:24f3. In order to get the maximum performance, even though when using the recognized country code (IT) it shows 867Mbit (433 x 2 NSS) it actually barely reaches 30Mbit. This does not happen when manually adding the boot argument `itlwm_cc=ZZ` which instead shows 585MBit and it actually reaches those speeds (70-75MB/s)

