# My set-up

## Drone

I use a standard X500 kit from Holybro. It has a PX4 autopilot, and a RPi 4 on-board computer
as a MAVLINK bridge


## Camera

GoPro HERO 9 Black, no gimbal yet.
This camera sends a preview over WiFi. I have not yet found out how to get that stream, as
all online examples fails. Maybe this live feed has a new URL on this camera? Maybe it is no longer
a RTSP feed? I have to figure this out
But, plugging the camera to your RPi using USB plug is your friend. You can put the camera on
"webcam mode" and get the live stream from UDP://172.x.x.51:8445

## GCS

QGroundControl on a Samsung Tab 10" connected to a XBox Elite 2 Bluetooth controller for manualy controlling the drone
QGC can show live RTSP feed, and hopefully the GPH9B can provide it


## Radio

The radiolink between the GCS and the drone is WiFi based. I have also connected a DSMX radio from Spektrum so the drone 
could be controlled by a regular spektrum radio. The spektrum set-up does not allow waypoint navigation
as it is a pure manual control solution.

It would also be possible to use a LTE module (USB stick, or M2?) on the drone and
use the LTE network as radio link. This would introduce a lot more delay, since the network packet roundtrip
in such an environment is higher than WiFi. But it would allow BVLOS missions (if you are a certified BVLOS pilot)

One caveat on the LTE link: Most operators use NAT to minimize the use of public IP addresses 
assigned to clients. This would in worst-case give you a NAT on NAT -> NAT on NAT if you use
SIM cards from the same operator in both the Tablet and LTE module on the drone.
This would NOT fly at all. Don't even try it.
In such a case you need both SIM cards to transmit commands via a publicly reachable proxy service.
I might create such a proxy later, but right now WiFi/DSMX is good enough for me.
