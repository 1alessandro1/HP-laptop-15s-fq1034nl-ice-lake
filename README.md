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
