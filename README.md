# Sensor Testing for Smart Carry Bagpack

This repository contains individual code examples for testing various sensors and functions used in the [Smart Carry Bagpack](https://github.com/g-gourav-r/Smart-Carry-Bagpack) project. If you are working on the Smart Carry Bagpack project, these code examples will help you ensure that your sensors are working correctly before integrating them into the main project.

## Code and Its Function

- **Force_Calculator_FSR.ino**: Use this code to check whether individual sensors are working properly.

- **Middle_Force_Sensor_test_Without_Buzzer.ino**: This code will print the force sensed by the sensor placed in the middle of the backpack.

- **Middle_Force_Sensor_with_Buzzer.ino**: Use this code to check whether the buzzer is working when the threshold is crossed.

- **Strap_Sensors.txt**: Use this code to check the force difference between the two straps. The output will be printed in the serial monitor of the Arduino IDE.

- **calibrate.ino**: This code can be used to check the overall working of the sensors with the application. It will check the force on both straps thrice successively to determine which side has more force.

- **find_my_bag.ino**: This code is used to check whether the input being sent by the application is working or not. For designing the app in MIT App Inventor, refer to the `android.md` file.

Make sure to refer to the individual code files for more detailed instructions on how to use them.
