# Running Autonomous code without controller

*Nov 23 2024 - Dec 2 2024*

### Problem
While testing our autonomous function, we discovered that the robot was unable to reverse adequately, it kept spinning, which is inefficient.
### Solution 1: Make a new function.
We decided on creating a new function that directly reverses the motor movement in order to have a more robust reverse system. 
### Solution 2 Code: Run it from the robot, but like actually do it
This code was put into a header file so we can access it from any other file.

In utils.h we have
```
#pragma once

/**
 * @brief sets the voltage of each drivetrain motor to speed for time milliseconds. 
 * 
 * @param time time in milliseconds
 * @param speed speed in mV
 * 
*/
void move(double time, int speed);

```

In utils.cpp we made
```
void move(double time, int speed) {
    pros::Motor l1(10, pros::MotorGearset::blue);
    pros::Motor l2(-9, pros::MotorGearset::blue);
    pros::Motor l3(8, pros::MotorGearset::blue);

    pros::Motor r1(-3, pros::MotorGearset::blue);
    pros::Motor r2(4, pros::MotorGearset::blue);
    pros::Motor r3(-2, pros::MotorGearset::blue);

    l1.move_voltage(speed);
    l2.move_voltage(speed);
    l3.move_voltage(speed);
    r1.move_voltage(speed);
    r2.move_voltage(speed);
    r3.move_voltage(speed);
    pros::delay(time);
    l1.move_voltage(0);
    l2.move_voltage(0);
    l3.move_voltage(0);
    r1.move_voltage(0);
    r2.move_voltage(0);
    r3.move_voltage(0);
}
```