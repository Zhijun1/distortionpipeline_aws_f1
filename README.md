## distortionpipeline_aws_f1
This project is to show case a sample Xilinx Vitis project running on AWS F1 instance. This is a continuation of [my previous work](https://github.com/Zhijun1/distortionpipeline) of the same nature but being implemented on the Xilinx embedded platform (e.g., ZCU104 etc.). In this project, I simply transplant the previous work to the AWS F1 cloud computing platform, which runs **Vitis 2021.1**. I am grateful to the organisers of the 2022 XACC Winter School, in particular, Mario and Cathal, for their kind help.

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
8. You can check the edited files [here](https://github.com/Zhijun1/distortionpipeline_aws_f1/tree/main/docs)

***Create Vitis application using the library***

Now we are ready to take reference of the Stereopipline example in Vitis L3 library for implementing the Barrel undistortion of the fisheye camera images. 

1. In Vitis GUI select **Create Application Project**
2. Select **AWS F1 platform** and click **Next **
3. Give an Application Project name like, **distortion** and click **Next**
4. Expand **Vitis Vision Library > L3 > examples** and select **Xilinx Stereopipeline L3 Test** (the following figure is for illustration purpose and the file selected is not correct)
<p align="middle">
<img src="https://github.com/Zhijun1/distortionpipeline_aws_f1/blob/main/img/thr_app.png" alt="thr_app"  width="900" height="440">
</p>

5. Click **Finish**
6. Explore the project and notice that source code and Hardware functions are automatically included

## Step 7 below is very Important

7. You need to check [my previous Barrel undistortaion site](https://github.com/Zhijun1/distortionpipeline) in order to change the codes of the refernece design


8. Build **Emulation-Software**
9. Run Emulation-SW by using ```Run > Run Configurations```... This is to verify the design logic, you can also check the run time of a CPU.

10. Then you should subsequently build **Emulation-Hardware**, and run it. This is to estimate the resources and time. The process takes about 10 minutes.
11. Then you should build **Hardwar**, and run it. This is to implement the project on the cloud hardware. The compilation process takes about 2 hours.

# Outcome
1. The original photo from a fisheye camera with Barrel distortion

<p align="middle">
<img src="https://github.com/Zhijun1/distortionpipeline_aws_f1/blob/main/img/frame_distorted.png" alt="frame_distorted"  width="720" height="540">
</p>

2. The undistorted photo

<p align="middle">
<img src="https://github.com/Zhijun1/distortionpipeline_aws_f1/blob/main/img/hls_out.png" alt="hls_out"  width="720" height="540">
</p>

*Note:* 

1. The above undistorted photo is an outcome from my embedded undistortion package as shown in my github. The AWS F1 instance generates the following gray-level photo after step 7 modification which was based on the codes saved in my laptop (I believe if you modify the original stereopipeline code based on the embedded undistortion package in my github, your modified package may generate the coloured undistorted photo). I simply do not have enough time to modify the code again. 

2. The analysis of the software emulation shows the time for the undistortion is around 2500ms, while the hardware emulation shows the time for the undistortion is around only 5ms (both in the case that the output photo is gray level). A more detailed estimation of the time and resources will be added in the future. 

<p align="middle">
<img src="https://github.com/Zhijun1/distortionpipeline_aws_f1/blob/main/img/hls_output.png" alt="hls_output"  width="720" height="540">
</p>



 


