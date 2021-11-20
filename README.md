# HP 15s-FQ1034NL
This repository contains the necessary files and information to successfully boot macOS on this laptop. 


 ### BIOS offsets (F21)
 
- **CFG Lock** = setup_var 0x43 0x0 (Disabled)
 
- **DVMT Pre-Allocated** = setup_var 0xA13 0x2 (64MB)
 
- **DVMT Total Gfx Mem** = setup_var 0xA14 0x3 (MAX)
 
- **SATA Controller(s)** = 0xB78 0x1 (Enabled) - if you have the cable inside
 
- **SATA Mode** = setup_var 0xB79 0x0 (AHCI) - this should be on zero by default
