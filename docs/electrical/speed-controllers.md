# Speed Controllers
!!! note
    This page is about the hardware/conceptual aspects of speed controllers. If you are looking for details on their usage in software, see /link/

Speed controllers are one of the most important components involved in getting a robot moving. In short, they are responsible for converting software commands into actual motor activity.

## Brushed and Brushless
An important distinction in speed controllers is if they are designed for brushed or brushless motors due to their differing means of actuation. You can usually tell this from how many output wires a speed controller has. Something with red, white, and black wires coming out of one side is designed for brushless, while just red and black is for brushed. Many brushless controllers like Spark MAX can also be configured for brushed motors, leaving the white wire disconnected.

!!! danger
    Speed controllers that support both brushed and brushless motors, like Spark MAX, **must** be configured for the correct type of motor. **Failing to do this can cause damage to connected motors.**

## CAN and PWM
How a speed controller connects to the [RoboRIO](roborio.md) is also an important thing to consider. Speed controllers can either use PWM or [CAN](can.md) to be controlled, with PWM being the more basic of the two. PWM can only be used to control speed as a raw percentage, while CAN allows for more functionality such as reading encoder values, using closed-loop control, and setting current limits. We almost always use CAN apart from if we need to quickly test something without a RoboRIO.

## Common Speed Controllers
- Spark MAX
- Talon FX
- Victor SPX
- Talon SRX

## "Smart" Functionality

### Encoders
Most smart speed controllers like Spark MAX and Talon FX support accessing an [Encoder](encoders.md) over their CAN connection in order to measure a motor's rotation. In most cases, there will be a port for the encoder cable on the body of the speed controller.

### Current Limits
Smart speed controllers also usually allow for setting current limits. This is **highly encouraged** as a means of protecting the motor from burning out. If the current drawn by the motor exceeds the defined threshold, the speed controller will automatically throttle down the motor until the current draw falls back to an acceptable level. They are also useful for artificially limiting the torque a motor can exert, such as to prevent game pieces from getting sucked into a small crevice above an intake roller.

### Ramping
Ramping functionality allows the speed controller to effectively limit acceleration. While this can smooth out motion and make a robot easier to drive, ramping can also limit precision and cause problems in conjunction with closed loop control, which relies on fast response times which ramping can impede. For this reason, we typically do ramping on the controller side instead of on the motor side.