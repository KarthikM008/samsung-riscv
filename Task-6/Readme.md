# TASK-6



 
# Object Detection System Using Ultrasonic Sensor & display it using  I2C LCD Display
This project utilizes an ultrasonic sensor to detect objects and measures the distance to them. The measured distance is then displayed on an I2C LCD screen.

# 1. Ultrasonic Sensor Operation:

The ultrasonic sensor operates by emitting high-frequency sound waves and measuring the time it takes for the sound waves to reflect back from an object.

Trigger Pulse: The sensor emits a short ultrasonic pulse through its transmitter.

Echo Pulse: The pulse travels through the air, reflects off an object, and returns to the sensor's receiver.

Time Measurement: The sensor measures the time interval between sending the trigger pulse and receiving the echo pulse.



# 2. I2C LCD Display:

The I2C LCD display is used to show the measured distance. It communicates with the microcontroller via the I2C protocol, which requires only two data lines: SDA (Serial Data) and SCL (Serial Clock).

Initialization: The microcontroller initializes the I2C communication and the LCD display.

Data Display: The calculated distance is converted to a string and sent to the LCD to be displayed.

# 3. System Workflow:

Initialization:

The microcontroller initializes the ultrasonic sensor and the I2C LCD display.
The LCD displays a welcome message or prompts the user.
Distance Measurement:

The microcontroller triggers the ultrasonic sensor to emit a pulse.
It waits for the echo pulse and measures the time taken for the round trip.
The distance to the object is calculated based on the measured time.
Display Update:

The LCD is cleared, and the new distance measurement is displayed.
Repeat:

The system repeats the measurement and display update at regular intervals.


# 4. Practical Applications:

This system can be used in various applications, such as:

Obstacle Detection: Detecting objects in the path of a robot or vehicle.

Level Measurement: Measuring the level of liquids or solids in a container.

Distance Sensing: Providing distance measurements for various automation tasks.



![WhatsApp Image 2025-02-17 at 9 23 47 PM](https://github.com/user-attachments/assets/4a530f90-c10f-42f6-8ae2-bed88094418b)


![Screenshot 2025-02-15 204918](https://github.com/user-attachments/assets/7e33fb01-34bb-482b-9dac-7ec183c20d54)

# VIDEO OF THE PROJECT



https://github.com/user-attachments/assets/8b87349d-d89b-4c6c-a4c9-51d903fcc41a





