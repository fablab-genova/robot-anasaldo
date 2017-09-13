# Robot specs / Specifiche del Robot


Number of DOF / Gradi di libertà: 6

## Kinematics / Cinematica

## Joints specifications / Specifiche giunti

All motors are from [GEC ALSTHOM][https://en.wikipedia.org/wiki/Alstom]; the company was acquired in 1998. No original datasheet and product data are available.

| Joint \# | motor model         | motor voltage | has brake |
|----------|-------------------- |---------------|-----------|
| 1        | RS440G K1300        |               |           |
| 2        | RS440G K1300        |               |           |
| 3        | RS130G              |               |           |
| 4        | RS130G              |               |           |
| 5        | RS130G              |               |           |
| 6        |                     |               |           |

## Comments / Commenti

**[ENG]**

The robot's kinematics are rather strange.
In particular, the axis of joint \#3 is oriented in an "axial" direction.
This choice is not conventional since this layout deos not extend significantly the workspace of the robot.
The original application of the robot, which we do not know, probably justified this design decision.

**[ITA]**

La cinematica del robot è un pò strana.
In particolare la configurazione del giunto \#3 orientato in direzione assiale è decisamente inusuale, dato che non contribuisce in modo importante ad estendere l'area di lavoro del robot.
L'applicazione originale del robot, che non ci è dato sapere, giustificava probabilmente questa scelta progettuale.
