# Spotify-Carthing-Jailbrake my Windows Hacking Tutorial
I just got my Car Thing few days ago, and after sevral hours trail and error, I managed to jailbroken it.

You can enjoy Cathing without premium subscribe account, go through your playlists, but there still be advertisemet and skip limitations, and you can't cancel shuffle mode or rewind to last song.

Here is how I did it, and hope this tutorial can help someone out.

# [This is just my procedure to jailbrake, DO IT ON YOUR OWN RISK]
# [DO NOT RELY SOLELY ON THIS TUTORIAL, USE COMMON SENSE]



## Thanks to bishopdynamics for superbird-tool
## Thanks to lmore377 for jailbrake firmware
## Thanks to williamtcastro for carthing-non-premium-spotify webapp



What you need:

A PC running Windows. (I'm using Windows 10 X64 Home Edition 21H2)
A USB-A or USB-C to USB-C cable
Some code from github
USB driver from Zadig
ADB tool
Python



## STEP 1. PREPARE THE ENVIROMENT AND JAILBRAKE FIRMWARE

Download and install ADB tool, link and some instructions are here: `https://www.xda-developers.com/install-adb-windows-macos-linux/`, see How to set up ADB on Microsoft Windows part

Download Python from `https://www.python.org/downloads/` (I'm using 3.10.8), after install google "add python to path" and follow the instructions.

Download Git for windows from `https://github.com/git-for-windows/git/releases/`, version should not matters, just download [Git-2.XX.X-64-bit.exe ].

Download Superbird Tool from `https://github.com/bishopdynamics/superbird-tool`, on the top of the page, a GREEN BUTTON says CODE, hit it and then the DOWNLOAD ZIP. Extract files to [C:\carthing\superbird-tool] for easy access.

Download JAILBRAKE Firmware from `https://github.com/err4o4/spotify-car-thing-reverse-engineering/issues/22` on first repo. Or direct access MEGA file from `https://mega.nz/folder/NxNXQCaT#-n1zkoXsJuw-5rQ-ZYzRJw`. Choose a firmware dump inclued ADB ENABLED. Extract files to [C:\carthing\latest_fw_with_adb] for easy access.

Download Non Premium webapp from `https://github.com/williamtcastro/carthing-non-premium-spotify`, procedure is same with 4. Extract files to [C:\carthing\carthing-non-premium-spotify] for easy access.

Download Zadig from `https://zadig.akeo.ie/` and install.



## STEP 2. FLASH THE JAILBRAKE FIRMWARE

Connect your carthing to computer while press button 1&4, go to your device manager, there shold be a unknown device called GX-CHIP. Luanch Zadig and install/replace the USB driver to libusbK.

Go to `C:\carthing\latest_fw_with_adb\`, change the settings.`dump` file suffix to settings.`ext4` and system_a.`dump` to system_a.`ext2` , system_b.`dump` to system_b.`ext2`, data.`dump` to data.`ext4`

Hit Windows+R and iput cmd or search cmd, go in to command line.


run these command for download another tool from Github

`python -m pip install git+https://github.com/superna9999/pyamlboot`

if failed try

`python -m pip install git+https://github.com/superna9999/pyamlboot.git`


then

`cd C:\carthing\superbird-tool`

`python ./superbird_tool.py`

After this step you shold see some instructions from command line, if not check your python or the file path.



`python ./superbird_tool.py --find_device`

check that Carthing is connected and is in usb mode, you should see USB MODE



`python ./superbird_tool.py --enable_burn_mode`

Carthing will auto reboot and reconnect to computer



`python ./superbird_tool.py --find_device`

check connectivity again and make sure it is in USB BURN MODE


`python ./superbird_tool.py --disable_avb2 A`

disable A/B, lock to A


`python ./superbird_tool.py --restore_device C:\carthing\latest_fw_with_adb`

Load jailbrake firmware to Cathing, This step will take some time, as long as the program is running, no worries. After finish, disconnect and reconnect Carthing to computer while push button 4.





## STEP 3. Enable Spotify non-premium account


`python ./superbird_tool.py --find_device`

Check connectivity and make sure it is in USB BURN MODE, if not, run command

`python ./superbird_tool.py --enable_burn_mode`

and this command again to check



`python ./superbird_tool.py --boot_adb_kernel A``

`adb devices`

Boot to ADB mode and check device, you shold see something like


List of devices attached

123456 device



`cd C:\carthing\carthing-non-premium-spotify`

`adb shell mount -o remount,rw /`

Enable carthing to write files


`adb push settings/onboarding_status /var/lib/qt-superbird-app/settings`

`adb push settings/setup_state /var/lib/qt-superbird-app/settings`

Setup carthing without need the phone app



`adb shell mv /usr/share/qt-superbird-app/webapp /usr/share/qt-superbird-app/webapp-orig`

Save the original app



`adb push webapp /usr/share/qt-superbird-app/`

Send the new Non-premium webapp to Carthing



`adb shell ls /usr/share/qt-superbird-app/`

Check the webapp is in correct location, you shold see a folder called `/webapp`. If not, run

`adb push webapp /usr/share/qt-superbird-app/webapp`

and check it again.




`adb shell reboot`

Reboot and re-pair your phone bluetooth.



Viola, you get a JAILBROKEN PREMIUM-FREE Carthing. Enjoy.
