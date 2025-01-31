# Cube Flight Controller

The [Cube](http://www.proficnc.com/61-system-kits2) flight controller (previously known as Pixhawk 2.1) is a flexible autopilot intended primarily for manufacturers of commercial systems. 它基于 [Pixhawk 项目](https://pixhawk.org/) 的 **FMUv3** 开放硬件设计，在 [NuttX](http://nuttx.org) 操作系统上运行 PX4。

<img src="../../assets/flight_controller/cube/pixhawk2_cube_hero.png" width="400px" />

The controller is designed to be used with a domain-specific carrier board in order to reduce the wiring, improve reliability, and ease of assembly. For example, a carrier board for a commercial inspection vehicle might include connections for a companion computer, while a carrier board for a racer could includes ESCs form the frame of the vehicle.

Cube includes vibration isolation on two of the IMU's, with a third fixed IMU as a reference / Backup.

## 主要特性

- 32bit STM32F427 [Cortex-M4F](http://en.wikipedia.org/wiki/ARM_Cortex-M#Cortex-M4)<sup>&reg;</sup> core with FPU
- 168 MHz / 252 MIPS 
- 256 KB RAM
- 2 MB Flash \(fully accessible\)
- 32 bit STM32F103 failsafe co-processor
- 14 PWM / Servo outputs (8 with failsafe and manual override, 6 auxiliary, high-power compatible)
- Abundant connectivity options for additional peripherals (UART, I2C, CAN)
- Integrated backup system for in-flight recovery and manual override with dedicated processor and stand-alone power supply (fixed-wing use)
- Backup system integrates mixing, providing consistent autopilot and manual override mixing modes (fixed wing use)
- Redundant power supply inputs and automatic failover
- External safety switch
- Multicolor LED main visual indicator
- High-power, multi-tone piezo audio indicator
- microSD card for high-rate logging over extended periods of time

## Where to Buy {#stores}

- [The Cube](http://www.proficnc.com/61-system-kits) (ProfiCNC)

## Specifications

### Processor

- 32bit STM32F427 [Cortex M4](http://en.wikipedia.org/wiki/ARM_Cortex-M#Cortex-M4) core with FPU
- 168 MHz / 252 MIPS 
- 256 KB RAM
- 2 MB Flash (fully accessible)
- 32 bit STM32F103 failsafe co-processor

### Sensors

- TBA

### Interfaces

- 5x UART (serial ports), one high-power capable, 2x with HW flow control
- 2x CAN (one with internal 3.3V transceiver, one on expansion connector)
- Spektrum DSM / DSM2 / DSM-X® Satellite compatible input
- Futaba S.BUS® compatible input and output
- PPM sum signal input
- RSSI (PWM or voltage) input
- I2C
- SPI
- 3.3v ADC input
- Internal microUSB port and external microUSB port extension

### Power System and Protection

- Ideal diode controller with automatic failover
- Servo rail high-power (max. 10V) and high-current (10A+) ready
- All peripheral outputs over-current protected, all inputs ESD protected

### 额定电压

Pixhawk can be triple-redundant on the power supply if three power sources are supplied. The three rails are: Power module input, servo rail input, USB input.

#### 正常运行最大额定值

Under these conditions all power sources will be used in this order to power the system

- Power module input (4.8V to 5.4V)
- Servo rail input (4.8V to 5.4V) **UP TO 10V FOR MANUAL OVERRIDE, BUT AUTOPILOT PART WILL BE UNPOWERED ABOVE 5.7V IF POWER MODULE INPUT IS NOT PRESENT**
- USB power input (4.8V to 5.4V)

#### 绝对最大额定值

在以下条件下，系统不会获得任何供电（不可运行），但不会损坏。

- Power module input (4.1V to 5.7V, 0V to 20V undamaged)
- Servo rail input (4.1V to 5.7V, 0V to 20V)
- USB power input (4.1V to 5.7V, 0V to 6V)

## Pinouts and Schematics

Board schematics and other documentation can be found here: [The Cube Project](https://github.com/proficnc/The-Cube).

The datasheet from Hex manufacturing can be found [here](http://www.hex.aero/wp-content/uploads/2016/07/DRS_Pixhawk-2-17th-march-2016.pdf).

## Ports

### Top-Side (GPS, TELEM etc)

![Cube Ports - Top (GPS, TELEM etc) and Main/AUX](../../assets/flight_controller/cube/cube_ports_top_main.jpg)

### Debug Ports

![Cube Debug Ports](../../assets/flight_controller/cube/cube_ports_debug.jpg)

### USB/SDCard Ports

![Cube USB/SDCard Ports](../../assets/flight_controller/cube/cube_ports_usb_sdcard.jpg)

## Building Firmware

> **Tip**大多数用户将不需要建立此固件! 它是预构建的, 并在连接适当的硬件时由 *QGroundControl* 自动安装。

为此目标 [编译 PX4](https://dev.px4.io/en/setup/building_px4.html)：

    make px4_fmu-v3_default
    

## Issues

CAN1 and CAN2 silk screen on the Pixhawk 2.1 are flipped (CAN1 is CAN2 and vice versa).