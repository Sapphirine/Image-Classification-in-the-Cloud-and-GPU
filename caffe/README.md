#G Classification

For more detailed information please visit the website http://bigdatagclass.tumblr.com/

For the initial steps look below, but the more detailed steps are in the website above

Step by Step Guide

A. How to Setup and get GPU/CUDA running in your machine

We spent a significant amount of time getting GPU and CUDA to work well. To prevent the graders and future students from having these issues, the first section of the guide will focus on GPU / CUDA setup and then move on to the deep learning framework setup and then run the algorithms we ran. We talk about more about CUDA and setting up our deep network Caffe etc since this was not done in homeworks nor taught in class.

1. We recommend you to a use a Ubuntu linux machine 14.04, preferably with another computer and network where you can SSH through. We need the SSH from another computer because we will be manipulating the device drivers in the machine which will pretty much turn on/off the x-server and turn off the display in the machine. The reason we recommend Ubuntu is like some of the frameworks which we will be looking at like Caffe and cuda-convent work and compile more easily with Linux rather than windows. This should be a physical machine in which you need to have root privileges (they are needed to run some of the tests). It shouldn’t be a virtual machine as CUDA and GPU tests may be very funky on virtual machines, and virtual machines in any case are not the best for performance tests.

2.Now ensure that your graphics card has CUDA capabilities, by checking if your graphics card name is supported in the following link

https://developer.nvidia.com/cuda-gpus

3. Remember to not say yes to any Linux updates to turn off all Ubuntu linux updates because Linux updates can bring new linux drivers that can potentially alter the drivers of the machine that will be setup.

4. Now install ssh on your main machine (which you want the GPU to be running on), and have another computer (say another laptop) to ssh to your machine. You install ssh on your main machine by running sudo apt-get install openssh-server and also install sudo apt-get install openssh-client on your main machine as well as your laptop.

5. So first let us try running this command nvidia-smi. It may potentially throw an error like the following 

image

The reason it’s giving this error is that nvidia is not the driver that is currently running the machine. We noticed that in the latest Ubuntu updates nouveau drivers came through. Before running the following commands this use another computer to ssh to your current machine and run it from that machine. These drivers were rather dysfunctional with nvidia drivers. So one step is if they exist, and you can check if the drivers are installed with dpkg –get-selections | grep nouveau. This gives us the installed nouveau drivers. Now once we have got the list of nouveau drivers let us remove them step by step.

image

 sudo apt-get —purge remove (the name of nouveau driver). Do so as long as this doesn’t give any error.

6. Now we will attempt to install the nvidia display driver. Before doing so it’s important to see what Nvidia kernel module you are running currently, you do that the following command “cat /proc/driver/nvidia/version”. This is also shown in the following screenshot.

image

Now you realize what version of display driver you need to install. You need to install the display driver matches the kernel module.

7. So now go ssh to your main machine and run the following commands

sudo apt-get —purge remove nvidia-* // This removes any current nvidia display drivers

sudo killall Xorg // This kills the x – server if running, if there is an error in this message you don’t need to worry about it.

sudo service lightdm stop // lightdm, is the display manager in Ubuntu linux desktop, this turns the display manager off.

If you see your main screen blank out, that is normal when switching drivers, nothing really to be concerned about there. This is exactly what shutting down display manager does. So now we install the display driver that matches the kernel driver version 304. There are couple of ways to do so in linux one is download the driver .run file yourself and then run it manually. The other way is to use apt-get and just run apt-get nvidia-304 . This will install 304-125 by default. You may need to reboot the computer to make sure this is the case.

8. Ensure your new display driver is installed, you can be sure this is the case by looking at the packages installed. One way to do that is the following. By running the following command you can ensure that the nvidia display driver is installed.

image

9. Now let us re-run. The nvidia-smi command if you get a following error as such as this

               Or an error like this

Failed to initialize NVML: Unknown Error

                              Or like this error

NVIDIA: API mismatch: the NVIDIA kernel module has version 304.116,

but this NVIDIA driver component has version 319.76.  Please make

sure that the kernel module and all NVIDIA driver components

have the same version.

Most likely if you get any of the above errors you have not installed the right Nvidia-display version to match the kernel version. Look at the previous step again and make sure the kernel and display driver match.

10.Now lets rerun the nvidia-smi -a command, and you will see if stuff is properly installed one will get a different result. Now if you run the command look at the following output, 

image

11. Now we now the Nvidia display driver works, next lets download CUDA drivers. The CUDA drivers are https://developer.nvidia.com/cuda-toolkit-50-archive . We downloaded both CUDA 5 and CUDA 5.5. so once this is done. Use the following code to extract the cuda downloaded run file and place it in the nvidia_installers folder

8.  mkdir ~/Downloads/nvidia_installers;

9.  cd ~/Downloads

10../cuda_5.0.35_linux_64.run -extract=~/Downloads/nvidia_installers;

Copy the results in to a folder and there should be samples and toolkit there something like below. Ignore the driver that is below (installing that driver which was incompatible with Nvidia kernel driver caused lots of incompatibility issues too), but run the cudtoolkit .run file, you need to add the chmod +x option to both cudatoolkit and samples file first, then just execute the toolkit file first and the samples file next.

image

This should install paths to your /usr/local/cuda-5.0 directory. Now add these files to the cuda-5.0 directory.

Add these paths to your bashrc file, and restart it by the source bashrc option.

export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-5.0/lib64

export PATH=/usr/local/cuda-5.0/bin:$PATH

export PATH=/usr/include/python2.7:$PATH

12. Now the initial cuda install is finished. You can try running one of the CUDA samples, a basic one is the device query samples. So browse to the /usr/local/cuda-5.0/samples/1_Utilities/deviceQuery directory. There will be a makefile present in the directory. Run this make file. If you run the ./deviceQuery sample 

image

When you execute device query, you get back the error message “no CUDA-capable device is detected”. If you do get this error message either you have the wrong version or don’t have the CUDA library installed.

This is the right version of libcuda for me, but it could be you have the wrong version. If it is the wrong version that doesn’t match the display driver and the kernel uninstall it.

image

Then try and install the 304 version. For example below is a download a link for my matching display drive.    

http://www.ubuntuupdates.org/package/core/utopic/restricted/updates/libcuda1-304

This above link for example contains deb files for download. Once you download the deb files and install the libcuda, you repeat the install check you should see libcuda like the following link.

image

After this is installed you need to reboot your machine. Now let us try to run the device query basic CUDA test again now. To do so we go to the /usr/local/cuda-5.0/samples folder as mentioned before and run the device query test.

image

The device query test now works fine, which is like basic the sanity test for GPU calculation.

Installing Caffe

1. This BLAS Is used by Caffe for linear operations. Run the following command to install it sudo apt-get install libatlas-base-dev

 2. Install OpenCV, which is a library for programming some of these computer vision functions. The command to install that is sudo apt-get install libopencv-dev

3. Next install Boost, which is set of C++ libraries that provide a variety of tasks and structures including algebra, multi-threading, etc. Run sudo apt-get install libboost-all-dev

4. Next we install Google protocol buffers, this is used by Caffe sometimes for communication between the different network layers as they can be potentially scaled to different servers also. This is the command to run for this sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev protobuf-compiler

5. Another installation command to run sudo apt-get install libprotobuf-dev libleveldb- 

 6. dev libsnappy-dev libopencv-dev libboost-all-dev libhdf5-serial-dev

 7. Several additional python libraries are also required, before doing that we install pip for python, pip is a package management system used to install and manage software package written in python.

 8. sudo apt-get install python3-setuptools

 9. sudo easy_install3 pip

10. We install cython which are C extensions for Python. sudo pip install Cython>=0.19.2

11. Fundamental package for python for N Dimensional arrays with Python. Sudo pip install numpy>=1.7.1

12. Package for scientific computing with python. Sudo pip install numpy>=1.7.1

 13. Tools for machine learning in python. sudo pip install scikit-image>=0.9.3

 14. Sudo apt-get install python-dev

 15. Sudo prp install scikit-learn>=0.14.1

 16. sudo pip install matplotlib>=1.3.1

 17. sudo pip install ipython>=1.1.0

 18. sudo pip install h5py>=2.2.0

 19. sudo pip install leveldb>=0.191

 20. sudo pip install networkx>=1.8.1

 21. sudo pip install nose>=1.3.0

 22. sudo pip install pandas>=0.12.0

 23. sudo pip install python-dateutil>=1.4,<2

 24. sudo pip install protobuf>=2.5.0

 25. sudo pip install python-gflags>=2.0

 26. Next copy the makefile.config.example to the config cp Makefile.config.example Makefile.config

 27. Next open and edit the Makefile.config and set the CUDA_DIR to the base directory CUDA is installed in and comment out the arch_code of compute_50 of two lines. This is shown in the image below

image28. Change the PYTHON_INCLUDE if necessary to run this as follows

image

29. Make all

30. Make test

31. Make runtest

32. These should work and when your make runtest you should see all the tests completed successfully

image33. To import the caffe Python module after completing the installation, add the module directory to  your $PYTHONPATH by export PYTHONPATH=/path/to/caffe/python:$PYTHONPATH or the like. You should not import the module in the caffe/python/caffe directory!

34. Now since that is done let us try running one of the algorithms using a python script.

35. Lets first do an easier example to get started with using the pre-trained caffe net model. Caffe provides a pre-trained model with its own images, after this is working well we will move on to how train our own images. So what we show in the next 6 steps or so, is how to test your model, if the training is already done. We will show how we created our own model, using two different algorithms after this easy example which makes one get started

36. Download Caffe’s model by running in the root caffe directory ./scripts/download_model_binary.py models/bvlc_reference_caffenet

37. So in the below screenshot you can see these python lines se the deep learning model, then the model of training is set and finally the image is shown.

MODEL_FILE = ‘../models/bvlc_reference_caffenet/deploy.prototxt’ # this is the model file

PRETRAINED = ‘../models/bvlc_reference_caffenet/bvlc_reference_caffenet.caffemodel’ # this is the trained model

IMAGE_FILE = ‘images/basketball.jpeg’ # this is the image

38. Then the prediction class is the finally called and it predicts using the pre-defined classes that exist in the Caffe model. In the next part we will talk about how we change the model to our own model and how we can modify the txt files to use the predefined categories in the yahoo dataset. 

image

39. Let us know look at the prototxt model file. The prototxt consists of several different layers and should be present in the existing implementation of caffe. 

image

Since now the basic image case is shown and can be extended to multiple images, let’s move on to some other scripts

40.

First download and save images to your computer from the massive dataset. There are R scripts provided in the github submission to aid this process.

/path/to/yahoo_set/train/image_2.JPEG

/path/to/yahoo_set/test/image_1.JPEG

The next following scripts will work in stages, one stage will push data ready for the next intermediate stage.

41. Now we will run the following script with the caffe data. The first step in building this training model is resizing the images and storing the resized images in a temporary location. It’s important that one needs to create these paths correctly. We had several places we needed to change the path to get this deep learning algorithm working correctly. The paths needed to be all made and all changed appropriately for the basic tests to work correctly.

image

image

The above scripts runs resize if necessary and places for the next intermediary step in the $EXAMPLE folder. The program converts a set of images to a lmdb format by storing them as Datum proto buffers.

Before moving on please ensure the paths you selected were correct and the lmdb (resized images in this new format) are correctly saved in the desired example location.

If one wants to understand this better the heart of the transformation lies in the below C++ function, ReadImageToDatum

image

42.Moving on to the next stage, the model requires us to subtract the image mean from each image, so we have to compute the mean. Tools/compute_image_mean.cpp implements that.

The script to run this is pretty simple assuming you had similar paths that you had before.

image

Diving deeper into technical details again, as you can see the below function collects the different datum image sizes and also calculates a count to divide too and the result is the image mean.

43.

Now its time to train the model which is the prototxt file. In that file make sure the paths are appropriately changed to match the path you had created in the above few steps

The above model file is present in models/bvlc_reference_caffenet

44.

After this step you should get a fully trained model, that you can now use for testing, using a similar script to what we wrote before. One would change the pretrained parameter in that script in Step 39, so that one would be ready for something new. Once the training starts you would expect to be see screenshot similar to this 

At the end you will have end up with accuracy measurements as follows

45. In this guide I have tried to give you a detailed view on how to reproduce this, but GPU and Deep networks are not a joke. They are courses in other university just on Deep learning or just on GPU. So if I have missed anything and any of are stuck on some error please feel free to contact us for any troubleshooting issues.

Classification with Mahout

Let us have a quick word about mahout. Since this was covered very heavily in assignments and lectures we are going to quickly breeze through this section. But the main idea was to use trainnb on the already given vectors and train.classifier.sgd on already given vectors too. The result were confusion matrixes with accuracy percentages.


