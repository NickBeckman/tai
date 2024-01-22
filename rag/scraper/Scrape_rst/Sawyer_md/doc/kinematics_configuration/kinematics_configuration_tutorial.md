# Kinematics Configuration

In this section, we will examine some of the parameters for configuring kinematics for your robot.

## The kinematics.yaml file

The kinematics.yaml file generated by the MoveIt Setup Assistant is the primary configuration file for kinematics for MoveIt. You can see an entire example file for the Panda robot in the {panda_codedir}`panda_moveit_config GitHub project <config/kinematics.yaml>`:

```
panda_arm:
  kinematics_solver: kdl_kinematics_plugin/KDLKinematicsPlugin
  kinematics_solver_search_resolution: 0.005
  kinematics_solver_timeout: 0.05
  kinematics_solver_attempts: 3
```

### Parameters

The set of available parameters include:
: - *kinematics_solver*: The name of your kinematics solver plugin. Note that this must match the name that you specified in the plugin description file, e.g. `example_kinematics/ExampleKinematicsPlugin`
  - *kinematics_solver_search_resolution*: This specifies the resolution that a solver might use to search over the redundant space for inverse kinematics, e.g. using one of the joints for a 7 DOF arm specified as the redundant joint.
  - *kinematics_solver_timeout*: This is a default timeout specified (in seconds) for each internal iteration that the inverse kinematics solver may perform. A typical iteration (e.g. for a numerical solver) will consist of a random restart from a seed state followed by a solution cycle (for which this timeout is applicable). The solver may attempt multiple restarts - the default number of restarts is defined by the kinematics_solver_attempts parameter below.
  - *kinematics_solver_attempts*: The number of random restarts that will be performed on the solver. Each solution cycle after the restart will have a timeout defined by the kinematics_solver_timeout parameter above. In general, it is better to set this timeout low and fail quickly in an individual solution cycle.

### The KDL Kinematics Plugin

The KDL kinematics plugin wraps around the numerical inverse kinematics solver provided by the Orocos KDL package.
: - This is the default kinematics plugin currently used by MoveIt
  - It obeys joint limits specified in the URDF (and will use the safety limits if they are specified in the URDF).
  - The KDL kinematics plugin currently only works with serial chains.

### The LMA Kinematics Plugin

The LMA (Levenberg-Marquardt) kinematics plugin also wraps around a numerical inverse kinematics solver provided by the Orocos KDL package.
: - It obeys joint limits specified in the URDF (and will use the safety limits if they are specified in the URDF).
  - The LMA kinematics plugin currently only works with serial chains.
  - Usage: `kinematics_solver: lma_kinematics_plugin/LMAKinematicsPlugin`

### The Cached IK Plugin

The Cached IK Kinematics Plugin creates a persistent cache of IK solutions. This cache is then used to speed up any other IK solver. A call to an IK solver will use a similar state in the cache as a seed for the IK solver. If that fails to return a solution, the IK solver is called again with the user-specified seed state. New IK solutions that are sufficiently different from states in the cache are added to the cache. Periodically, the cache is saved to disk.

To use the Cached IK Kinematics Plugin, you need to modify the file `kinematics.yaml` for your robot. Change lines like these:

```
manipulator:
  kinematics_solver: kdl_kinematics_plugin/KDLKinematicsPlugin
```

to this:

```
manipulator:
  kinematics_solver: cached_ik_kinematics_plugin/CachedKDLKinematicsPlugin
  # optional parameters for caching:
  max_cache_size: 10000
  min_pose_distance: 1
  min_joint_config_distance: 4
```

The cache size can be controlled with an absolute cap (`max_cache_size`) or with a distance threshold on the end effector pose (`min_pose_distance`) or robot joint state (`min_joint_config_distance`). Normally, the cache files are saved to the current working directory (which is usually `${HOME}/.ros`, not the directory where you ran `roslaunch`), in a subdirectory for each robot. Possible values for `kinematics_solver` are:

- *cached_ik_kinematics_plugin/CachedKDLKinematicsPlugin*: a wrapper for the default KDL IK solver.
- *cached_ik_kinematics_plugin/CachedSrvKinematicsPlugin*: a wrapper for the solver that uses ROS service calls to communicate with external IK solvers.
- *cached_ik_kinematics_plugin/CachedTRACKinematicsPlugin*: a wrapper for the [TRAC IK solver](https://bitbucket.org/traclabs/trac_ik). This solver is only available if the TRAC IK kinematics plugin is detected at compile time.
- *cached_ik_kinematics_plugin/CachedUR5KinematicsPlugin*: a wrapper for the analytic IK solver for the UR5 arm (similar solvers exist for the UR3 and UR10). This is only for illustrative purposes; the caching just adds extra overhead to the solver.

See the [Cached IK README](https://github.com/ros-planning/moveit/blob/master/moveit_kinematics/cached_ik_kinematics_plugin/README.md) for more information.

## Position Only IK

Position only IK can easily be enabled (only if you are using the KDL Kinematics Plugin) by adding the following line to your kinematics.yaml file (for the particular group that you want to solve IK for):

```
position_only_ik: True
```