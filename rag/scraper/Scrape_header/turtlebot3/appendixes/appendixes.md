
[Edit on GitHub](https://github.com/ROBOTIS-GIT/emanual/blob/master/docs/en/platform/turtlebot3/more_info/appendixes.md "https://github.com/ROBOTIS-GIT/emanual/blob/master/docs/en/platform/turtlebot3/more_info/appendixes.md") 

# [More Info](#more-info "#more-info")

## [Appendixes](#appendixes "#appendixes")

### [DYNAMIXEL](#appendix-dynamixel "#appendix-dynamixel")

![](/assets/images/platform/turtlebot3/appendix_dynamixel/dynamixel_x.jpg)

#### [Overview](#overview "#overview")

`DYNAMIXEL X-Series` is a new line-up of high performance networked actuator module, which has been widely used for building various types of robots with reliability and expandability.

Two different types of DYNAMIXEL is adopted in TurtleBot3 Burger, Waffle and Waffle Pi as they have different requirements. DYNAMIXEL X-Series shares its design, therefore, users can replace actuators depend on applications.

* Basic Features
	+ Improved Torque with Compact Size
	+ Enhanced Durability and Expandability
	+ Hollow Back Case Minimizes Cable Stress (3-way-routing)
	+ Direct Screw Assembly to the Case (without Nut Insert)
	+ Improved Heat Sink Featuring Aluminum Case
* Various Control Functions
	+ 6 Operating Modes
	+ Current-Based Torque Control (4096 steps, 2.69mA/step)
	+ Profile Control for Smooth Motion Planning
	+ Trajectory Data and Moving Status (In-Position, Following Error, etc.)
	+ Energy Saving (Reduced Current from 100mA to 40mA)

#### [Specifications](#specifications "#specifications")

| Items | [XL430-W250](/docs/en/dxl/x/xl430-w250/ "/docs/en/dxl/x/xl430-w250/") (for Burger) | [XM430-W210](/docs/en/dxl/x/xm430-w210/ "/docs/en/dxl/x/xm430-w210/") (for Waffle and Waffle Pi) |
| --- | --- | --- |
| Microcontroller | ST CORTEX-M3 (STM32F103C8 @ 72Mhz, 32bit) | ST CORTEX-M3 (STM32F103C8 @ 72Mhz, 32bit) |
| Position Sensor | Contactless Absolute Encoder (12bit, 360°) | Contactless Absolute Encoder (12bit, 360°) |
| Motor | Cored Motor | \*\*Coreless Motor \*\* |
| Baud Rate | 9600 bps ~ 4.5 Mbps | 9600 bps ~ 4.5 Mbps |
| Control Modes | Velocity, Position, Extended Position, PWM | Velocity, Position, Extended Position, PWM, **Current**, **Current-base Position** |
| Gear Ratio | 258.5 : 1 | 212.6 : 1 |
| Stall Torque | 1.0 N.m (@ 9V, 1A) | **2.7 N.m (@ 11.1V, 2.1A)** |
|  | 1.4 N.m (@ 11.1V, 1.3A) | 3.0 N.m (@ 12V, 2.3A) |
|  | 1.5 N.m (@ 12V, 1.4A) | 3.7 N.m (@ 14.8V, 2.7A) |
| No Load Speed | 47rpm (@ 9V) | **70rpm (@ 11.1V)** |
|  | 57rpm (@ 11.1V) | 77rpm (@ 12V) |
|  | 61rpm (@ 12V) | 95rpm (@ 14.8V) |
| Communication | TTL Level Multi Drop Bus | TTL Level / RS485 Multi Drop Bus |
| Material | Engineering Plastic | Full Metal Gear, Metal Body, Engineering Plastic |
| Standby Current | 52mA | 40mA |

* More information for actuators can be found at below ROBOTIS e-Manual links.
	+ [XL430-W250](/docs/en/dxl/x/xl430-w250/ "/docs/en/dxl/x/xl430-w250/") for TurtleBot3 Burger
	+ [XM430-W210](/docs/en/dxl/x/xm430-w210/ "/docs/en/dxl/x/xm430-w210/") for TurtleBot3 Waffle and Waffle Pi

#### [DYNAMIXEL SDK](#dynamixel-sdk "#dynamixel-sdk")

![](/assets/images/sw/sdk/dynamixel_sdk/overview/dynamixel_sdk_concept_logo.jpg)

The ROBOTIS DYNAMIXEL SDK is a software development library that provides DYNAMIXEL control functions for packet communication. The API is designed for DYNAMIXEL actuators and DYNAMIXEL-based platforms. TurtleBot3 uses DYNAMIXEL SDK in OpenCR to control the actuator.

* More information for DYNAMIXEL SDK can be found at below ROBOTIS e-Manual and GitHub links.
	+ [e-Manual of DYNAMIXEL SDK](/docs/en/software/dynamixel/dynamixel_sdk/overview/ "/docs/en/software/dynamixel/dynamixel_sdk/overview/")
	+ [GitHub Repository of DYNAMIXEL SDK](https://github.com/ROBOTIS-GIT/DynamixelSDK "https://github.com/ROBOTIS-GIT/DynamixelSDK")

 Previous Page
Next Page 