
### Building issues


This is part of the building and should be non-chargeable.  This email address is only set up for M&S (billable) work.  All regular maintenance issues are more quickly handled thru Customer Service @ 5-3323, they are available 24/7.

if there is aproblem with building (usually cooling), do not email facworkrequest@jhmi.edu


### Startup software

 - Prairie View : To scan 2p images
 - Prairie Canvas (Igor Pro) : To construct a canvas of video and 2p images


 - putty : To login to Raspberry Pi treadmill
 - VirtualDub : To view a live video feed from Raspberry Pi camera
   - turn on video feed with 'File - Capture AVI'

### Raw data from Prairie

Raw data shoud be saved in following locations. When you set a 'session id' in Igor mp285Canvas, these are set automatically (if Prairie View is running).

Raw data is on drive f:\

    f:\cudmore\data


### To DO
 - hook up dimmer to treadmill green led
 - hook up on/off switch to treadmill ir
 - get 4-8 port powered usb box. We are running out of usb ports
 - Make simple interface in Igor to show video feed
 - Get 2x backup motor driver borads, first look up to see if there is a new version
 - make mp285 finalize when canvas is closed (Ask user and default to yet).
    on click 'session id', check if there is an existing canvas open and warn
    this will work real sweet without really changing code


### Init Igor PrairieCanvas
 - Open PrairieCanvas.ipf (desktop shortcut). Should open in Igor 6
 - Click on empty command window to activate menus
 - Select menu 'MP285 - Load User' and select cudmore_prairie.txt
    This file is in 
    F:cudmore:apps:bJHU:MapManager_Options:Users:scope:cudmore_prairie.txt
 - Each time you mount a new mouse, set a new 'session id'
 - When your finished with an imaging session, click 'Finalize and Clear mp285Canvas'

### Hooking up treadmill

 1. 3x BNC should be plugged in to PRairie BNC breakout
    - Trig 1 In, first on treadmill rat-nest
        Purpose: Allow treadmill to trigger prairie view (when Prairie Vie xxx is checked)
    - PCI-6052E AI0, there is a t-splitter, second (middle) on treadmill rat-nest
        Purpose: Allow prairie view to record the frame clock which passes through Treadmill
    - PCI-6052E AI1, third on treadmill rat-nest
        Purpose: Allow prierie view to record status of motor

2. 2x ethernet cables
    - 1st, red, motor, red
    - 2nd, green, ir led and encoder (encoder not used)

3. 1x USB dongle
    - USB dongle from rats-nest to usb port on computer
        Purpose: View video feed from camera on computer with Virtual Dub

4. IMPORTANT: DO this last. Plug in 12v ac/dc on rat-nest
    Purpose: This is motor and ir led power.
    If motor cable (red ethernet) is unplugged while 12v is plugged, will burn motor board
    Always check that motor (red ethernet) is plugged in before pluggin in 12v ac/dc

### To load a canvas

    xxx

### Starting treadmill software
 - login to pi using putty
    ip: 10.16.81.61
    user: pi
    password:
 - cd Sites/treadmill
 - python treadmill_app.py
 - Then, on main computer browse to http://10.16.81.61:5010

### Tearing down treadmill

1. IMPORTANT: Do this first. Unplug 12v power from rat-nest
2. Unplug 2x ethernet from stage
     IMPORTANT: ALways check that 12V ac/dc is unplugged before unplugging red ethernet cable
3. Unplug BNC cables
4. Unplug usb video cable


### Fiji

#### Loading line scans

Load line scan with 'Plugins - Bio-Formats - Bio-Formats Importer and select .xml file in line scan folder



### SOCKIT Igor Pro Extension

SOCKIT is an Igor Pro extension allowing Igor Pro to talk to other applications.

SOCKIT is used by Igor Pro to talk to Prairie view

   the Prairie Canvas uses SOCKIT to
      (1) Set file paths in Prairie view
      (2) Get the objective position from Prairie View
      (3) Move the objective with Prairie View

Install socket for Igor 6 using
   SOCKIT-IGOR.5.00.x-1.x-dev/SOCKIT/win/SOCKITInstaller.exe

### Have Prairie View send REST command to treadmill webserver

This will only work if 'after scan' is specified in 'misc' tab of prairie view ???

Have Prairie View send rest command with name of file to treadmill web server. Prairie View sends tis at start of scan. Assuming treadmill is master, a trial is running on treadmill. Treadmill notes this prairie file and saves it with other stuff in .txt at end of trial. Offline we can then load a treadmill trial .txt file and know which prairie view file (folder) to associate with it.


 - install curl on windows

    https://help.zendesk.com/hc/en-us/articles/229136847-Installing-and-using-cURL#curl_win

 - write script that takes a param and send rest call

    http:<treadmill_ip>:5010/newprairiefile/<filename>

Where filename is the name of a new prairie file when we start scanning.


### Video camera to image surface vasculature

#### New camera for surface plus IOS imaging

DMK 33UX174 (5710179)

1/1.2 inch Sony CMOS Pregius sensor (IMX174LL), 

1,920◊1,200 (2.3 MP), up to 162 fps

https://www.theimagingsource.com/products/industrial-cameras/usb-3.0-monochrome/dmk33ux174/

Use IC Capture 2.4 to view live video feed

IC Capture is using 'Y800 (1920x1080)'

download drivers from:

https://www.theimagingsource.com/support/downloads-for-windows/device-drivers/icwdmuvccamtis33u/

windows driver is 'Cam33U_setup_4.1.0.1211.exe'

#### Old Camera

sony xc-st30, 1/3" CCD B/W Camera, EIA, $637

https://pro.sony.com/bbsc/ssr/product-XCST30/

#### Comparing sensor sizes

Accorind to wikipedia: https://en.wikipedia.org/wiki/Image_sensor_format

1/3", width:4.8, height: 3.6, diagonal: 6.0
1/1.2", width:10.67, height: 8.00, diagonal: 13.33

### Anaconda Python 2.7

Installed Python via Anaconda and am trying to get opencv to show a video feed

following this:

https://chrisconlan.com/installing-python-opencv-3-windows/



### Matlab video

Must run in matlab 2013b (desktop shortcut)

run custom .m file, f:\cudmore\matlabVideo\bCapture.m

I have added this path to matlab 2013b: f:\cudmore\matlabVideo

This will save an image every 0.5 seconds into f:\cudmore\tmp\myfirstimage.tif

Igor canvas can then load this
