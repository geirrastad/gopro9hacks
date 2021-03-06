# Enable WiFi

Easiest: Use GoPro App

This howto is for people who would like to connect a gopro h9b to a drone for streaming
live video to QGroundGrontrol (or other GCS capable of RTSP video feed)


## Enable WiFi from linux (debian based)

Out of the box GoPro has neither Bluetooth nor WiFi enabled. This is a security mechanism so no hacker can pwn it.
The first step is therefore to pair your GoPro with the GoPro app. NOTE: If you, as I, HATE all products where you need to register on some company web site to use their product, you don't need to do it with GoPro. Then shove the "login" and "register" up your face, but simply click the small camera icon in the top right corner of the GoPro app.

As soon as the app is paired with your cam BT is enabled, and can be utilized.

TODO: Figure out how to do this without the GP app

Also, the examples are only tested on Raspberry Pi with Raspbian OS and Ubuntu 20.10. It might work with other distros.

## Pairing and connecting the camera

NOTE: You need a working bluetooth and wifi stack for this to work. Both Raspbian OS and Ubuntu 20.10 installes this 
with their default installs.

If you scan bluetooth devices, you will notice a GoPro xxx device in the list. This was created in the app pairing process,
but it cannot be used as is. It will not connect or pair, just fail with an "AuthenticationFailed" message.

To pair do the following:

```
sudo bluetoothctl
```

Make sure it prints out "agent on". If not issue the command:

```
agent on
```

Now start scanning for devices:
```
scan on
```

At this point you will see the "GoPro xxx" device. Take a note of the device address,
it should start with "FA:15:" for a GoPro 9

run:
```
trust FA:15:xx:xx:xx:xx
```

Now go to your camera and select the Connections menu. Then press "Connect Device"
and select "Remote"

The device is now in discovery mode, and the output from scan should notify you of a change
It could read something like:
```
[CHG] Device FA:15:7A:xx:xx:xx ServicesResolved: no
[CHG] Device FA:15:7A:xx:xx:xx Connected: no
```

Now it is time to connect and pair:
```
connect FA:15:7A:xx:xx:xx
```

You should then see
```
Attempting to connect to FA:15:7A:6E:23:60
[CHG] Device FA:15:7A:6E:23:60 Connected: yes
Connection successful
```

Then pair it:
```
pair FA:15:7A:xx:xx:xx
```

Please answer yes to this:
```
[agent] Accept pairing (yes/no):
```

The device should now be paired and redy to use.
issue "disconnect" then exit the bluetoothctl

## Enabling WiFi

After pairing bluetooth, it's time to enable WiFi.
gattool is your friend:
```
sudo gattool -t random -b FA:15:7A:xx:xx:xx -I
```

You will now get a gattool prompt. Type
```
connect FA:15:7A:xx:xx:xx
```

If connection is successful:
```
char-write-req 33 03170101
```
NOTE: Some GoPro examples uses 2f insted of 33, that is for previous versions of GoPro HERO. The #9 requires 33

WiFi is now enabled, and you should see a "GPxxxxxxx" SSID being broadcast

## Connect WiFi

If you're using a GUI just connect to the "GPxxxxxxx" AP lik you would connect to any other WiFi network.

The password is found in the camera menu: Connections->Camera Info

To manually connect on a headless RPi or similar you must edit the 
/etc/wpa_supplicant/wpa_supplicant.conf file and add this in the bottom of the file:
```
network={
	ssid="GPxxxxxxxx"
	psk="<the-cam-pwd>"
}
```

If the file doesn't exist on  a RPi, you must run the raspi-config and enable WiFi. 
You might as well use that tool to connect to the GoPro.

To bring the WiFi up run this command:
```
wpa_cli -i wlan0 reconfigure
```

Wait..... et voila, you should have a wlan0 interface with an IP address of 10.5.5.x (probably .100)
