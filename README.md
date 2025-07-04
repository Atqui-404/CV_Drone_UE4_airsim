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
0. Download your environment from Unreal market (the one I used is City Park Environment Collection by SilverTM) and click 'create project' in Epic Games Launcher under library > FAB library > *environment*
1. Follow mattquinoa's tutorial using the environment you downloaded.
   If there's an error in vs studio when trying to build, do make the project a start-up project, this will fix the error.
2. Download the Drone_prop.fbx and Drone FBX.fbx or your desired drone model seperated as propellers and the drone(except propellers) and import it into *project_name\Plugins\AirSim\Content\Blueprints* in the       Unreal project at the same time. You may need to adjust the directions or resize them when importing.
   **Do scale the drone body to about 100 x 100 x smth. For the fbx files in this page, both were uniformly scaled by x3 and drone body was orientated by -90 in the Z-axis** 

   **Method 1:**
   Duplicate the BP_FlyingPawn and rename it.
   Go into the renamed bp and replace the drone with your imported drone and then replace the propellers
   -> if the propeller pivot is not correct, go to the propeller asset and adjust using top view. *(For the Drone_prop.fbx, it was translated to X: -42, Y: -32, Z: -22)*

   Fit the propellers nicely on top of the drone for each propeller used.

   **Method 2:**
   If you're using the Mavic 2 Pro, you can try to add BP_MyPawn.uasset immediately to *project_name\Plugins\AirSim\Content\Blueprints* and hopefully everything would be inside already otherwise pls go back to      method 1.
   
   Head to settings.json and add
```
   "PawnPaths":{
    "DefaultQuadrotor": {"PawnBP": "Class'/Airsim/Blueprints/BP_MyPawn.BP_MyPawn_C'"}
  },
```
3. To increase resolution, after opening the .sln folder, open SimHUD.cpp and go to line 196
```
    //Equivalent to enabling Custom Stencil in Project > Settings > Rendering > Postprocessing
    UKismetSystemLibrary::ExecuteConsoleCommand(GetWorld(), FString("r.CustomDepth 3"));
```
   and add the following code below:
```
    //set up for better resolution
    UKismetSystemLibrary::ExecuteConsoleCommand(GetWorld(), FString("t.MaxFPS 80"));
    UKismetSystemLibrary::ExecuteConsoleCommand(GetWorld(), FString("r.ScreenPercentage 200"));
    UKismetSystemLibrary::ExecuteConsoleCommand(GetWorld(), FString("r.Streaming.PoolSize 2000"));
    UKismetSystemLibrary::ExecuteConsoleCommand(GetWorld(), FString("r.ShadowQuality 2"));
    UKismetSystemLibrary::ExecuteConsoleCommand(GetWorld(), FString("r.OneFrameThreadLag 0"));
    UKismetSystemLibrary::ExecuteConsoleCommand(GetWorld(), FString("r.MipMapLODBias -2"));
    UKismetSystemLibrary::ExecuteConsoleCommand(GetWorld(), FString("r.ViewDistanceScale 4"));
```

# How to Run
View this demonstration on how to run the simulator: https://drive.google.com/file/d/131emWFGXbcBOnIILi92xgsu8BX166k-I/view?usp=drive_link

# How to annotate
Use CVAT annotator to annotate the simulator videos you have from this link: https://docs.cvat.ai/docs/manual/basics/track-mode-basics/ 

Step 1: Create a project

Step 2: Under 'Constructor', you can input the label 'drone' and click the 'continue' button under it. You will see the label disappear but not to worry.

Step 3: Click 'Submit & Open' to create the project and open it immediately. If you accidentally went out of it, just click under 'projects' and you've find your desired project there.

Step 4: Click the '+' button to create a new task

Step 5: Upload the video you want to annotate. Go to advanced configurations and change the 'Image Quality' to **100%** from 70%

Step 6: Open the task and on the side bar on the left, you'll see a rectangle button. Select that 'rectangle' and click drawing method 'by 2 points' followed by 'Track'

Step 7.1: If the drone happens to be blocked by something, Click 'switch outside property' on the right side of the screen at the label. Repeat step 6.
