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

1. In Vitis GUI click Xilinx > Libraries...

<p align="left">
<img src="https://github.com/Zhijun1/distortionpipeline_aws_f1/blob/main/img/install_menu.png" alt="install_menu"  width="400" height="210">
</p>

2. Click **Download** button to get a local copy of the GitHub repository

<p align="middle">
<img src="https://github.com/Zhijun1/distortionpipeline_aws_f1/blob/main/img/download_libs.png" alt="download_libs"  width="900" height="410">
</p>

3. After a few seconds the libraries are installed. Note the branch used and the local directory where the libraries are installed

<p align="middle">
<img src="https://github.com/Zhijun1/distortionpipeline_aws_f1/blob/main/img/installation_path.png" alt="installation_path"  width="900" height="410">
</p>






* Follow this [tutorial](https://xilinx.github.io/xup_compute_acceleration/Vitis_intro-1.html) to create a new Vitis project
* 

