## distortionpipeline_aws_f1
This project is to show case a sample Xilinx Vitis project running on AWS F1 instance. This is a continuation of my previous work of the same nature but being implemented on the Xilinx embedded platform (e.g., ZCU104 etc.). In this project, I simply transplant the previous work to the AWS F1 cloud computing platform, which runs **Vitis 2021.1**. I am grateful to the organisers of the 2022 XACC Winter School, in particular, Mario and Cathal, for their kind help.

## Create a Vitis project

* Use this [link](https://xilinx.github.io/xup_compute_acceleration/setup_xup_aws_workshop.html) to set up a link to the AWS F1 instance
* Use this [link](https://xilinx.github.io/xup_compute_acceleration/setup_aws.html) to configure your AWS F1 instance
* We need to install some OS packages, and install the Vitis Accelerated Libraries, following the below steps.

***Open a terminal and run***

```
sudo yum install opencv opencv-core opencv-devel opencv-python libxml2 libxml2-devel -y
```
***Install Vitis Accelerated Libraries in your Vitis IDE*** 

Since Vitis 2020.1 the [Vitis Accelerated Libraries](https://github.com/Xilinx/Vitis_Libraries) can be installed directly from the GUI.

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
<img src="https://github.com/Zhijun1/distortionpipeline_aws_f1/blob/main/img/installation_path.png" alt="installation_path"  width="900" height="430">
</p>

4. Click **OK** to finish

***Edit local repository***

We need to make a few editions in the local repository to use the libraries in AWS F1.

1. Open a new terminal
2. Open ```xf_headers.hpp``` to edit using Visual Code Studio
```
gedit ~/.Xilinx/Vitis/2021.1/vitis_libraries/vision/L1/include/common/xf_headers.hpp &
```
3. Comment line 26 in the file ```xf_headers.hpp```

```
//#include "opencv2/imgcodecs/imgcodecs.hpp"
```

4. Save the file
5. Go back to the terminal and open ```library.json``` using Visual Code Studio
```
gedit ~/.Xilinx/Vitis/2021.1/vitis_libraries/vision/library.json &
```

6. In the ```library.json``` file, replace from line 10 to 30 with the following

```
"host": {
"compiler": {
        "includepaths": [
            "LIB_DIR/ext/xcl2/",
            "LIB_DIR/L1/include",
            "/usr/include/opencv"
        ]
    },
    "linker" : {
        "libraries" : [
            "xml2",
            "opencv_core",
            "opencv_imgproc",
            "opencv_features2d",
            "opencv_flann",
            "opencv_video",
            "opencv_calib3d",
            "opencv_highgui"
        ]
    }
}
```

We have added /usr/include/opencv in the includepaths. We have also removed opencv_videoio and opencv_imgcodecs and include xml2 in libraries

7. Save the file
8. You can check the edited files here







* Follow this [tutorial](https://xilinx.github.io/xup_compute_acceleration/Vitis_intro-1.html) to create a new Vitis project
* 

