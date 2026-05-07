# Control Systems
I touched on this briefly, talking about NextControl in the libraries page. However, I feel like control systems are one of the most important parts of FTC outside of pathing and the structure of the code (though pathing does use control systems; Pedro abstracts that away).

[CtrlAltFTC](https://www.ctrlaltftc.com/), as I mentioned in the libraries section, talks about control systems. So, I won't go over the same ground as it did. I'll instead try to cover a few usecases and implementations that the website may not have shown. I'll also give some examples. I will assume that you have read to the `Feedforward Control` page on CtrlAltFTC.

Let's talk about some practical places you may want to use a control system. It is very likely that if your robot has some sort of arm, you'll want to make it move to a certain position. Here's some example code to do such a thing:
```java
private PIDController pidController;
private ArmFeedforward feedforward;

@Override
public void initialize() {
    pidController = new PIDController(0.001, 0.001, 0.001);
    feedforward = new SimpleFeedforward(0.001, 0.003, 0.08, 0.001);
}

@Override
public void periodic() {
    motor.setPower(
            pidController.calculateFromReference(targetVelocity, currentVelocity) +
            feedforward.calculate(targetVelocity),
    );
}
```

This is probably a bit confusing, so let's talk about it. So, first off, we create a PID controller and a feedforward controller, specifically an arm feedforward controller. In the initialization step, we construct the two controllers. The three terms in the PID controller are the P, I, and D, constants respectively. The feedforward is a bit different. The first term is the gravity value, which is added to overcome gravity. The following 3 terms are the static, velocity, and acceleration gains. The first is used to combat static friction. The second and third are multiplied by the velocity and acceleration. The periodic section just sets the motor's power to the result of the feedforward controller added to the PID controller's output. We are not giving the feedforward controller acceleration in this example, so the last term does nothing.

## Control System Examples

### Controlling Multiple Motors
Let's say you have two motors that you want to apply the same control system to. How would you go about doing this? Well, firstly, you could take the average of the data you get from the two and use the control system on that, and then apply the power to both based on that. However, this is not a good way of doing things. Averaging the data from the motors is not good. Instead, it is quite a fair bit better to just take the control system of the output of one motor and apply the resulting power to both. NextFTC also has a `MotorGroup` class that streamlines this. Here is an example subsystem that uses the `MotorGroup`.
```java
private MotorGroup motors;

private PIDController pidController;
private SimpleFeedforward feedforward;

@Override
public void initialize() {
    motors = new MotorGroup(
            new MotorEx("right_flywheel_motor"),
            new MotorEx("left_flywheel_motor")
    );
    pidController = new PIDController(0.001, 0, 0);
    feedforward = new SimpleFeedforward(0.003, 0.08, 0.00);
}

@Override
public void periodic() {
    motors.setPower(Range.clip(
            pidController.calculateFromReference(targetVelocity, motors.getVelocity()) + 
            feedforward.calculate(targetVelocity),
            0, 1
        )
    );
}
```

One other thing you may notice about this code is that it clips the power to the motors to be within the range of 0 and 1. We don't particularly care about stopping the flywheel, and if we set it to allow the negatives the motor would work against the flywheel, which could cause burnout. Also if the flywheel is still spinning when we want to use it again that can decrease spin up time.

### Looptimes
Looptimes are very important for PIDs, with a lower loop time the faster the PIDs are. There's a trick we can do with the PIDs themselves to lower the looptimes. If we don't care about it holding it's position at certain times, we can just have a state for the motor that just sets the motor power to 0, instead of doing all of the expensive PID calculations. And when we get back to wanting to use the PID we can just toggle it back on. 

---
[Previous Page](https://github.com/FTC-26651/Lions-Documentation/blob/main/Programmers/Control%20Flow.md)

[Next Page](https://github.com/FTC-26651/Lions-Documentation/blob/main/Programmers/Miscellaneous.md)