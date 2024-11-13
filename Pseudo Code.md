MAX_TOTAL_POWER = 92
MAX_DEVICE_POWER = 40

class Device:
    id: string
    connected_at: int
    power_requested: int
    power_allocated: int

devices = []  // FIFO queue of connected devices

function connect_device(device_id, requested_power):
    device = new Device(device_id, current_time(), requested_power, 0)
    devices.push(device)
    allocate_power()

function disconnect_device(device_id):
    // Find and remove the device from the list
    device = find_device_by_id(device_id)
    if device != null:
        devices.remove(device)
        allocate_power()

function adjust_power(device_id, new_requested_power):
    device = find_device_by_id(device_id)
    if device != null:
        device.power_requested = min(new_requested_power, MAX_DEVICE_POWER)
        allocate_power()

function allocate_power():
    total_power_used = sum(device.power_allocated for device in devices)
    available_power = MAX_TOTAL_POWER - total_power_used

    // Allocate power in FIFO order
    for device in devices:
        max_allowable = min(device.power_requested, MAX_DEVICE_POWER)
        
        if device.power_allocated < max_allowable:
            additional_power_needed = max_allowable - device.power_allocated
            power_to_allocate = min(additional_power_needed, available_power)
            
            device.power_allocated += power_to_allocate
            available_power -= power_to_allocate

function find_device_by_id(device_id):
    for device in devices:
        if device.id == device_id:
            return device
    return null

function current_time():
    // Return the current time (to simulate the time each device connects)
    return current_timestamp()

// Example Usage:
connect_device("A", 40)  // t=0: Device A requests 40 units
connect_device("B", 40)  // t=1: Device B requests 40 units
connect_device("C", 40)  // t=2: Device C requests 40 units
adjust_power("A", 20)    // t=3: Device A reduces its request to 20 units
disconnect_device("B")   // t=4: Device B disconnects
