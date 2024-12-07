# Auton Code not running correctly

*Nov 2024*

### Problem
When we made an auton, the robot did not correctly follow the path.

### Solution 1: Make new auton
When we made a new autonomous file, Joe.cpp, we saw that the path the robot took was similar to the one in Joe.cpp, leading some of us to believe that the robot had randomly selected a file to run instead of the one it was directed to run. However, we decided that this was highly unlikely and decided to think of another solution.

### Solution 1 Code: Make new auton
Joe.cpp

### Solution 2: Figure out what's not working
Having decided that the robot was in fact runnning the correct autonomous file, we set out to find which specific part of the path the robot did not follow. Do do this we isolated the different parts of the path. For example, intaking goals, intaking rings, following lemlib instructions, and following paths from path.jerryio. From this, we concluded that the conveyor and ring intake worked perfectly. The goal intake worked inconsistently. The robot consistently followed instructions from lemlib, but did not move the correct distance. The robot followed straight paths from path.jerryio, but not other paths. To help solve movement based issues, we decided to tune the PIDs.

### Solution 2 Code: Figure out what's not working
We isolated different parts of the program:
###### Conveyor/ring intake:
    conveyor.move_velocity(12000); //run both the intake and the conveyor
    intake.move_velocity(12000);
    pros::delay(5000);
    conveyor.move_velocity(0); //stop both the intake and the conveyor
    intake.move_velocity(0);
###### goal intake:
    goal_intake.set_value(false); //close intake
    pros::delay(5000);
    goal_intake.set_value(true); //open intake
###### Instructions from lemlib:
    chassis.setPose(0,0,0);
    chassis.moveToPose(0,10,0,2000);
###### Following paths from path.jerryio:
    ASSET(path_txt);
    chassis.set_pose(0,0,0);
    chassis.follow(path_txt, 15, 2000);