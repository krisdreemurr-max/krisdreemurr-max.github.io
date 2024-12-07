# Chassis.moveToPose() is broken

*Nov 29 2024 - ongoing*

### Problem
When using the `chassis.moveToPose()` function, it takes a coordinates x and y as well as the angle theta that it will move to and a timeout. However, the robot kept moving until the timeout, even after it reached its destination.

### Problem code
```
chassis.setPose(0, 0, 0);
chassis.moveToPose(0, 36, 0, 100);
```
AND
```
chassis.setPose(0, 0, 0);
chassis.moveToPose(0, 36, 0, 1000);
```

### Solution 1: Measure the distance
To fix this, we decided to measure the distance the robot traveled when manipulated by timeout and adjust the timeout accordingly. This way, we could ensure that the robot would always travel the correct distance.
This method is highly time-consuming and impractical, so we didn't implement it.
There was no programming involved in this fix, beside altering the timeout parameter in the `chassis.moveToPose` function.

### Solution 2: Attempt to find the problem
We needed to know what specifically is causing the problem. We think that the robot is not reading its position correctly and thinks it needs to keep going forward to read its destination. To solve this, we simplifed our sensors, since we previously included tracking wheels that didn't exist, to ensure that all the sensors were correct. When we removed the tracking wheels (that we didn't have), the robot seemed to read its position correctly and worked as expected.

### Solution 2 Code: Attempt to find the problem
We just replaced the sensor's tracking wheels with ```nullptr```.
    
    lemlib::OdomSensors sensors(nullptr, // vertical tracking wheel 1
                            nullptr, // vertical tracking wheel 2
                            nullptr, // horizontal tracking wheel 1
                            nullptr, // horizontal tracking wheel 2
                            &imu // inertial sensor.
    );