# My set-up

## Drone

I use a standard X500 kit from Holybro. It has a PX4 autopilot, and a RPi 4 on-board computer
as a MAVLINK bridge


## Camera

GoPro HERO 9 Black, no gimbal yet

## GCS

QGroundControl on a Samsung Tab 10" connected to a XBox Elite 2 Bluetooth controller for manualy controlling the drone


## Radio

The radiolink between the GCS and the drone is WiFi based. I have also connected a DSMX radio from Spektrum so the drone 
could be controlled by a regular spektrum radio. The spektrum set-up does not allow waypoint navigation
as it is a pure manual control solution.

It would also be possible to use a LTE module (USB stick, or M2?) on the drone and
use the LTE network as radio link. This would introduce a lot more delay, since the network packet roundtrip
in such an environment is higher than WiFi. But it would allow BVLOS missions (if you are a certified BVLOS pilot)

