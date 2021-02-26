# GoPro 9 hacks

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

Now go to your camera and select the Connections menu. Then press "Connect Device"
and select "Remote"

The device is now in discovery mode, and the output from scan should notify you of a change
([CHG]) o




