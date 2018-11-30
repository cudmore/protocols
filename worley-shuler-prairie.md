### Startup software

 1. Prairie View : To scan 2p images
 2. Prairie Canvas (Igor Pro) : To construct a canvas of video and 2p images
 3. Putty : To login to Raspberry Pi treadmill
 4. VirtualDub : To view a live video feed from Raspberry Pi camera. Turn on video feed with 'File - Capture AVI'
 5. Matlab : To view real-time feed of scope video camera and import into Pririe Canvas
 6. Web browser to control treadmill
 
### Raw data from Prairie

Raw data shoud be saved in following locations. When you set a 'session id' in the  Igor Prairie Canvas, these are set automatically (if Prairie View is running).

    f:\cudmore\data

It is important that Prairie View saves files to a solid-state drive. If saving to a triditional psinning-disk drive there may be image corruption.

### To Do
 - Hook up dimmer to treadmill green led
 - Hook up on/off switch to treadmill ir
 - [done] Get 4-8 port powered usb box. We are running out of usb ports
 - Get 2x backup motor driver borads, first look up to see if there is a new version
 - Make Igor Prairie Canvas finalize when canvas is closed (Ask user and default to yet).
    on click 'session id', check if there is an existing canvas open and warn
    this will work real sweet without really changing code


### Running Prairie Canvas
 - Open PrairieCanvas.ipf (desktop shortcut). Should open in Igor Pro 7
 - Click on empty command window to activate menus
 - Select menu 'Canvas - Load User' and select 'cudmore_prairie.txt' file.
 - Each time you mount a new mouse, set a new 'session id'
 - When your finished with an imaging session, click 'Finalize and Clear Canvas'

Prairie user configurations are in the main Map Manager folder at 'F:\cudmore:apps:bJHU:MapManager_Options:Users:scope:cudmore_prairie.txt'.

### Hooking up treadmill

 1. 3x BNC should be plugged in to Prairie BNC breakout
    - **Trig 1 In**, first (left) on treadmill rat-nest. Purpose: Allow treadmill to trigger Prairie View
    - **PCI-6052E AI0**, there is a t-splitter, second (middle) on treadmill rat-nest. Purpose: Allow Prairie View to record the frame clock which passes through Treadmill
    - **PCI-6052E AI1**, third (right) on treadmill rat-nest. Purpose: Allow Prairie View to record status of motor

2. 2x ethernet cables
    - 1st, red, motor, red
    - 2nd, green, ir led and encoder (encoder not used)

3. 1x USB dongle
    - USB dongle from rats-nest to usb port on computer. Purpose: View video feed from camera on computer with Virtual Dub

4. IMPORTANT: DO this last. Plug in 12v ac/dc on rat-nest
    Purpose: This is motor and ir led power.
    If motor cable (red ethernet) is unplugged while 12v is plugged, will burn motor board
    Always check that motor (red ethernet) is plugged in before pluggin in 12v ac/dc

### Starting treadmill software
Login to pi using putty software

```
ip: 10.16.81.61
user: pi
password: <ask bob>
```

At the command prompt, type

```
cd Sites/treadmill
python treadmill_app.py
```

Then, on main computer, browse to http://10.16.81.61:5010

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

SOCKIT is an Igor Pro extension allowing Igor Pro to talk to other applications. The Igor Prairie Canvas uses SOCKIT to talk to Prairie view to do the following:

 1. Set file paths and names in Prairie view
 2. Get the objective position from Prairie View
 3. Move the objective with Prairie View

Install socket for Igor 6 using

	SOCKIT-IGOR.5.00.x-1.x-dev/SOCKIT/win/SOCKITInstaller.exe

### Have Prairie View send REST command to treadmill webserver

This will only work if 'after scan' is specified in 'misc' tab of Prairie View.

Have Prairie View send rest command with name of file to treadmill web server. Prairie View sends this at start of scan. Assuming treadmill is master, and a trial is running on treadmill. Treadmill saves the Prairie View file name (and many other things) in a .txt file at end of trial. Offline we can then load a treadmill trial .txt file and know which prairie view file (folder) to associate with it.


This system requires 'curl' to be installed on Windows system

    https://help.zendesk.com/hc/en-us/articles/229136847-Installing-and-using-cURL#curl_win

todo: give an example of my dos batch file that actually does this.

Once configured, prairie view triggers the dos batch file which uses curl to send a web request (with the file name) to the treadmill:

    http:<treadmill_ip>:5010/newprairiefile/<filename>

Where <filename> is the name of the new prairie view file we scanned.


### Video camera to image surface vasculature

#### New camera for surface plus IOS imaging

DMK 33UX174 (5710179)

1/1.2 inch Sony CMOS Pregius sensor (IMX174LL), 

1,920x1,200 (2.3 MP), up to 162 fps

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

### Building issues (e.g. cooling)


This is part of the building and should be non-chargeable.  This email address is only set up for M&S (billable) work.  All regular maintenance issues are more quickly handled thru Customer Service @ 5-3323, they are available 24/7. If there is aproblem with building (usually cooling), do not email facworkrequest@jhmi.edu but call instead.
