# TrainYourOwnYOLO: Building a Custom Object Detector from Scratch [![license](https://img.shields.io/github/license/mashape/apistatus.svg)](LICENSE)

This repo let's you train a custom image detector using the state-of-the-art [YOLOv3](https://pjreddie.com/darknet/yolo/) computer vision algorithm. For a short write up check out this [medium post](https://medium.com/@muehle/how-to-train-your-own-yolov3-detector-from-scratch-224d10e55de2). 

### Pipeline Overview

To build and test your YOLO object detection algorithm follow the below steps:

 1. [Image Annotation](/1_Image_Annotation/)
	 - Install Microsoft's Visual Object Tagging Tool (VoTT)
	 - Annotate images
 2. [Training](/2_Training/)
 	- Download pre-trained weights
 	- Train your custom YOLO model on annotated images 
 3. [Inference](/3_Inference/)
 	- Detect objects in new images and videos

## Repo structure
+ [`1_Image_Annotation`](/1_Image_Annotation/): Scripts and instructions on annotating images
+ [`2_Training`](/2_Training/): Scripts and instructions on training your YOLOv3 model
+ [`3_Inference`](/3_Inference/): Scripts and instructions on testing your trained YOLO model on new images and videos
+ [`Data`](/Data/): Input Data, Output Data, Model Weights and Results
+ [`Utils`](/Utils/): Utility scripts used by main scripts

## Getting Started

### Requisites
The only hard requirement is a running version of python 3.3 or newer. To install the latest python 3.x version go to 
- [python.org/downloads](https://www.python.org/downloads/) 

and follow the installation instructions. Note that this repo has only been tested with python 3.6 and thus it is recommened to use `python3.6`.

To speed up training, it is recommended to use a **GPU with CUDA** support. For example on [AWS](/2_Training/AWS/) you can use a `p2.xlarge` instance (Tesla K80 GPU with 12GB memory). Inference is very fast even on a CPU with approximately ~2 images per second. 


### Installation

#### 1a Setting up Virtual Environment [Linux or Mac]

Clone this repo with:
```
git clone https://github.com/AntonMu/TrainYourOwnYOLO
cd TrainYourOwnYOLO/
```
Create Virtual **(Linux/Mac)** Environment (requires [venv](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/) which is included in the standard library of Python 3.3 or newer):
```
python3 -m venv env
source env/bin/activate
```
Make sure that, from now on, you **run all commands from within your virtual environment**.

#### 1b Setting up Virtual Environment [Windows]
Use the [Github Desktop GUI](https://desktop.github.com/) to clone this repo to your local machine. Navigate to the `TrainYourOwnYOLO` project folder and open a power shell window by pressing **Shift + Right Click** and selecting `Open PowerShell window here` in the drop-down menu.

Create Virtual **(Windows)** Environment (requires [venv](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/) which is included in the standard library of Python 3.3 or newer):

```
py -m venv env
.\env\Scripts\activate
```
![PowerShell](/Utils/Screenshots/PowerShell.png)
Make sure that, from now on, you **run all commands from within your virtual environment**.

#### 2 Install Required Packages [Windows, Mac or Linux]
Install all required packages with:

```
pip install -r requirements.txt
```
If this fails, you may have to upgrade your pip version first with `pip install pip --upgrade`. If your system has working CUDA drivers, it will use your GPU automatically for training and inference.

## Quick Start (Inference only)
To test the cat face detector on test images located in [`TrainYourOwnYOLO/Data/Source_Images/Test_Images`](/Data/Source_Images/Test_Images) run the `Minimal_Example.py` script in the root folder with:

```
python Minimal_Example.py
```

The outputs are saved in [`TrainYourOwnYOLO/Data/Source_Images/Test_Image_Detection_Results`](/Data/Source_Images/Test_Image_Detection_Results). This includes:
 - Cat pictures with bounding boxes around faces with confidence scores and
 - [`Detection_Results.csv`](/Data/Source_Images/Test_Image_Detection_Results/Detection_Results.csv) file with file names and locations of bounding boxes.

 If you want to detect cat faces in your own pictures, replace the cat images in [`Data/Source_Images/Test_Images`](/Data/Source_Images/Test_Images) with your own images.

## Full Start (Training and Inference)

To train your own custom YOLO object detector please follow the instructions detailed in the three numbered subfolders of this repo:
- [`1_Image_Annotation`](/1_Image_Annotation/),
- [`2_Training`](/2_Training/) and
- [`3_Inference`](/3_Inference/).
 
**To make everything run smoothly it is highly recommended to keep the original folder structure of this repo!**

Each `*.py` script has various command line options that help tweak performance and change things such as input and output directories. All scripts are initialized with good default values that help accomplish all tasks as long as the original folder structure is preserved. To learn more about available command line options of a python script `<script_name.py>` run:

```
python <script_name.py> -h
```

## License

Unless explicitly stated otherwise at the top of a file, all code is licensed under the MIT license. This repo makes use of [**ilmonteux/logohunter**](https://github.com/ilmonteux/logohunter) which itself is inspired by [**qqwweee/keras-yolo3**](https://github.com/qqwweee/keras-yolo3).

## Acknowledgements
Many thanks to [Niklas Wilson](https://github.com/NiklasWilson) for contributing towards making this repo compatible with Tensorflow 2.0. 

## Troubleshooting

0. If you encounter any error, please make sure you follow the instructions **exactly** (word by word). Once you are familiar with the code, you're welcome to modify it as needed but in order to minimize error, I encourage you to not deviate from the instructions above. If you would like to file an issue, please use the provided template and make sure to fill out all fields. 

1. If you encounter a `FileNotFoundError` or a `Module not found` error, make sure that you did not change the folder structure. In particular, your  working directory needs to look like this: 
    ```
    TrainYourOwnYOLO
    └─── 1_Image_Annotation
    └─── 2_Training
    └─── 3_Inference
    └─── Data
    └─── Utils
    ```
    If you want to use a different folder layout (not recommended) you will have to specify your paths as command line arguments. Also, try to avoid spaces in folder names, i.e. don't use a folder name like this `my folder` but instead use `my_folder`.

2. If you are using [pipenv](https://github.com/pypa/pipenv) and are having trouble running `python3 -m venv env`, try:
    ```
    pipenv shell
    ```

3. If you are having trouble getting cv2 to run, try:

    ```
    apt-get update
    apt-get install -y libsm6 libxext6 libxrender-dev
    pip install opencv-python
    ```

4. If you are a Linux user and having trouble installing `*.snap` package files try:
    ```
    snap install --dangerous vott-2.1.0-linux.snap
    ```
    See [Snap Tutorial](https://tutorials.ubuntu.com/tutorial/advanced-snap-usage#2) for more information.

## Filing an Issue
If you would like to file an issue, please use the provided issue template and make sure to complete all fields. This makes it easier to reproduce the issue for someone trying to help you. 

![Issue](/Utils/Screenshots/Issue.gif)

Issues without a completed issue template will be deleted after 7 days. 

## Stay Up-to-Date

- ⭐ **star** this repo to get notifications on future improvements and
- 🍴 **fork** this repo if you like to use it as part of your own project.

![CatVideo](/Utils/Screenshots/CatVideo.gif)

## Pip list

C:\Users\bob>pip list
Package                         Version
------------------------------- -------------------
absl-py                         0.7.1
asgiref                         3.2.7
astor                           0.8.0
astunparse                      1.6.3
attrs                           19.1.0
backcall                        0.1.0
bleach                          3.1.4
cachetools                      4.0.0
certifi                         2019.6.16
chardet                         3.0.4
colorama                        0.4.3
contextlib2                     0.6.0.post1
cycler                          0.10.0
Cython                          0.29.16
decorator                       4.4.0
defusedxml                      0.6.0
Django                          3.0.5
docutils                        0.16
entrypoints                     0.3
gast                            0.2.2
google-auth                     1.13.1
google-auth-oauthlib            0.4.1
google-pasta                    0.2.0
grpcio                          1.22.0
h5py                            2.10.0
idna                            2.8
image                           1.5.28
importlib-metadata              1.6.0
ipykernel                       5.1.1
ipython                         7.6.1
ipython-genutils                0.2.0
ipywidgets                      7.5.0
jedi                            0.14.0
Jinja2                          2.10.1
joblib                          0.13.2
jsonschema                      3.0.1
jupyter                         1.0.0
jupyter-client                  5.3.0
jupyter-console                 6.0.0
jupyter-core                    4.5.0
Keras                           2.1.5
Keras-Applications              1.0.8
Keras-Preprocessing             1.1.0
keyring                         21.2.0
kiwisolver                      1.1.0
lxml                            4.5.0
Markdown                        3.1.1
MarkupSafe                      1.1.1
matplotlib                      3.0.3
mistune                         0.8.4
mpmath                          1.1.0
nbconvert                       5.5.0
nbformat                        4.4.0
notebook                        5.7.8
numpy                           1.18.2
oauthlib                        3.1.0
opencv-python                   4.1.0.25
opt-einsum                      3.2.0
pandas                          0.24.2
pandocfilters                   1.4.2
parso                           0.5.0
pexpect                         4.7.0
pickleshare                     0.7.5
Pillow                          6.2.1
pip                             20.0.2
pkginfo                         1.5.0.1
progressbar2                    3.46.1
prometheus-client               0.7.1
prompt-toolkit                  2.0.9
protobuf                        3.11.3
ptyprocess                      0.6.0
pyasn1                          0.4.8
pyasn1-modules                  0.2.8
Pygments                        2.4.2
pyparsing                       2.4.0
pyrsistent                      0.15.3
python-dateutil                 2.8.0
python-utils                    2.4.0
pytz                            2019.1
pywin32                         227
pywin32-ctypes                  0.2.0
pywinpty                        0.5.7
PyYAML                          5.3.1
pyzmq                           18.0.2
qtconsole                       4.5.1
QtPy                            1.9.0
readme-renderer                 25.0
requests                        2.22.0
requests-oauthlib               1.3.0
requests-toolbelt               0.9.1
rsa                             4.0
scikit-learn                    0.21.2
scipy                           1.4.1
Send2Trash                      1.5.0
setuptools                      46.1.3
six                             1.14.0
sklearn                         0.0
sqlparse                        0.3.1
sympy                           1.4
tb-nightly                      2.3.0a20200404
tensorboard                     1.15.0
tensorboard-plugin-wit          1.6.0.post2
tensorflow-estimator            1.15.1
tensorflow-gpu                  1.15.0
tensorflow-gpu-estimator        2.1.0
tensorflow-object-detection-api 0.1.1
termcolor                       1.1.0
terminado                       0.8.2
testpath                        0.4.2
tf-estimator-nightly            2.3.0.dev2020040301
tornado                         6.0.3
tqdm                            4.45.0
traitlets                       4.3.2
twine                           3.1.1
urllib3                         1.25.3
wcwidth                         0.1.7
webencodings                    0.5.1
Werkzeug                        0.15.4
wheel                           0.34.2
widgetsnbextension              3.5.0
wrapt                           1.11.2
zipp                            3.1.0
