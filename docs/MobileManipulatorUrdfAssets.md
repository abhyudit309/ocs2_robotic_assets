# OCS2 Mobile Manipulator

The `ocs2_mobile_manipulator` package supports robotic arms and wheel-based mobile manipulators. The system model is determined by parsing the URDF and the task file.

Over here, we specify the steps involved in creating the URDF used for the Kinova Gen3.

* In the `src` directory of your ocs2 catkin workspace, clone the [following](https://github.com/Kinovarobotics/ros_kortex) repository:

   ```bash
   git clone https://github.com/Kinovarobotics/ros_kortex
   ```

* Build the necessary packages and source the workspace:

   ```bash
   catkin build kortex_description ocs2_robotic_assets

   source ~/ocs2_ws/devel/setup.bash
   ```

* Convert the xacro file to urdf format:

   ```bash
   rosrun xacro xacro -o $(rospack find ocs2_robotic_assets)/resources/mobile_manipulator/kortex/urdf/gen3_robotiq_2f_85.urdf $(rospack find 
   kortex_description)/robots/gen3_robotiq_2f_85.xacro
   ```

* Copy all meshes from `kortex_description` to `ocs2_robotic_assets/resources` directory:

  - For the **Gen3** arm:
     ```bash
     cp -r $(rospack find kortex_description)/arms/gen3/7dof/meshes $(rospack find ocs2_robotic_assets)/resources/mobile_manipulator/kortex/meshes
     ```

  - For the **Robotic-2F-85** gripper:
     ```bash
     cp -r $(rospack find kortex_description)/grippers/robotiq_2f_85/meshes/visual $(rospack find ocs2_robotic_assets)/resources/mobile_manipulator/kortex/meshes/visual

     cp -r $(rospack find kortex_description)/grippers/robotiq_2f_85/meshes/collision $(rospack find 
     ocs2_robotic_assets)/resources/mobile_manipulator/kortex/meshes/collision
     ```    
 
* Replace the meshes locations in the robot's urdf from `kortex_description/arms/gen3/7dof/` to `ocs2_robotic_assets/resources/mobile_manipulator/kortex/`.

* Replace all arm joint types from **continuous** to **revolute** with high joint limits.

* Add a root link and a root (fixed) joint.
