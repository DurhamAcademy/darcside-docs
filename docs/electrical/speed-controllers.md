# Speed Controllers
!!! note
    This page is about the hardware/conceptual aspects of speed controllers. If you are looking for details on their usage in software, see /link/

Speed controllers (AKA ESCs, Electronic Speed Controllers, Motor Controllers, etc.) are one of the most important components involved in getting a robot moving. In short, they are responsible for converting software commands into actual motor activity.

## Brushed and Brushless
An important distinction in speed controllers is if they are designed for brushed or brushless motors due to their differing means of actuation. You can usually tell this from how many output wires a speed controller has. Something with red, white, and black wires coming out of one side is designed for brushless, while just red and black is for brushed. Many brushless controllers like Spark MAX can also be configured for brushed motors, leaving the white wire disconnected.

!!! danger
    Speed controllers that support both brushed and brushless motors, like Spark MAX, **must** be configured for the correct type of motor. **Failing to do this can cause damage to connected motors.**

## CAN and PWM
How a speed controller connects to the [RoboRIO](roborio.md) is also an important thing to consider. Speed controllers can either use PWM or [CAN](can.md) to be controlled, with PWM being the more basic of the two. PWM can only be used to control speed as a raw percentage, while CAN allows for more functionality such as reading encoder values, using closed-loop control, and setting current limits. We almost always use CAN apart from if we need to quickly test something without a RoboRIO.

## Common Speed Controllers

<table>
<tr>
<td><h2>Spark MAX</h2> <img src="https://gblobscdn.gitbook.com/assets%2F-M7iEUG41QXEdyOMqbkc%2F-MJYv9C4h8tbatStpaCF%2F-MJYvPrW5J9iBBZiHcm5%2Fimage.png?alt=media&token=5eb47b17-072a-4d4a-8554-854e4f55248d"></td>
<td>
A "smart" speed controller by REV Robotics. Capable of driving brushed and REV Neo brushless motors. Controllable via both CAN and PWM. As of 2020, we used these exclusively.
</td>
</tr>
<tr>
<td><h2>Talon FX</h2> <img src="http://www.ctr-electronics.com/media/catalog/product/cache/1/image/c96a280f94e22e3ee3823dd0a1a87606/c/a/capture_1.png"></td>
<td>A "smart" speed controller integrated into and exclusively compatible with the VEX Falcon 500 brushless motor. Controllable via both CAN and PWM.</td>
</tr>
<tr>
<td><h2>Talon SRX</h2> <img src="https://www.vexrobotics.com/media/catalog/product/cache/d64bdfbef0647162ce6500508a887a85/2/1/217-8080.jpg"></td>
<td>Prior to brushless motors, these were considered the flagship "smart" speed controller. Only support brushed motors and are controllable via CAN and PWM.</td>
<td>
</tr>
<tr>
<td><h2>Victor SPX</h2> <img src="https://andymark-weblinc.netdna-ssl.com/product_images/aussie-victor-spx-motor-controller/5cdc1cd6fe93c623522f4e9c/zoom.jpg?c=1578276532"></td>
<td>A less smart brushed-only speed controller. Typically used to follow for a Talon SRX in a gearbox with multiple motors, since only a single speed controller needs to be "smart" in that case to handle encoders, etc. Supports CAN and PWM.
</tr>
</table>

## "Smart" Functionality

### Encoders
Most smart speed controllers like Spark MAX and Talon FX support accessing an [Encoder](encoders.md) over their CAN connection in order to measure a motor's rotation. In most cases, there will be a port for the encoder cable on the body of the speed controller.

### Current Limits
Smart speed controllers also usually allow for setting current limits. This is **highly encouraged** as a means of protecting the motor from burning out. If the current drawn by the motor exceeds the defined threshold, the speed controller will automatically throttle down the motor until the current draw falls back to an acceptable level. They are also useful for artificially limiting the torque a motor can exert, such as to prevent game pieces from getting sucked into a small crevice above an intake roller.

### Ramping
Ramping functionality allows the speed controller to effectively limit acceleration. While this can smooth out motion and make a robot easier to drive, ramping can also limit precision and cause problems in conjunction with closed loop control, which relies on fast response times which ramping can impede. For this reason, we typically do ramping on the controller side instead of on the motor side.