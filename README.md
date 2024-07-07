# CSCI 3081W Drone Simulation Project

Welcome to Drone Simulation Project!

*Done as part of CSCI 3081W class*

## Prerequisites

Before you begin, ensure you have the following installed:

- Git
- GNU Make
- A C++ compiler supporting C++17 (e.g., g++ or clang)

## Accessing a CSE Lab Machine

 ### SSH in to university lab machines 
If you have a CSE Labs account, you can SSH into one of the CSE lab machines on campus (_Keller 1-262 machines are preferred_). For detailed instructions on how to SSH, information on computer names, and operating systems of the machines, visit [this link](https://cse.umn.edu/cseit/classrooms-labs#cselabs).

You can also access a CSE lab machine virtually using [VOLE](https://csel-vole-fx3-prd.cselabs.umn.edu:3443/auth/ssh/). For a tutorial to help you get started with VOLE, click [here](https://mediaspace.umn.edu/media/t/1_xlkh0azp). 

If you do not have a CSE account, you can create one following these [instructions](https://wwws.cs.umn.edu/account-management).

Example code if you wish to ssh into keller 1-262 lab machines. 
````
ssh X500@csel-kh1262-01.cselabs.umn.edu
````

replace x500 with your personal x500, for example 

```
ssh sonsa021@csel-kh1262-01.cselabs.umn.edu. 
```
_This will prompt you for a duo authentication if ssh private keys not configured_

## CSE Quota 

To prevent the simulation from failing to build properly or from preventing you from logging into the CSE lab machine, let's begin by checking our personal CSE Lab Machine's quota. You can check this by following these steps:

1. Open a seperate terminal window. Make sure you are SSHed in to the CSE lab machine 

2. Copy the following code 

```
$ csequota
```

3. This will show you the current quota usage on the CSE machines. If you are over 90%, consider deleting some files or clearing out some cache by using the following command
```
$ rm rf .cache  
```

## Clone the repository 

To download and install the project, first clone the repository.

1. Open a terminal window 

2. Make a project folder 

```
$ mkdir project 
$ cd project
```

3. Clone the repository by pasting the following code in the terminal 

```
$ git clone https://github.umn.edu/umn-csci-3081-s24/team-010-21-finalproject.git
```

At this point you would have the entire code base in your personal machine. 

4. Run the simulation 

Begin by cleaning the repository with any generated files.

```
$ make clean
```

Build the simulation  

```
$ make -j
```

Run the simulation 

```
$ make run 
```

## Port Forwading

The Makefile provided with the coding files directs the program to open on port 8086.

Navigate to http://127.0.0.1:8086 to see the simulation.

_Note_: If the program doesn't load properly, navigate to the Makefile and update the port (e.g., 8081, 8082, 8083...). Also, update the link accordingly.

## Overview of the simulation 
The project builds a up a 3-D model of the UMN campus, along with a robot, human, drone, a helicopter entities. All the entities, apart from the drone, will be traversing through the simulation as it runs. The data dashboard will collect this as the first entry with all the first row containing all zeroes (Since the drone remains stationary if there is no delivery assigned). One can schedule a delivery by hitting Schedule trip button on the tab, which can be seen on the frontend. Create a package by giving it a name and assign the drone a starting and drop off coordinates. One can build as many drone entities and schedule as many trips as they wish by hitting the add Drone button and schedule trip. The data collected by the drones during the travel can be accesed by seeing the standard-output.csv file generated during runtime.  


## New Features 
### Data Dashboard
The feature which we have implemented in this project is adding a data dashboard. This dashboard is implemented by following a singleton design pattern, which collects data from the drone when a trip is scheduled. The drone, when provided with a starting and endpoint and a routing strategy, moves to pickup a package from the starting checkpoint and move to the drop off point. All this while, the data collection model collects the distance travelled by the drone to reach the package, distance travelled by the drone to deliver the package as well as the time associated with it. This allows us to figure out which strategy pattern is the most effective in package deliveries for both short distance travel and long distane travel, and potentially which routing methods would be ideal for fuel conservation (idealy the model which takes the shortest path to conserve energy)

| Drone Name | Package No. | Trip Distance | Total Distance Travelled | Trip Time | Total Flying Time |
|------------|-------------|---------------|--------------------------|-----------|-------------------|
| Drone      | 0           | 0             | 0                        | 0         | 0                 |
| Drone      | 1           | 257.839       | 551.817                  | 8.59462   | 18.4114           |
| Drone      | 2           | 494.539       | 968.517                  | 24.489    | 40.3157           |
| Drone      | 3           | 23784.5       | 24339.5                  | 804.83    | 823.367           |
| Drone      | 4           | 24247.7       | 25744.4                  | 824.276   | 874.213           |



