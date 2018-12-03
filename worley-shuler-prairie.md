# Worley-Shuler Prairie/Bruker Scope Readme

## Power up the system

Use the big white switch on right-hand side of rack.

## Startup software

 1. Prairie View : To scan 2p images
 2. Prairie Canvas (Igor Pro) : To construct a canvas of video and 2p images
 3. Putty : To login to Raspberry Pi treadmill
 4. VirtualDub : To view a live video feed from Raspberry Pi camera. Turn on video feed with 'File - Capture AVI'
 5. bCapture.m (Matlab) : To view real-time feed of scope video camera and import into Prairie Canvas
 6. Web browser to control treadmill
 
## Raw data from Prairie

Prairie View and the Prairie Canvas need to save files to the same folder. When you set a 'session id' in the Prairie Canvas, this is automatically set in Prairie View (assuming Prairie View program is running).

    f:\cudmore\data

It is important that Prairie View saves files to a solid-state drive. If saving to a traditional spinning-disk drive there may be image corruption.

## Running Prairie Canvas

 - Open PrairieCanvas.ipf (desktop shortcut). Should open in Igor Pro 7
 - Click on empty command window to activate menus
 - Select menu 'Canvas - Load User' and select 'cudmore_prairie.txt' file.
 - Ensure you can read Prairie View motor position with 'Read Position'. When this is working, the motor position will be filled in and the button will be green. Do not proceed until this works. If it fails, go to Prairie View and move the objective lef or right (with arrow buttons) and then try to 'Read Position' from the Prairie Canvas again.
 - Enter a 'Session ID' and click 'Initialize session'. This will bring up a canvas where both video snapshots and 2p images will be imported. There is no explicit 'save canvas', the canvas is saved each time either video and/or 2p stacks are imported. Each time you mount a new mouse on the scope, set a new 'session id'. If you mount the same mouse twice in one day, append 'a', 'b', 'c' to the session id.
 - When your finished with an imaging session, click 'Finalize and Clear mp285 Canvas'

Prairie user configurations specify user defaults including the save path and are in the main Map Manager folder at 'F:\cudmore:apps:bJHU:MapManager_Options:Users:scope:cudmore_prairie.txt'.

**Important**. When you click 'Initialize Session', ensure both the save path and file names are set correctly in Prairie View. Verify this for both the Z-Series and T-Series tab. If one of them is correct, the others should also be correct.

## Matlab video

Run bCapture.m found in f:\cudmore\matlabVideo\bCapture.m

This script will open a live feed of the video camera on top of the scope and will save an average image (taken from 3 snapshots) every 0.2 seconds into 'f:\cudmore\tmp\myfirstimage.tif'. Igor canvas can then load this video image into a canvas

**Important**. If the live vido feed fails, you need to close the window and reopen it by typing bCapture at Matlab command prompt. If this still does not work, unplug the camera USB, reinsert USB and try again. When the live video fails you can visually see this as the specle noise of the video will stop being noticeable.

### Matlab video detials

 - Must run in matlab 2013b (desktop shortcut)
 - I have added this path to matlab 2013b: f:\cudmore\matlabVideo

## Hooking up treadmill

1. Attach red/male/motor ethernet cable to female/motor ethernet on the treadmill imaging platform
2. Attach green/male/led ethernet cable to female/led ethernet on the treadmill imaging platform
3. Plug in the 12v AC/DC adapter near the Raspberry Pi. **IMPORTANT**. Only plug this in after the ethernet is attached.

## Tearing down the treadmill

1. Unplug the 12v AC/DC adapter near the raspberry Pi. **Important**. Always unplug 12v AC/DC BEFORE you unplug ethernet.
2. Unplug both red/motor and green/led ethernet cables from the treadmill imaging platform.

## One time hookup of Raspberry Pi (treadmill computer system) to scope and main Prairie View imaging computer

1. 3x BNC should be plugged in to Prairie BNC breakout
    - **Trig 1 In**, first (left) on treadmill rat-nest. Purpose: Allow treadmill to trigger Prairie View
    - **PCI-6052E AI0**, there is a t-splitter, second (middle) on treadmill rat-nest. Purpose: Allow Prairie View to record the frame clock which passes through Treadmill
    - **PCI-6052E AI1**, third (right) on treadmill rat-nest. Purpose: Allow Prairie View to record status of motor

2. 1x USB dongle
    - USB dongle from rats-nest to usb port on computer. Purpose: View video feed from camera on computer with Virtual Dub

## Starting treadmill software

Login to pi using putty software (use ssh port 22)

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

## VirtualDub

VirtualDub is a program to play video files and display a live video feed from a USB video camera. Once VirtualDub is opened, start a live video feed using 'File - Capture AVI...' and select the correct USB camera with 'Select a Video Device' popup. This is usually 'USB2.0 ATV'.

The video feed will only work if

 - The Raspberry Pi (output headphone jack) is connected to an analog video to USB converter.
 - The Raspberry Pi is running the treadmill software.
 
# Acquiring images with Prairie View

This is beyond the scope of this recipe. You are on your own.

## Turning the laser on/off with Prairie View

 - Turn on laser in '2-P Laser' tab
 - Open the laser shutter in '2-P Laser' tab
 - **Important**. At the end of imaging, be sure to turn off the 2P laser (using '2-P Laser' tab) before exiting Prairie View software. When the laser is on, the soft white light on top of the actual laser box (behind the scope) will be on. Always check this to verify you have turned off the laser. If you forget to turn off the laser, you need to run Prairie View again and turn it off in the '2-P Laser' tab.
 
## Fiji

Prairie View saves all acquired images in individual Tiff files, it does not ever save a single Tiff stack. Prairie View saves all acquisition parameters into an xml file.

### Loading image stacks and time-series

See [bPrairie2Tif](https://github.com/cudmore/bob-fiji-plugins/blob/master/bPrairie2tif.v0.0_.py) for a script to convert individual Tiff files saved by Prarie View into single Tiff stack Tiff. This script can be used to easily convert Prairie View images into a format that can easily be loaded into Map Manager for offline analysis.

Alternatively, in Fiji, drag and drop the Prairie View xml file and if your lucky it will open as a single image Tiff stack.

### Loading line scans

Load line scan with 'Plugins - Bio-Formats - Bio-Formats Importer and select .xml file in line scan folder



# Hardware details

## Video camera to image surface vasculature (on top of the scope)

### New camera for surface plus IOS imaging

DMK 33UX174 (5710179)

1/1.2 inch Sony CMOS Pregius sensor (IMX174LL), 

1,920x1,200 (2.3 MP), up to 162 fps

https://www.theimagingsource.com/products/industrial-cameras/usb-3.0-monochrome/dmk33ux174/

Use IC Capture 2.4 to view live video feed

IC Capture is using 'Y800 (1920x1080)'

download drivers from:

https://www.theimagingsource.com/support/downloads-for-windows/device-drivers/icwdmuvccamtis33u/

windows driver is 'Cam33U_setup_4.1.0.1211.exe'

### Old Camera

sony xc-st30, 1/3" CCD B/W Camera, EIA, $637

https://pro.sony.com/bbsc/ssr/product-XCST30/

### Comparing sensor sizes

According to wikipedia: https://en.wikipedia.org/wiki/Image_sensor_format

1/3", width:4.8, height: 3.6, diagonal: 6.0
1/1.2", width:10.67, height: 8.00, diagonal: 13.33


# Building issues (e.g. cooling)

This is part of the building and should be non-chargeable.  This email address is only set up for M&S (billable) work.  All regular maintenance issues are more quickly handled thru Customer Service @ 5-3323, they are available 24/7. If there is aproblem with building (usually cooling), do not email facworkrequest@jhmi.edu but call instead.

# Implementation details

## SOCKIT Igor Pro Extension

SOCKIT is an Igor Pro extension allowing Igor Pro to talk to other applications. The Igor Prairie Canvas uses SOCKIT to talk to Prairie view to do the following:

 1. Set file paths and names in Prairie view
 2. Get the objective position from Prairie View
 3. Move the objective with Prairie View

Install socket for Igor 6 using

	SOCKIT-IGOR.5.00.x-1.x-dev/SOCKIT/win/SOCKITInstaller.exe

## Have Prairie View send REST command to treadmill webserver

This will only work if 'after scan' is specified in 'misc' tab of Prairie View.

Have Prairie View send rest command with name of file to treadmill web server. Prairie View sends this at start of scan. Assuming treadmill is master, and a trial is running on treadmill. Treadmill saves the Prairie View file name (and many other things) in a .txt file at end of trial. Offline we can then load a treadmill trial .txt file and know which prairie view file (folder) to associate with it.


This system requires 'curl' to be installed on Windows system

    https://help.zendesk.com/hc/en-us/articles/229136847-Installing-and-using-cURL#curl_win

todo: give an example of my dos batch file that actually does this.

Once configured, prairie view triggers the dos batch file which uses curl to send a web request (with the file name) to the treadmill:

    http:<treadmill_ip>:5010/newprairiefile/<filename>

Where <filename> is the name of the new prairie view file we scanned.


## Anaconda Python 2.7

Installed Python via Anaconda and am trying to get opencv to show a video feed

following this:

https://chrisconlan.com/installing-python-opencv-3-windows/

# To Do
 - Hook up dimmer to treadmill green led
 - Hook up on/off switch to treadmill ir
 - [done] Get 4-8 port powered usb box. We are running out of usb ports
 - Get 2x backup motor driver borads, first look up to see if there is a new version
 - Make Igor Prairie Canvas finalize when canvas is closed (Ask user and default to yet).
    on click 'session id', check if there is an existing canvas open and warn
    this will work real sweet without really changing code


