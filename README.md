# Object-Detection-In-Video-Using-Tensorflow-on-Windows
These are simple instructions that I used for running an object detection app in a video stream on your Windows PC using Tensorflow. The instructions in the official repository are somewhat incomplete and quite linux-specific.

Here is the overview for a simple Windows PC installation (I did it on Windows 7 Professional), without GPU support and without using Anaconda :

<image>

1. Install Python 3.6
Go to https://www.python.org/downloads/ and download the Windows version and install it. Please make sure that you can run
c:\python36> python -V and it shows "Python 3.6" or better.

You can use Anaconda to install multiple versions of Python. For one, Anaconda makes my PC crawl. Also, I see no need of multiple versions of Python (unless I am also using Python 2.7). So I just install one version of Python natively. 

2. Install tensorflow 1.8
This would be easy once you have Python installed.
Python -m pip install --upgrade tensorflow

Again, you can install tensorflow via Anaconda, if you went that route in #1.
conda install --upgrade tensorflow.

And obviously, things would be a bit more complicated for you if you're using the NVIDIA GPU support. For that you'd need to install NVIDIA CUDA libraries. See https://www.tensorflow.org/install/install_windows for details. 

3. Install supporting libraries
The documentation says the following libraries are required. In my experience, you only need a few. You can always include the "missing" libraries, if your compiler starts to complain about a missing library.

pillow: python -m pip install pillow
lxml: python -m pip install lxml
jupyter: python -m pip install jupyter
matplotlib: python -m pip install matplotlib
cynthon (optional)
cocoapi (optional)
tfslim (optional)
python-tk (optional)

4. Install protoc and compile protobuf
Download protoc from https://github.com/google/protobuf/releases. I used version 3.5.1 (protoc-3.5.1-win32.zip). Unzip into a known directory. There would be a file called protoc.exe. The instructions in Tensorflow documentation don't work with Windows. Compile one .proto file at a time.

<path-to>protoc.exe object_detection\protos\<one-file-name>.proto --python_out=.

The .proto files, once compiled with your protoc compiler will create corresponding .py file. Some file may not compile and you'd run into compilation issues. It is generally OK.

5. Update PYTHONPATH
I think this is an optional step, but it is generally easier to specify the Python paths in the user variables in Windows control panel. Control Panel -> System and Security -> System -> Advanced System Settings -> Environment Variables -> user variables.
C:\tensorflow\models; C:\tensorflow\models\research; C:\tensorflow\models\research\slim;C:\tensorflow\models\research\object_detection;

6. Run Object-Detection-Demo on one image
Since you installed jupyter notebook, you can run this by the command:
jupyter notebook object_detection_tutorial.ipynb

Another option is to download this file (in the same directory) as a .py file by clicking on "download as". But you'd need to change the output into a matplotlib rendering, instead of the default rendering from the jupyter notebook.

Assuming you downloaded the file as object_detection_tutorial.py, and made the changes to matplotlib rendering, you can simply run it as
python object_detection_tutorial.py

Regardless of how you run it, the default run of this program will tag the two image files in the images folder - in one case it will tag (and box) dogs, and in the other case, it will tag (and box) people and kites.

If you reached this point, rejoice. You're more than half way there.

7. Install Computer Vision (OpenCV3.4)
I used the current-latest version (3.4.1). Simply download the Windows installer from Sourceforge. The link is on this page: https://opencv.org/opencv-3-4-1.html

8. Modify the sample code - use the code I have provided. The default code is slow for videos.
The default changes got me to a refresh rate of 1 in ~15 seconds. I made some changes to the code, and it looks like the version of the sample that was release a few months ago. I now can see a refresh rate of ~2/second.

9. Run object detection on live video
Enjoy watching the default model detect and tag differnt things! Now you can compare to see how the different models behave (check out the model zoo: https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md).

Or try training your current model. I'll post the instructions in the next project.
