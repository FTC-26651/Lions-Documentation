# Libraries

In our codebase, we use a variety of libraries. A library is a collection of pre-written code. Because of this, you can use them instead of writing everything from scratch. They can contain complicated things that are very useful, though hard to implement. They also often reduce bugs, as other people use the libraries and can report issues that arise.

### [Pedro Pathing](https://pedropathing.com/)
Pedro Pathing, or Pedro as it's more commonly called, is a pathing library. This means that it tells the drivetrain what to do. One of the biggest things that it can do is make paths, which the robot can be setup to follow. This is amazing for autonomous. The vast majority of teams have poor autonomous periods because they can't path well. Pedro fixes this by making following paths easy and accessible.

### [NextFTC](https://nextftc.dev/)

NextFTC is a command-based library with other utilities built in. There are two key ideas in command-based programming. Firstly, a command represents an action the robot can take. Commands run when scheduled, until they are interrupted or their end condition is met. The second is that of a subsystem. A subystem can represent one singular piece of hardware, but it can also represent seperate pieces of hardware that are working together for a goal. Take, for example, a drivetrain. A drivetrain constists of 4 seperate motors and odometry, but they're all working together for the same goal of moving the robot around.

NextFTC is not the only library in the NextFTC ecosystem. One of the other libraries in the ecosystem is NextControl. NextControl covers control systems. I won't go into much detail here, as [CTRL ALT FTC](https://www.ctrlaltftc.com/) already does a great job explaining everything. However, the goal of a control system is to move something to a desired state. This could be moving an arm to a specific position, or moving a flywheel to a specific velocity.

The final library in the NextFTC ecosystem is NextBindings. NextBindings is a command-based bindings library. It supports binding commands to buttons, and much more. It supports rising and falling edge detection, automatic gamepad polling, and joystick curving. I have not had the pleasure of using NextBindings all that much, but it is a very powerful library.

---
[PreviousPage](https://github.com/FTC-26651/Lions-Documentation/blob/main/Programmers/Learn%20Coding%20for%20FTC.md)