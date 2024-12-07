# Wrong Kernel
*Oct 30 2024 - Nov 3 2024*

### Problem
When upgrading pros to the current version, so we could follow the current documentation, we accidentally upgraded the kernel as well. Lemlib only supports pros kernel version 4.1.0, so when we upgraded the kernel, lemlib broke, so our code stopped building.

### Solution
To solve this problem, we made a new project with the correct kernel version, and then copy and pasted all of the code that we changed in the previous project into the new project.

### Code Changed
Everything