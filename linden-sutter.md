# lindensutter
How to manual for Linden Sutterm 2P microscope

### Starting up the scope

1. Turn on all equipment
 - Scanners - MDR-6
 - Objective motor - MP285
 - PMT and mirrors - PS-2
 - Pockels cell - Conoptics 302RM (power strip under table)
 - Laser - Turn key on front of Mai-Tai box (laser is not active until software is run)

3. Start software
 - MaiTai.
 Serial port needs to be correct, as of Sept 2015 it is COM4

 - Serial Splitter.
 COM1 is split into COM13 and COM14

 - Matlab.
   Start ScanImage by typing 'scanimage' in Matlab command prompt.
   Select a valid .ini file, needs to have "port='COM13'".

 - Igor.
   Run 'mp285_2p.ipf'.
   In Igor, activate menus by clicking in Igor command window.
   Select menu 'mp285 -> Init User'.
   Open a user .txt file.

### Downloads
 - Example ScanImage .ini file

   Critical to share objective motor serial port between Matlab and Igor.

 - Serial Splitter software
 [Serial Port Splitter 5.0](http://www.eltima.com/products/serialsplitter/) by Etima Software

 - Igor code for mp285_2p
 - Example mp285_2p user .txt file
 
### Wiring diagram
 - [upload images of how it is wired]
 - [link to scan image documentation]
 

### Parts list
 - **Laser**, MaiTai Deep-See, Serial #4754
 - **Lamdba Half-Wave Plate**, xxx
 - **Glan Polarizer**, xxx
 - **Pockels cell**, xxx
 - **Beam Expander**, xxx
 - **Mirror Mounts**, xxx
 - **Mirrors**, xxx
 - **PMTs**, 2x Hamamatsu xxx, GaAsp
 - **PMT Filters**
  - Red, original was HQ610/75m, replaced May 2015 with ET620/60m 
  - Green, xxx
 - **Scope Body**, Sutter MOM [link]
 - **Scanners**, Cambridge xxx, 6mm mirrors
 - **Objective**, Zeiss 20x, xxx
 - **Software**, ScanImage 3.8, Igor Pro, Serial Splitter, MaiTai Control

### Emmission path filters

 - Top PMT is HQ 535/50 M 2P 18 DEG 219730
 - Right PMT is ET 620/60 M 291809

### Consumables
Order these at [Spectra-Physics Service Parts and Consumables](http://www.spectra-physics.com/service/service-parts)

  - Purge Filter, 90035539, dessicant filter in the laser head
  - Water filter, 2604-0488 or 2604-0488, simple water filter in blue bucket on back of chiller
  - 1607-0546, NALCO circulating solution, 1 gallon - fill tank as required
  - 1607-0547, NALCO cleaner solution, 1 gallon - to be used as required to clean contaminated chiller
  - 0129-9323S, J-series Power Supply, air filters J40/J80 (qty.3)
