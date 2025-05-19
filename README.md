# CV_Drone_UE4_airsim
This project setup was originally based on mattquinoa's excellent tutorial and repository: https://github.com/mattquinoa/PX4Project.
Modifications were made to the drone model, camera setup, and system behavior to suit custom CV data collection needs.

# Acknowledgements
This project uses Microsoft AirSim, an open-source simulator for drones, cars and more, built on Unreal Engine. AirSim is licensed under the MIT License. https://microsoft.github.io/AirSim/

It also uses PX4 Autopilot, an open-source flight control software licensed under the BSD 3-Clause License. https://github.com/PX4/PX4-Autopilot

This setup integrates with QGroundControl for mission planning and real-time telemetry.

# Requirements
Ensure that you've downloaded Unreal 4.27
# Setup
0. Download your environment from Unreal market
1. Follow mattquinoa's tutorial using the environment you downloaded.
   If there's an error in vs studio when trying to build, do make the project a start-up project, this will fix the error.
2. Download the Drone_prop.fbx and Drone FBX.fbx or your desired drone model seperated as propellers and the drone(except propellers)
   Duplicate the BP_FlyingPawn and rename it
   Go into the renamed bp and replace the drone with your imported drone and then replace the propellers
   -> if the propeller pivot is not correct, go to the propeller asset and adjust using top view
   Place the propellers nicely
   go settings.json and add
```
   "PawnPaths":{
    "DefaultQuadrotor": {"PawnBP": "Class'/Airsim/Blueprints/BP_MyPawn.BP_MyPawn_C'"}
  },
```
