## distortionpipeline_aws_f1
This project is to show case a sample Xilinx Vitis project running on AWS F1 instance. This is a continuation of my previous work of the same nature but being implemented on the Xilinx embedded platform (e.g., ZCU104 etc.). In this project, I simply transplant the previous work to the AWS cloud computing platform. I am grateful to the organisers of the 2022 XACC Winter School, in particular, Mario and Cathal, for their kind help.

## Create a Vitis project

* Use this [link](https://xilinx.github.io/xup_compute_acceleration/setup_xup_aws_workshop.html) to set up a link to the AWS F1 instance
* Use this [link](https://xilinx.github.io/xup_compute_acceleration/setup_aws.html) to configure your AWS F1 instance
* We need to install some OS packages, open a terminal and run
```
sudo yum install opencv opencv-core opencv-devel opencv-python libxml2 libxml2-devel -y
```
Then, install Vitis Accelerated Libraries in your Vitis IDE. Since Vitis 2020.1 the [Vitis Accelerated Libraries](https://github.com/Xilinx/Vitis_Libraries) can be installed directly from the GUI.

In Vitis GUI click Xilinx > Libraries...

<p align="left">
<img src="https://github.com/Zhijun1/distortionpipeline_aws_f1/blob/master/img/install_menu.png" alt="install_menu"  width="400" height="250">
</p>


* Follow this [tutorial](https://xilinx.github.io/xup_compute_acceleration/Vitis_intro-1.html) to create a new Vitis project
* 

