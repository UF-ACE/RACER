## R*ACE*R PROJECT TEAM DOCS ##

---

#### Index ####
* Inertial Measurement Units (IMUs)
  * Overview
  * Accelerometers
  * Gyroscopes
  * Magnetometers
* Communication Interfaces
  * Universal Asynchronous Receiver-Transmitter (UART)
  * Serial Peripheral Interface Bus (SPI)
  * Inter-integrated Circuit Protocol (I2C)
  * Pulse Width Modulation (PWM)

 .
---

#### Inertial Measurement Units ####

Devices designed to track object motion. They vary from simple accelerometer/gyroscope combo boards to more elaborate systems with other integrated sensors like magnetometers as well as on-board microprocessors.

![imu-1](https://raw.githubusercontent.com/UF-ACE/RACER/master/documentation/assets/imu-1.png)

Several common factors are considered in selection of an IMU:
* Range: greater measurement ranges usually yield lower precision (and vice versa), some IMU devices allow for range/precision selection
* Interface:
  * Analog - output voltage is directly proportional to acceleration with mid-range voltage corresponding to 0 m/s2, easy to work with since most MPs come with ADCs, less expensive
  * Pulse-Width Modulation (PWM) - square wave of fixed frequency with varying duty cycle, not common for IMUs
  * Digital - (SPI/I2C), can be difficult to set up, more features, less noisy
* Axes: one, two or three, of course - the more the merrier, related to "degrees of freedom" or number of independent quantities being sensed
* Power: devices this small usually draw about .1 mA, some fancier (digital) sensors have sleep functions or power-saving operation modes

###### _Accelerometers_ ######

Devices capable of measuring static and dynamic acceleration. This is typically measured in units of meters per seconds squared (m/s2) or acceleration due to gravity (g ~ 9.8 m/s2) - 1g at rest and 0g in free-fall. Common applications include: tilt sensing in phones, motion sensing in game controllers, and automatic shutoff in dropped hard drives.

Generally, accelerometers contain internal capacitive plates - sometimes fixed, sometimes linked to small springs that oscillate as acceleration acts upon the sensor. Acceleration can be determined from the change in potential across these capacitive plates as they are mechanically forced toward or away from each other. Alternatively, some accelerometers rely on piezoelectric materials - tiny crystals that generate electricity when under mechanical stress.

![accelerometer-1](https://raw.githubusercontent.com/UF-ACE/RACER/master/documentation/assets/accelerometer-1.png)

###### _Gyroscopes_ ######

Devices used for measuring angular velocity - the speed and direction of rotation about an axis in units of degrees per second (deg/s). These sensors are not affected by noise due gravity and are therefore more effective at gauging orientation than an accelerometer. There are three primary axes of measurement roll (x), pitch (y), and yaw (z), each requiring unique hardware. Gyroscopes are used in various manned/autonomous land, air, and sea navigation applications as well as general motion capture.

When a gyroscope is rotated, a small resonating mass is shifted as the angular velocity changes and that motion is converted into low-current signals. These devices are notorious for "drift" (accumulated error/bias) in measurements over time. Some gyroscopes come with on-board thermometers which allow the user to compensate for drift by calibrating the device using advanced modeling techniques to correlate temperature with error.

![gyroscope-1](https://raw.githubusercontent.com/UF-ACE/RACER/master/documentation/assets/gyroscope-1.png)

###### _Magnetometers_ ######

Devices that measure magnetic field power and direction in units of Gauss (G), effectively serving as compasses used to track heading over a course of motion. Coupled with an accelerometer and gyroscope, this sensor offers IMUs additional data to supplement their other sensors and provide as many as nine degrees of freedom (3 axes for each of three devices).

![magnetometer-1](https://raw.githubusercontent.com/UF-ACE/RACER/master/documentation/assets/imu-2.png)

---

#### Communication Interfaces ####

Communication protocols are systems of rules allowing two or more entities transmit information via variation of some physical quantity. A well-defined protocol precisely formalizes syntax, semantics, and synchronization as well as possible error recovery methods. Protocols may be implemented by hardware, software, or a combination of both. A _serial interface_ is one in which single bits of data are sent sequentially from one system to another over a wire whereas a _parallel interface_ allows for entire bytes of data to be sent in parallel over a bus.

###### _Universal Asynchronous Receiver-Transmitter (UART)_ ######
A UART is a computer hardware device often built into microcontrollers for asynchronous communication with peripheral devices over a serial port with configurable data format and transmission speeds. At the source, bytes of data are decomposed into bits using a shift register, transmitted sequentially, and reassembled into complete bytes at the destination using another shift register. This serial transmission of bits through a single wire is less costly than parallel transmission through multiple wires. Communication may be set up in a simplex (single direction), half duplex (toggle transmit/receive), or full duplex (simultaneous transmit/receive) fashion.

![uart-1](https://raw.githubusercontent.com/UF-ACE/RACER/master/documentation/assets/uart-1.png)

###### _Serial Peripheral Interface Bus (SPI)_ ######
SPI is a interface bus often used to send data between microcontrollers and small peripherals especially good for high data rate full-duplex connections. This interface resolves a common problem with asynchronous transmission, namely that there is no guarantee both devices are transmitting/receiving the right data (i.e. “in sync”), without the overhead of appending “start” and “stop” bits for each byte and the need to establish a transmission speed in advance. It is also much simpler and cheaper to implement the required hardware than is necessary for a UART.

![spi-1](https://raw.githubusercontent.com/UF-ACE/RACER/master/documentation/assets/spi-1.png)

In this setup, a Master device produces a Serial Clock (SCK) to control the rate at with data is transmitted (Master Out Slave In - MOSI) and received (Master In Slave Out – MISO). This does require the Master to know when the data is ready and how much data is expected, but this is reasonable for peripherals with a rigid command structure. This system also allows for multiple Slaves to be connected to the Master device and toggled on/off via a Slave Select (SS) signal. However, these Slaves are unable to communicate directly with each other, and Master I/O may become unmanageable since each additional Slave requires its own select signal.

###### _Inter-Integrated Circuit_ ######


###### _Pulse-Width Modulation (PWM)_ ######


---

Other Topics
* Motion/Path Tracking
* Computer Vision
