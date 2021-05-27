# Robot Networking

Under normal conditions, IPs of networked robot hardware reside in the 10.65.2.x range as assigned by the [RoboRIO](roborio.md) DHCP server. These IPs can also be assigned statically, which can significantly improve startup and connection times. However, if static addresses are used, *every* device on the robot's network, including the driver station, must have a static IP set.


!!! info "More Information"
    [WPILib](https://docs.wpilib.org/en/stable/docs/networking/networking-introduction/index.html) has much more detailed information on robot networking and how it interacts with the field and driver station.