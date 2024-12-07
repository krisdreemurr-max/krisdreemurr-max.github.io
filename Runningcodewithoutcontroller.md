# Running Autonomous code without controller

*Nov 23 2024 - Dec 2 2024*

### Problem
Over Thanksgiving break, our team captain took home our robot to work on it. However, he forgot to bring a controller, so he couldn't test the autonomous code, or drive the robot.

### Solution 1: Run it from the robot
The robot brain has a menu where you can run autonomous code, so we tried to run it from the robot. However, the timed run button, which ran the autonomous code, did not work on our brain, so this solution didn't work.

### Solution 2: Run it from the robot, but like actually do it
However, the robot brain also had a run button, which ran drive code, which did work. However, we couldn't test autonomous code because the button ran driver code. The workaround we found was to call the autonomous function form the driver code, before the forever loop that ran the driver code. We also added a delay before running the autonomous to allow our captain to remove his fingers from the robot before the autonomous code ran.

### Solution 2 Code: Run it from the robot, but like actually do it
The code for this improvement is very simple, just running the autonomous before the driver code.

    OPcontrol() {
        pros::delay(5000);
        autonomousFunction(chassis, Intake, Conveyor, goal_piston);

        //rest of driver code
    }