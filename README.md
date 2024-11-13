# Power Allocation System (FIFO)

This repository contains a FIFO-based power allocation system designed to manage device power consumption within a safe capacity limit. The system is designed to handle real-world constraints, ensuring efficient power usage across multiple devices that connect and disconnect over time.

## Problem Overview

In this scenario, a power supply system has a maximum capacity of 100 units, but only 92 units can be used for safety. Devices can connect, disconnect, and change their power consumption levels dynamically. Each device can consume a maximum of 40 units.

### Example Scenario

- **t=0**: Device A connects and gets 40 units (max capacity).
- **t=1**: Device B connects, A retains 40 units, and B gets 40 units.
- **t=2**: Device C connects, A and B retain 40 units each, and C gets 12 units (remaining available).
- **t=3**: Device A drops to 20 units, C’s allocation increases to 32 units.
- **t=4**: Device B disconnects, and C reaches 40 units with 32 units remaining available.

## Solution Approach

The algorithm uses a First-In-First-Out (FIFO) approach for allocating power:

- **When a device connects**: It gets as much power as possible up to its maximum.
- **When a device disconnects**: Its allocated power is freed up for other devices.
- **When a device changes consumption**: Available power is redistributed as needed.

## Pseudo Code

Please refer to the provided pseudo code for the implementation of the FIFO power allocation algorithm.

## Usage

1. **Define Device Actions**: Specify the devices’ connections, disconnections, and consumption changes.
2. **Run the Algorithm**: Execute the allocation logic to manage power usage dynamically.
3. **Observe Outputs**: View the power distribution per device, ensuring it remains within the system's safe capacity.

## Future Enhancements

Consider implementing logging to track power usage over time or visualizing power allocation dynamics for better insights.
