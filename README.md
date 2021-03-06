# Easy GATE Installation
[![Easy GATE](https://img.shields.io/badge/Easy%20GATE-v1.1-brightgreen.svg)](https://github.com/Alxaline/Easy-GATE-Installation)
![platform](https://img.shields.io/badge/plateform-Linux-lightgrey.svg)
![APMLicense](https://img.shields.io/badge/licence-MIT-green.svg)

<p align="center"> <b>
  You want to install GATE and you don't know how to do it ? You are in the right place !!!
</b></p>

<p align="center">
  <img width="477" height="369" src="https://github.com/Alxaline/Easy-GATE-Installation/blob/master/images/logo_EG.png">
</p>
<p align="justify">
GATE is an advanced opensource software developed by the international OpenGATE collaboration and dedicated to numerical simulations in medical imaging and radiotherapy. It currently supports simulations of Emission Tomography (Positron Emission Tomography - PET and Single Photon Emission Computed Tomography - SPECT), Computed Tomography (CT), Optical Imaging (Bioluminescence and Fluorescence) and Radiotherapy experiments. Using an easy-to-learn macro mechanism to configurate simple or highly sophisticated experimental settings, GATE now plays a key role in the design of new medical imaging devices, in the optimization of acquisition protocols and in the development and assessment of image reconstruction algorithms and correction techniques. It can also be used for dose calculation in radiotherapy experiments.

The installation of GATE is tedious, time consuming and may seem complicated for a novice user. In order not to discourage a novice user to apprehend the formidable tool GATE is, you can use the script provided here which will install absolutely all the necessary files. All you have to do is comply the following instructions. The compilation is long, so don't be afraid !
For more advance users, the script also allows you to install cluster tools with HTcondor (only for Ubuntu distro).
</p>

The script has been tested on : 
- Ubuntu 18.04
- Ubuntu 16.04 
- openSUSE Leap 15.0
- Fedora 29
- Centos 7 (required cmake 3.3 or higher)

If you want the tool available for other distributions, please contact me ! 
</br> 

Some informations : 
- If you want to know more about GATE, please refer to [the official webpage of GATE](http://www.opengatecollaboration.org/).<br/>
- GATE User's Guide is available on [Wiki OpenGATE](http://wiki.opengatecollaboration.org/index.php/Users_Guide).<br/>
- Before using this tool on your system it would be interesting to know about the possibility to use an image of the vGATE 9.0, virtual machine equipped with all the necessary software for running GATE simulations. Please refer to [the official vGate 9.0 webpage](https://opengate.readthedocs.io/en/latest/compilation_instructions.html)<br/>
 
Report bugs to the author [Alexandre CARRE](mailto:alexandre.carre@gustaveroussy.fr)<br/>
NB : use this script at your own risk.


# Requirements
- an internet connection.
- 13 GB of free hard disk space 
- sudo privilege.

# Installation & Instruction

<p align="center">
  <img width="401" height="293" src="https://github.com/Alxaline/Easy-GATE-Installation/blob/master/images/terminal_EG.png">
</p>

## First method
Open a terminal:
```
git clone https://github.com/Alxaline/Easy-GATE-Installation.git
cd Easy-GATE-Installation
source easy_gate.sh
```
## Second method
Download ZIP directly from [the github repo](https://github.com/Alxaline/Easy-GATE-Installation)
then open a terminal:
```
unzip Downloads/Easy-GATE-Installation.zip
cd Easy-GATE-Installation
source easy_gate.sh
```

# How to run GATE after installation? 
Source Gate:
```
gate90
```
Then:
```
Gate
```

# Cluster tools (optional for Ubuntu distro)
For information on How to use Gate on a Cluster, please refer to [the official users guide](http://wiki.opengatecollaboration.org/index.php/Users_Guide:How_to_use_Gate_on_a_Cluster)
## Installation
After the installation of GATE the script will ask you if you want to install cluster tools. In this case, respond "Yes". The script will then install cluster tools (jobsplitter, filemerge) and HTcondor. For non expert users, we recommand you to answer "yes" for the HTcondor prompt GUI.
## How to use HTcondor ?
For information about HTcondor, please refer to [the official documentation of HTcondor](http://research.cs.wisc.edu/htcondor/manual/v8.6/index.html).<br/>
### First step:
You need to export two environment variables:
```
export GC_DOT_GATE_DIR=/somedir/
```
if default path installation:
```
export GC_GATE_EXE_DIR=/usr/local/GATE/Gate-9.0-install/bin
```
if personnalize path installation:
```
export GC_GATE_EXE_DIR=/somedir/GATE/Gate-9.0-install/bin
```
The first variable indicates the location of a hidden directory called .Gate. The directory will contain the split macros for each part of the simulation. Even when splitting the same macro several times, a new directory will be created for each instance (with an incremental number).
The second environment variable indicates the location of the job splitter executable. (you don't have to modify it)
### Second step:
Execute from your macro path this command:
```
../somedir/GATE/Gate-9.0/cluster_tools/jobsplitter/gjs  -numberofsplits N -clusterplatform condor -condorscript ../somedir/GATE/Gate-9.0/cluster_tools/jobsplitter/script/condor.script  your_file.mac
```
The job splitter will subdivide the simulation macro into fully resolved, non-parameterized macros. In this case there are N such macros. Remplace N by the number of macros that you want. They are located in the .Gate directory, as specified by the GC_DOT_GATE_DIR environment variable.
### Third step:
Execute the main submit files create in your_file.mac folder to start clustering:
```
condor_submit your_file.submit
```
### optional step:
If you want to merge your file after simulation, please refer to [the official users guide](http://wiki.opengatecollaboration.org/index.php/Users_Guide:How_to_use_Gate_on_a_Cluster)

# Information
## Where is installed GATE?
If you use default path installation, GATE is installed in:
```
/usr/local
```
## What this script will install ?
- Package Requirements 
- ROOT 6.20/04
- Geant4 10.6.p01
- InsightToolkit 5.0.1
- Gate V9.0 
- Cluster tools / HTcondor (optional for Ubuntu distro)

## Doubt about quality of the installation ?
if you have any doubt about the quality of the installation and want to remove it.
### First remove the installation folder
```
cd /usr/local (default path) or cd /somedir (personalize path)
sudo rm -R GATE
```
### Second remove the environnement variable
The script will add the environnement variable to your .bashrc:
```
gedit ~/.bashrc
```
Remove the line at the end:
```
alias gate90="source /usr/local/GATE/gate_env.sh" (default path) or source alias gate90="source /somedir/GATE/gate_env.sh" (personalize path)
```