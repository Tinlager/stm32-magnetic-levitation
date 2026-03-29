# STM32 Magnetic Levitation (DIY)

A single-axis magnetic levitation system built from scratch using an STM32 microcontroller. The project demonstrates real-time control of an electromagnetic coil using a custom PID controller to keep a permanent magnet suspended in mid-air.

## Hardware Stack
* **MCU:** STM32F103 (configured via STM32 HAL)
* **Sensor:** Linear Hall Effect Sensor (analog)
* **Actuator:** Repurposed 12V printer solenoid with a custom-modified iron core (to focus the magnetic field and reduce reluctance force).
* **Power / Driver:** IRF540N MOSFET with a flyback diode.

## Key Software Features & Math
* **Custom PID Controller:** Written in C from scratch.
* **ADC Signal Processing:** Implementation of 64x oversampling and exponential moving average (EMA) filters to clean up noisy Hall sensor data.
* **Magnetic Interference Compensation:** The software dynamically subtracts the coil's own magnetic field "noise" from the Hall sensor readings based on the current PWM duty cycle.
* **Hardware Inversion Handling:** PWM logic accounts for the inverted state of the N-channel MOSFET driver.

## Engineering Challenges Solved
During development, I faced the "Zone of No Return" (reluctance force) where the passive iron core attracted the magnet stronger than gravity. I solved this by replacing the massive original core with a thinner one (a screw) to focus the magnetic field lines and adjusting the PID `setpoint` to operate safely below the critical threshold.
