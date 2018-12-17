# Worley-Shuler Prairie/Bruker Scope Readme

## Power up the scope

 - Turn on the big white switch on right-hand side of rack.
 - Turn on the computer using button on top of computer case.

## Power down the scope

 - Shutdown the computer.
 - Turn off the big white switch on right-hand side of rack.
 
## Startup software

 1. Prairie View : To scan 2p images
 2. Prairie Canvas (Igor Pro) : To construct a canvas of video and 2p images
 3. bCapture.m (Matlab) : To view real-time feed of scope video camera and import into Prairie Canvas
 4. Putty : To login to Raspberry Pi treadmill
 5. VirtualDub : To view a live video feed from Raspberry Pi camera
 6. Web browser to control treadmill

## Hooking up treadmill

The order is**CRITICAL**. Attach the red/green ethernet and then plug-in the 12v AC/DC. Never have the 12v AC/DC plugged in without having the ethernet plugged in. If 12v AC/DC is plugged in without ethernet, the motor controller board will be permanently damaged and no longer function. This is the way the [Easy Driver](https://www.sparkfun.com/products/12779) motor controller works, sorry.

1. Attach red/male/motor ethernet cable to female/motor ethernet on the treadmill imaging platform
2. Attach green/male/led ethernet cable to female/led ethernet on the treadmill imaging platform
3. Plug in the 12v AC/DC adapter near the Raspberry Pi. **IMPORTANT**. Only plug this in after the ethernet is attached.

## Tearing down the treadmill

The order is**CRITICAL**. Un-plug the 12v AC/DC and then unplug the red/green ethernet. Never have the 12v AC/DC plugged in without having the ethernet plugged in. If 12v AC/DC is plugged in without ethernet, the motor controller board will be permanently damaged and no longer function. This is the way the [Easy Driver](https://www.sparkfun.com/products/12779) motor controller works, sorry.

1. Unplug the 12v AC/DC adapter near the raspberry Pi. **Important**. Always unplug 12v AC/DC BEFORE you unplug ethernet.
2. Unplug both red/motor and green/led ethernet cables from the treadmill imaging platform.

## One time hookup of Raspberry Pi (treadmill computer system) to scope and main Prairie View imaging computer

1. 3x BNC should be plugged in to Prairie BNC breakout
    - **Trig 1 In**, first (left) on treadmill rat-nest. Purpose: Allow treadmill to trigger Prairie View
    - **PCI-6052E AI0**, there is a t-splitter, second (middle) on treadmill rat-nest. Purpose: Allow Prairie View to record the frame clock which passes through Treadmill
    - **PCI-6052E AI1**, third (right) on treadmill rat-nest. Purpose: Allow Prairie View to record status of motor

2. 1x USB dongle
    - USB dongle from rats-nest to usb port on computer. Purpose: View video feed from camera on computer with Virtual Dub

## 1) Running Prairie View

The Prairie View software is in 'C:\Program Files\Prairie\Prairie View\Prairie View.exe'.

Turn on the laser and open the shutter in the '2-P Laser' tab.

## 2) Running Prairie Canvas

 - Open PrairieCanvas.ipf (desktop shortcut). Should open in Igor Pro 7. The original file is in 'F:\cudmore\apps\bJHU\PrairieCanvas.ipf'.
 - Click on empty command window to activate menus
 - Select menu 'Canvas - Load User' and select 'cudmore_prairie.txt' file.
 - Ensure you can read Prairie View motor position with 'Read Position'. When this is working, the motor position will be filled in and the button will be green. Do not proceed until this works. If it fails, go to Prairie View and move the objective lef or right (with arrow buttons) and then try to 'Read Position' from the Prairie Canvas again.
 - Enter a 'Session ID' and click 'Initialize session'. This will bring up a canvas where both video snapshots and 2p images will be imported. There is no explicit 'save canvas', the canvas is saved each time either video and/or 2p stacks are imported. Each time you mount a new mouse on the scope, set a new 'session id'. If you mount the same mouse twice in one day, append 'a', 'b', 'c' to the session id.
 - When your finished with an imaging session, click 'Finalize and Clear mp285 Canvas'

Prairie user configurations specify user defaults including the save path and are in the main Map Manager folder at 'F:\cudmore:apps:bJHU:MapManager_Options:Users:scope:cudmore_prairie.txt'.

**Important**. When you click 'Initialize Session', ensure both the save path and file names are set correctly in Prairie View. Verify this for both the Prairie View Z-Series and T-Series tab. If one of them is correct, the others should also be correct.

### Saving files

Prairie View and the Prairie Canvas need to save files to the same folder. This is controlled from within the Prairie Canvas. When you set a 'session id' in the Prairie Canvas, folders for todays date (yyyymmdd) and the session (yymmdd_sesisonid) are created. This path is automatically set within Prairie View (assuming it is running).

    e:\cudmore\data

It is important that Prairie View saves files to a solid-state drive. If saving to a traditional spinning-disk drive there may be image corruption.

## 3) Matlab video with bCapture

Open bCapture.m found in 'f:\cudmore\matlabVideo\bCapture.m' and type 'bCapture' at the Matlab command prompt.

The bCapture script will open a live feed of the video camera (the one on top of the scope) and will save an average image (taken from 3 snapshots) every 0.2 seconds into 'f:\cudmore\tmp\myfirstimage.tif'. Igor canvas can then load this video image into a canvas. The Igor Canvas assumes it will find the saved video snapshots in this folder, if you change the save folder in the Matlab script, you need to change the code in Igor.

**Important** The USB3 camera on top of the scope needs to be plugged into the back of the computer where the USB ports have enough power. The USB plugs on the top/front of the computer do not have enough power for the camera. The symptom is that the camera (and matlab) will randomly lose the camera and when it does it is really annnoying.

**Important** Now that the usb3 camera on top of the scope is plugged into the back of the computer, it needs to be unplugged on top of the scope.

**Important**. If the live vido feed fails, you need to close the window and reopen it by typing 'bCapture' at Matlab command prompt. If this still does not work, unplug the camera USB, reinsert USB and try again. When the live video fails you can visually see this as the specle noise of the video will stop being noticeable.

**If someone wants to be a good colleague, I would appreciate some troubleshooting. Is it the Matlab script that looses the camera? Is it the USB power? Is it the install Windows 7 drivers that came with the camera?**

### Matlab video detials

 - Must run in Matlab 2013b (desktop shortcut)
 - I have added this path to Matlab 2013b: f:\cudmore\matlabVideo


## 4) Starting treadmill software (use putty to login)

Login to the Treadmill Raspberry Pi using putty software (use ssh port 22). The putty software is at 'F:\cudmore\apps\putty.exe' and is preconfigured with a saved session named 'treadmill' to login to the Treadmill Raspberry Pi.

```
ip: 10.16.81.61
user: pi
password: <ask bob>
```

At the Treadmill Raspberry Pi command prompt, type

```
cd Sites/treadmill
python treadmill_app.py
```

Then, on main computer, browse to http://10.16.81.61:5010

Make sure you include port 5010 in the address with ':5010'. Once the web interface is opened in a browser, it is easy enough to make a bookmark to return to it in the future.

## 5) VirtualDub

VirtualDub is a program to play video files and display a live video feed from a USB video camera. The VirtualDub program is at 'F:\cudmore\apps\VirtualDub-1.10.4\VirtualDub.exe'.

Open VirtualDub and start a live video feed using 'File - Capture AVI...' and select the correct USB camera with 'Select a Video Device' popup. This is usually 'USB2.0 ATV'.

The video feed will only work if

 - The Raspberry Pi (output headphone jack) is connected to an analog video to USB converter.
 - The Raspberry Pi is running the treadmill software.
 
# Using the scope hardware

## Switching between video and 2p light path

 - **video**. Turn top nob all the way to the back (clockwise if looking at it from side of scope) and set Olympus style filter wheel to position '2'.
 - **2p**. Turn the top knowb all the way towards you (counter clockwise if looking at it from side of scope) and set the Olympus style filter wheel to position '1'.
 - In both cases, ensure the light path slider is all the way out (camera position).
 - In both cases, ensure the 'shutter' switch is closed (in the dark circle position).

## GAsP detectors

 - The GAsP detectors have a control box directly below the main computer keyboard. There are lots of switches and 1-2 dials. The only thing I do is ensure the detectors are on using the vertical toggle switch 'PMT Power On/Off'.
 - If the detectors every receive too much light, an audible (and annoying) alarm will go off. Silence the alarm by cycling the detector power off then on again. Be sure to reduce your laser power and/or detector gain a bit if this happens repeatedly.
 
## Pockels Cell

The Pockels cell controller is above the monitor. IT is a box labeled 'conoptics model 302RM'. Ensure this is powered on.

# Acquiring images with Prairie View

This is beyond the scope of this recipe. You are on your own.

## Turning the laser on/off with Prairie View

 - Turn on laser in '2-P Laser' tab
 - Open the laser shutter in '2-P Laser' tab
 - **Important**. At the end of imaging, be sure to turn off the 2P laser (using '2-P Laser' tab) before exiting Prairie View software. When the laser is on, the soft white light on top of the actual laser box (behind the scope) will be on. Always check this to verify you have turned off the laser. If you forget to turn off the laser, you need to run Prairie View again and turn it off in the '2-P Laser' tab.

## Prairie View considerations

 - If you want to set laser power as a function of depth, make sure 'Adjust PMT & Laser' is checked before setting the Start/Stop position. This option is always off when Prairie View is first run. Do not try to turn this on in the middle of setting the start/stop z-plane.
 - After each Z-Stack, be sure to press Start Position 'Goto' to set the laser power to that of the actual start posiiton. At the end of a Z-Stack acquisition, the objective is moved back to the 'start position' but if using 'Adjust PMT & Laser', the laser power is left at its 'stop position' value.
 - If triggering Prairie View as a slave from the Treadmill web interface, ensure 'Start with input trigger' is checked and press 'Start T-Series'. Prairie view will then wait for an imput trigger that is sent by the treadmill when 'Start Trial' is pressed in the web interface.
 - Remember to turn off the laser before quiting Prairie View. Always check the laser is off by looking for the white light on the top of the laser box behind the scope.
 - Remember to check the 'Optical Zoom [mag]' when switching between 'Galvo' and 'Resonant Galvo' scanning. They are independent for each mode and do not always switch back to the last value.
 - By default, Prairie View saves files in an intermediate (raw) format that is not Tif. You need to choose if you want to convert the intermediate Prairie View format to Tif at the end of each aquisition or manually in batch mode using the 'Image Block Ripping Utility'. In general, automatic conversion at the end of acquisition works well for a small number of images like with a Z-Stack but not for longer/larger time-series (e.g. 1800 frames). The longer/larger time series conversion takes longer than the time it took to acquire the images! This option is set in Prairie View using the main menu 'Preferences - Automatically Convert Raw Files', and choosing either 'Never (Use Image-Block Ripping Utility)' or 'After Aquisition'.
 
To use the 'Image-Block Ripping Utility', run it, click 'Browse..' button and select a folder with Prairie View files, turn on 'Include Sub-folders' checkbox and start conversion with 'Start Conversion ' button.
 
 
## Loading stacks and time-series acquired with Prairie View

Prairie View saves all acquired images in individual Tiff files, it does not ever save a single Tiff stack or time-series. In addition, Prairie View saves all acquisition parameters into an xml file.

### Loading Prairie View images into the Prairie Canvas

The Prairie Canvas will automatically load native Prairie View files with no conversion needed. This can be done while imaging on the Prairie/Bruker scope and offline using Map Manager on any analysis machine.

### Loading Prairie View images in other programs

Drag and drop the Prairie View xml file onto Fiji and if your lucky it will open as a single image Tiff stack.

Alternatively, see [bPrairie2Tif](https://github.com/cudmore/bob-fiji-plugins/blob/master/bPrairie2tif.v0.0_.py) for a script to convert individual Tiff files saved by Prarie View into single Tiff files. This will work for both z-stacks and for time-series images. This script converts Prairie View images into a format that can be loaded into the Prairie Canvas or offline into Map Manager. One added bonus is this automatically sets the voxel size by reading the Prairie View xml acquisition parameters.

# Troubleshooting

If you don't get a two-photon image

 - Is the laser on, the shutter open, and the wavelength set to 920 for GFP? Check Prairie View '2-P Laser' tab.
 - Is the Prairie View laser power and PMT gains set properly? Check the Prairie View 'Power/Gain' tab and ensure the Pockels has power (surface is 160-220, may is ~460) and the Red/Green PMT have gain, somewhere between 575-610.
 - Is the light path on the scope set to 2p mode? Ensure top black knob is all the way to the front (counter-clockwise while looking at scope from right) and the olympus filter turret is in position '1'.
 - Are the PMT's power on? Check the pmt power switch on the 'GaAsP detector control box' (below keyboard).
 - Is prairie view displaying the color channel you are interested in? Check the color buttons in the Prairie View 'Image Window - 1' and 'Image Window - 2'.
 - Is the Pockels cell on? Ensure the 'conoptics model 302RM' box is on (above monitor).
 - Is your focus within an area you would expect to excite some fluorophore?
 - Is the objective still submerged in water? Visually check this.
 
 
# Hardware details

## Video camera to image surface vasculature (on top of the scope)

### New camera

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


# Building/Room issues (e.g. cooling)

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

This will only work if 'after scan' is set to 'bob_eos' in Prairie View. See 'Mic Tab - Actions To Perform - After Scan.

'bob_eos' is a Windows batch file with the following

```
```

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


