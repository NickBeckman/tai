

<!--
// @@ Buildsystem macro
function Buildsystem(sections) {
 var dotversion = ".buildsystem."

 // Tag shows unless already tagged
 $.each(sections.show,
 function() {
 $("div" + dotversion + this).not(".versionshow,.versionhide").addClass("versionshow")
 }
 )

 // Tag hides unless already tagged
 $.each(sections.hide,
 function() {
 $("div" + dotversion + this).not(".versionshow,.versionhide").addClass("versionhide")
 }
 )

 // Show or hide according to tag
 $(".versionshow").removeClass("versionshow").filter("div").show()
 $(".versionhide").removeClass("versionhide").filter("div").hide()
}

function getURLParameter(name) {
 return decodeURIComponent(
 (
 new RegExp(
 '[?|&]' + name + '=' + '([^&;]+?)(&|#|;|$)'
 ).exec(location.search) || [,""]
 )[1].replace(/\+/g, '%20')
 ) || null;
}

$(document).ready(function() {
 var activesystem = "catkin";
 var url\_distro = getURLParameter('buildsystem');
 if (url\_distro)
 {
 activesystem = url\_distro;
 }
 $("div.buildsystem").not("."+activesystem).hide();
 $("#"+activesystem).click();
 $("input.version:hidden").each(function() {
 var bg = $(this).attr("value").split(":");
 $("div.version." + bg[0]).css("background-color", bg[1]).removeClass(bg[0])
 });
})
 // -->

 catkin 
 rosbuild 

|  |
| --- |
| (!) Please ask about problems and questions regarding this tutorial on [answers.ros.org](http://answers.ros.org "http://answers.ros.org"). Don't forget to include in your question the link to this page, the versions of your OS & ROS, and also add appropriate tags. |

# Creating a ROS package by hand.

**Description:** This tutorial explains how to manually create a ROS package.  

**Tutorial Level:** INTERMEDIATE   

**Next Tutorial:** [Managing System Dependencies](/ROS/Tutorials/rosdep "/ROS/Tutorials/rosdep")   

 There is a tool for creating ROS [Packages](/Packages "/Packages") ([roscreate-pkg](/roscreate "/roscreate")), but, as you will see, there is nothing actually difficult here. roscreate-pkg prevents mistakes and saves effort, but packages are just a directory and a simple XML file. Now we'll create a new foobar package. This tutorial assumes that we're working in the directory pkgs on your [ROS\_PACKAGE\_PATH](/ROS/EnvironmentVariables "/ROS/EnvironmentVariables"). 
```
pkgs$ mkdir foobar
pkgs$ cd foobar
```
The very first thing we'll do is add our [manifest](/Manifest "/Manifest") file. The manifest.xml file allows tools like [rospack](/rospack "/rospack") to determine information about what your package depends upon. Inside of foobar/manifest.xml put the following: 
```
<package>
  <description brief="example package tutorial">A simple tutorial package</description>
  <author>Your Name Here</author>
  <license>BSD</license>
  <depend package="roscpp" />
  <depend package="std_msgs" />
</package>
```
Now that your package has a manifest, ROS can find it. Try executing the command: 
```
rospack find foobar
```
If ROS is set up correctly you should see something like: /home/user/ros/pkgs/foobar. This is how ROS finds packages behind the scenes. Note that this package now also has dependencies on [roscpp](/roscpp "/roscpp") and [std\_msgs](/std_msgs "/std_msgs"). To see one example of why specifying these dependencies is useful, try executing the following commands [rospack](/rospack "/rospack") commands: 
```
rospack export --lang=cpp --attrib=cflags foobar
rospack export --lang=cpp --attrib=lflags foobar
```
When you run these, rospack looks up the dependencies of foobar and generates the necessary list of includes or linking statements to compile and link the executable. These commands are used by the ROS build system to correctly compile and link your packages despite the modular nature of ROS. You'll probably never have to use these directly since our build system takes care of it for you. However, as you can see, they are reasonably easy use if you want to use a different build system. In order to take advantage of this, we need to make two build files: a Makefile and [CMakeLists.txt](/CMakeLists "/CMakeLists") file. Inside of foobar/Makefile, put: 
```
include $(shell rospack find mk)/cmake.mk
```
This tells make that we're going to use CMake instead of Make to build this package. Now we need the [CMakeLists.txt](/CMakeLists "/CMakeLists") file so that we can use CMake instead. ROS uses CMake for its more powerful flexibility when building across multiple platforms. In foobar/CMakeLists.txt put: 
```
cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)
rosbuild_init()
```
That's all you need to start building a package in ROS. Of course, if you want it to actually start building something, you're going to need to learn a couple more CMake macros. See our [CMakeLists](/CMakeLists "/CMakeLists") guide for more information. 

There is a tool for creating ROS [Packages](/Packages "/Packages") ([catkin\_create\_pkg](/catkin/commands/catkin_create_pkg "/catkin/commands/catkin_create_pkg")), but, as you will see, there is nothing actually difficult here. catkin\_create\_pkg prevents mistakes and saves effort, but packages are just a directory and a simple XML file. Now we'll create a new foobar package. This tutorial assumes that we're working your catkin workspace and sourcing of the setup file is already done. 
```
catkin_ws_top $ mkdir -p src/foobar
catkin_ws_top $ cd src/foobar
```
The very first thing we'll do is add our [manifest](/catkin/package.xml "/catkin/package.xml") file. The package.xml file allows tools like [rospack](/rospack "/rospack") to determine information about what your package depends upon. Inside of foobar/package.xml put the following: 
```
<package format="2">
  <name>foobar</name>
  <version>1.2.4</version>
  <description>
  This package provides foo capability.
  </description>
  <maintainer email="foobar@foo.bar.willowgarage.com">PR-foobar</maintainer>
  <license>BSD</license>

  <buildtool_depend>catkin</buildtool_depend>

  <build_depend>roscpp</build_depend>
  <build_depend>std_msgs</build_depend>

  <exec_depend>roscpp</exec_depend>
  <exec_depend>std_msgs</exec_depend>
</package>
```
See also [this page from catkin tutorial](/catkin/Tutorials/CreatingPackage#ROS.2BAC8-Tutorials.2BAC8-catkin.2BAC8-CreatingPackage.Customizing_the_package.xml "/catkin/Tutorials/CreatingPackage#ROS.2BAC8-Tutorials.2BAC8-catkin.2BAC8-CreatingPackage.Customizing_the_package.xml") for further information on [catkin/package.xml](/catkin/package.xml "/catkin/package.xml"). Now that your package has a manifest, ROS can find it. Try executing the command: 
```
rospack find foobar
```
If ROS is set up correctly you should see something like: /home/user/ros/catkin\_ws\_top/src/foobar. This is how ROS finds packages behind the scenes. Note that this package now also has dependencies on [roscpp](/roscpp "/roscpp") and [std\_msgs](/std_msgs "/std_msgs"). Such dependencies are used by catkin to configure packages in the right order. Now we need the [CMakeLists.txt](/CMakeLists "/CMakeLists") file so that [catkin\_make](/catkin_make "/catkin_make"), which uses CMake for its more powerful flexibility when building across multiple platforms, builds the package. In foobar/CMakeLists.txt put: 
```
cmake_minimum_required(VERSION 2.8.3)
project(foobar)
find_package(catkin REQUIRED roscpp std_msgs)
catkin_package()
```
That's all you need to start building a package in ROS using catkin. Of course, if you want it to actually start building something, you're going to need to learn a couple more CMake macros. See our [CMakeLists.txt](/catkin/CMakeLists.txt "/catkin/CMakeLists.txt") guide for more information. Also always go back to beginner level tutorial ([CreatingPackage](/ROS/Tutorials/CreatingPackage "/ROS/Tutorials/CreatingPackage") and so on) to customize your package.xml and CMakeLists.txt. 
