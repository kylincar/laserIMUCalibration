# Automated LiDAR-IMU Calibration with ICP

I wrote this program as part of my [mastersthesis](https://github.com/gismo141/mastersthesis).

It provides an automated calibration method that uses movement data collected by Inertial Measurement Units (IMU)- and Global Positioning Satellite Systems (GNSS)-sensors to calibrate the mounting-pose of a Light Detection and Ranging (LiDAR)-scanner.

## Background

Unmanned aircraft fulfil dirty, dangerous and demeaning tasks for human beings. Some applications require a map of the environment by consecutively registering point-cloud-data generated by LiDAR-sensors. The registration-process requires a mounting-pose between the LiDAR and NAV sensors (IMU and GNSS). Due to inaccurate measured mounting-poses the registration fails.

## Approach

In this thesis I propose a method for an automated relative extrinsic calibration between the LiDAR and NAV, that uses a non-linear optimisation (Levenberg-Marquardt) to optimize the given mounting-pose. The results show, that the calibration may fail when the point-cloud data suffers from geometric instability, therefore I present different filter-techniques such as covariance-sampling to improve the point-cloud-data. This promising approach needs investigation concerning the parametrization of the proposed techniques.

## Implementation

This repository contains the developed research code. The implementation uses Qt5 for a Graphical User Interface (GUI), VTK for algorithm visualisation and the Point-Cloud-Library (PCL) for point-cloud management as well as the Levenberg-Marquardt implementation from [Dr. Joachim Wuttke](http://apps.jcns.fz-juelich.de/doku/sc/lmfit).

## Installation

### Dependencies

To install the software and its dependencies on Mac OS X, use the package manger [Homebrew](http://brew.sh).

After the installation of Homebrew you should install the software.

```Shell
brew install cmake pcl graphviz doxygen
```

### Fix for CMake and Qt5

When you use Qt5 you need to fix some links according to the [wireshark-documentation](https://github.com/Homebrew/homebrew/issues/29938).

```Shell
brew link --force qt5 && ln -s /usr/local/Cellar/qt5/5.4.1/mkspecs /usr/local/mkspecs && ln -s /usr/local/Cellar/qt5/5.4.1/plugins /usr/local/plugins
```

### Download

Replace `<YOUR_DESTINATION>` with the path where you want to store the source-code (e.g. `~/Development`).

```Shell
git clone git@github.com:gismo141/laserIMUCalibration <YOUR_DESTINATION>
```

```Shell
cd <YOUR_DESTINATION>
mkdir build && cd build
cmake ..
make
```

<!-- ## Usage

### Fly through multiple LiDAR-scans

```Shell
./laserIMUCalibration_noBundle <PATH_TO_FOLDER_WITH_PCD_FILES>
```

This opens the interactive VTK-visualizer with consecutive presentation of each LiDAR-scan. The use can move, rotate and scale the scene with the mouse.

Planned Improvements:

- develop a GUI as filter-interface

### Plot the ICP-fitness-score for different intervals

```Shell
./laserIMUCalibration_noBundle <PATH_TO_FOLDER_WITH_PCD_FILES> <INTERVAL_BETWEEN_SCANS>
```

This launches the ICP-algorithm and calculates the transformation between every LiDAR-scan and its `<INTERVAL_BETWEEN_SCANS>` successor. A small percentage-indicator represents the amount of processed scans divided by the total to provide a little feedback on the calculation-intensive task. While processing, the program writes its results to the semicolon-separated-file `icp_fitness_<INTERVAL_BETWEEN_SCANS>.csv` in the executed folder. The first row is the unix-timestamp of the first scan, the second row is the unix-timestamp of the second scan and the third is the ICP-fitness-score. The fitnessscore is according to the [PCL](http://docs.pointclouds.org/trunk/classpcl_1_1_registration.html#ab26742c383b6f5e86fb96a236fb08728) the sum of the squared distances divided by its total.

An example `icp_fitness_1.csv` may look like:

```csv
timestamp_1;timestamp_2;icp-score
1412242263.910747;1412242264.910452;0.135022
1412242264.010833;1412242265.010031;0.288052
1412242264.110734;1412242265.109657;0.107826
1412242264.210728;1412242265.209419;0.256894
``` -->
