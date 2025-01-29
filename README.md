# Baseline-Lidar-assisted-Controller
A reference baseline lidar-assisted wind turbine controller for the wind energy community. 

The code uses Bladed style interface, which is responsible for exchanging variables between the OpenFAST executable and the external controllers compiled as
Dynamic Link Library(DLL).  The functions of each DLL is described below:

WRAPPER.dll: The master (wrapper) DLL.  It calls sub-DLLs by a specific sequence specified in the "WRAPPER.IN" input file.
LDP_v1.dll:     The LDP module reads in LOS measurements from lidar and estimates the rotor effective wind speed, which will eventually be written to the avrSWAP array.
FFP_v1.dll:     The FFP module reads in the rotor effective wind speed from the avrSWAP array, then filter the signal and shifts it in time.  It eventually returns the feed-forward pitch time derivative (rate), which is written into the avrSWAP array.     
ROSCO.dll:   The ROSCO.  Version 2.6.0 controller, https://github.com/NREL/ROSCO  by NREL.  The pitch controller is modified to accept the pitch forward rate signal.

Author: Feng Guo from Flensburg University of Applied Sciences, funded by LIKE -- Lidar Knowledge Europe, grant agreement No. 858358.   
Target: This code aims to provide a reference Lidar-assisted control package for the community.  Please cite the following paper if this code is helpful for your research:
"Guo, Feng, David Schlipf, and Po Wen Cheng. "Evaluation of lidar-assisted wind turbine control under various turbulence characteristics." Wind Energy Science 8.2 (2023): 149-171.  " for more details.   
    
! License: MIT License
!  Copyright (c) 2022 Flensburg University of Applied Sciences, WETI

# How to Compile
We recommend to use "Cmake"+"Visual Studio"+"Intel Fortran Compiler".

The "Cmake" GUI-based version is freely available from: https://cmake.org/download/

Step1: Use Cmake to generate Visual Studio project, remember to ensure "CMakeLists.txt" and the "src" folder are in the same folder. See the tutorial here: https://cmake.org/runningcmake/
Step2: Compile using visual studio. 

Currently, the following combinations have been tested:

Visual Studio 2015 Community+Intel Fortran Compiler 2019.
Visual Studio 2017 Community+Intel Fortran Compiler 2019(available here: https://www.intel.com/content/www/us/en/developer/articles/tool/oneapi-standalone-components.html#fortran).

The pre-compiled DLLs in the "Release" folder are compiled using Visual Studio 2015 and Fortran compiler 2019.  If your system reports the error that the DLL file could not be found, installing Visual Studio 2015 or a newer version may solve the issue. 

# Examples
Example files will be added soon

# For collaborators
When you make new DLLs or modify one of the DLLs, and you want to push the source code, please only push the "CMakeLists.txt" file and the "src" folder containing all source codes.


