
Drive By Wire
-------------

.. contents:: Table of contents
    :depth: 2
    :local:

This document describes the design of the drive by wire system used in the Autonomous Rover.

Overwiew
--------

The goal of a drive by wire system is to enable the control of a vehicle using a computer. It is considered the heart of advanced driver assisiance systems (ADAS) and autonomous vehciles applications. It enables the implementation of a wide range of applications in the automotive field. Typically, the system is composed of one or more compute platforms and a set of sensors and actuators. The system is then installed onto a vehicle to enable the control of the throttle, the brakes and the steering wheel. Each one of those components is categorized as a subsystem of the overall drive-by-wire system.

In the Autonomous Rover application, the steering wheel and the throttle are controllable through an Electronic Speed Controller (ESC), which accepts an PWM signal with a duty cycle between 1ms and 2ms, with 1.5ms being the center or the zero position. The ESC accepts a PWM frequency in the range of 100Hz.

An Electronic Control Unit (ECU) will need to be programmed to send the PWM output the the ESC in order to control the vehicle velocity and direction.

In this project a Tiva C, TM4C123GXL, microcontroller (MCU) has been chosen as the drive-by-wire ECU since it contains all the required periphirals to control and monitor electric motors, e.g: PWM, Quadrature Encoders and CAN interface.

The TM4C is an ARM Cortex M4 MCU with a maximum frequency of 80MHz, https://www.ti.com/lit/gpn/tm4c123gh6pm

.. image:: resources/TM4C.png
    :width: 400

For steering and throttle control, pins PD0 and PD1 are programmed to output a PWM at 100Hz. PD0 and PD1 are pinmuxed to PWM0 and PWM1 respectively, on PWM Module 1 and Genarator 0.

For speed measurement the quadrature encoder interface is used with a two channels quadrature encoder sensor, which is installed on the vehicle and connected to the gear box using a 3d printed gear and mounting bracket.

.. image:: resources/Quadrature_encoder.jpg
    :width: 400

The TM4C has two quadrature encoder interface in this project QEI0 is used and channel 0 and 1 of the quadrature encoder sensor are connected to pins PD6 and PD7 respectively.