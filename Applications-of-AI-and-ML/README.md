# About me

![About Me](speaker.jpg)

# Real World Applications of AI and ML - Deep Dive 

## Pre-Requisites-1
- Before starting the session. Here are some prerequisites
- All you need is understanding of Python.
- You should be familiar with common data structures and algorithms like arrays, linked lists, binary search trees, and graph algorithms
- You should be familiar with data visualization, data cleaning, feature engineering, and model selection.

## Setting up system Pre-requisites.

- Hardware: You will need a computer with a powerful processor (such as an Intel i5 or i7) and a good amount of RAM (at least 8GB, but preferably 16GB or more). A dedicated GPU (Graphics Processing Unit) with CUDA support, such as NVIDIA GeForce or Quadro series, is also recommended as it can significantly improve the training and inference speed of the model.

- Operating System: You will need an operating system that supports the deep learning framework you will be using. The most common operating systems for deep learning are Linux, MacOS, and Windows.

- Deep Learning Framework: You will need to install a deep learning framework that supports object detection. Popular choices include TensorFlow, PyTorch etc.

- Object Detection Library: You will need to install an object detection library that is compatible with your deep learning framework. Popular object detection libraries include Detectron2, YOLO, and Mask R-CNN.

- Dataset: You will need a dataset of images or videos with labeled objects for training and evaluation of the object detection model. There are several publicly available datasets such as COCO, Pascal VOC, and ImageNet, or you can create your own dataset.

- Pre-trained Models: To speed up the training process, you can use pre-trained models that have been trained on large datasets. These models can be fine-tuned on your own dataset to improve their performance for your specific application.

## Data Sets/ Create a custom data set. 

- One of the Main step is to choose proper datasets or create a proper dataset.
- To select or create a dataset, you first need to identify the type of information you want to use. For example, if you want to create a dataset for recognizing objects in images, you might need to collect photographs of various objects.
- Once you know what type of data you need, you can start collecting it. This could involve taking pictures or recording audio. If you are creating a custom dataset, you may need to create a survey or questionnaire to collect information from people.
- It is important to make sure the data you collect is accurate and relevant to your application. You may need to check for errors and inconsistencies in the data before using it for analysis or AI.
- For getting proper dataset we can use https://www.kaggle.com/datasets 
```
ssh-keygen
generate new key
```

# Install cv2
```
sudo pip3 install opencv-contrib-python
For Open Cv
 - wget https://github.com/Qengineering/Install-OpenCV-Raspberry-Pi-32-bits/raw/main/OpenCV-4-5-5.sh
 - sudo chmod 755 ./OpenCV-4-5-5.sh
- ./OpenCV-4-5-5.sh
Takes around 45+ mins
```
## Library dependency 
```
 sudo apt-get install cmake gfortran
 sudo apt-get install python3-dev python3-numpy
 sudo apt-get install libjpeg-dev libtiff-dev libgif-dev
 sudo apt-get install libgstreamer1.0-dev gstreamer1.0-gtk3
 sudo apt-get install libgstreamer-plugins-base1.0-dev gstreamer1.0-gl
 sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev
 sudo apt-get install libgtk2.0-dev libcanberra-gtk*
 sudo apt-get install libxvidcore-dev libx264-dev libgtk-3-dev
 sudo apt-get install libtbb2 libtbb-dev libdc1394-22-dev libv4l-dev
 sudo apt-get install libopenblas-dev libatlas-base-dev libblas-dev
 sudo apt-get install libjasper-dev liblapack-dev libhdf5-dev
 sudo apt-get install protobuf-compiler
 sudo apt-get install libopencv-dev python3-opencv
```

# Installing PyTorch and OpenCV
PyTorch and all the other libraries we need have ARM 64-bit/aarch64 variants so you can just install them via pip and have it work like any other Linux system.

```
 pip install torch torchvision torchaudio
 pip install opencv-python
 pip install numpy --upgrade
```

We can now check that everything installed correctly:
```
 python -c "import torch; print(torch.__version__)"
```

## Tensorflow lite for bullseye os RPi 4
### Supported features

* NEON optimization
* VFPv4 optimization
* XNNPACK delegate
* Ruy matrix multiplication library
* MMAP-based allocation
* C and C++ APIs
* Python 3 bindings

## Prerequisites

### Supported Boards

* Raspberry Pi 3 Model A+
* Raspberry Pi 3 Model B+
* Raspberry Pi 4 Model B

Tested on Raspberry Pi 4 Model B (8 GB).

### Supported OS

* Raspberry Pi OS Bullseye (32-bit and 64-bit)

## Install

* 32-bit:

```shell
wget https://github.com/prepkg/tensorflow-lite-raspberrypi/releases/latest/download/tensorflow-lite.deb
```

```shell
sudo apt install -y ./tensorflow-lite.deb
```

* 64-bit:

```shell
wget https://github.com/prepkg/tensorflow-lite-raspberrypi/releases/latest/download/tensorflow-lite_64.deb
```

```shell
sudo apt install -y ./tensorflow-lite_64.deb
```

## Uninstall

```shell
sudo apt purge --autoremove -y tensorflow-lite
```

## Debian Package

Debian package contains the following shared libraries:

| Library                     | Description                                                            |
|:----------------------------|:-----------------------------------------------------------------------|
| libtensorflowlite_c.so      | C API to access TensorFlow Lite interpreter and perform an inference   |
| libtensorflow-lite.so       | C++ API to access TensorFlow Lite interpreter and perform an inference |

## Training custom data to get .h5 model
#### [Reference code in colab](https://colab.research.google.com/drive/1zNItoV6dVHXR4UbZaVnHMNKaDTKU0Czq?usp=sharing)

```

# Import necessary libraries
import numpy as np
from keras.models import Sequential
from keras.layers import Conv2D, MaxPooling2D, Flatten, Dense
from keras.preprocessing.image import ImageDataGenerator

# Set image size and path to dataset
img_size = (128, 128)
train_dir = '/content/drive/My Drive/dataset/train'
valid_dir = '/content/drive/My Drive/dataset/valid'

# Preprocess the dataset
train_datagen = ImageDataGenerator(rescale=1./255)
train_generator = train_datagen.flow_from_directory(
    train_dir,
    target_size=img_size,
    batch_size=32,
    class_mode='categorical'
)

valid_datagen = ImageDataGenerator(rescale=1./255)
valid_generator = valid_datagen.flow_from_directory(
    valid_dir,
    target_size=img_size,
    batch_size=32,
    class_mode='categorical'
)

# Define the model architecture
model = Sequential()
model.add(Conv2D(32, (3, 3), activation='relu', input_shape=(img_size[0], img_size[1], 3)))
model.add(MaxPooling2D((2, 2)))
model.add(Conv2D(64, (3, 3), activation='relu'))
model.add(MaxPooling2D((2, 2)))
model.add(Conv2D(128, (3, 3), activation='relu'))
model.add(MaxPooling2D((2, 2)))
model.add(Conv2D(128, (3, 3), activation='relu'))
model.add(MaxPooling2D((2, 2)))
model.add(Flatten())
model.add(Dense(512, activation='relu'))
model.add(Dense(3, activation='softmax'))

# Compile the model
model.compile(optimizer='rmsprop', loss='categorical_crossentropy', metrics=['accuracy'])

# Train the model
history = model.fit_generator(
    train_generator,
    steps_per_epoch=len(train_generator),
    epochs=50,
    validation_data=valid_generator,
    validation_steps=len(valid_generator)
)

# Save the model as an .h5 file
model.save('my_model.h5')
```
Files will be saved as .h5 model with this code.

## Training custom .h5 model and detecting.
```
import cv2
import torch
import torchvision.transforms as transforms
import numpy as np

# Load the custom model
model = torch.load('test.h5')

# Define the transformations to be applied to the input image
transform = transforms.Compose([
    transforms.ToPILImage(),
    transforms.Resize((224, 224)),
    transforms.ToTensor(),
    transforms.Normalize(mean=[0.485, 0.456, 0.406],
                         std=[0.229, 0.224, 0.225])
])

# Define the labels for the objects that the model can detect
labels = ['object1', 'object2', 'object3']

# Initialize the camera capture
cap = cv2.VideoCapture(0)

while True:
    # Capture a frame from the camera
    ret, frame = cap.read()

    # Convert the frame to a PyTorch tensor
    frame = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)
    img_pil = transform(frame)
    img_tensor = torch.unsqueeze(img_pil, 0)

    # Pass the tensor through the model to detect objects
    with torch.no_grad():
        output = model(img_tensor)

    # Convert the output tensor to a numpy array and get the index of the predicted label
    output = output.numpy()[0]
    index = np.argmax(output)

    # Draw the predicted label on the frame
    label = labels[index]
    cv2.putText(frame, label, (50, 50), cv2.FONT_HERSHEY_SIMPLEX, 1, (0, 255, 0), 2)

    # Show the frame
    cv2.imshow('frame', frame)

    # Exit the loop if 'q' is pressed
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

# Release the capture and close the window
cap.release()
cv2.destroyAllWindows()
```
## change .h5 model to tflite model

```
import tensorflow as tf

model = tf.keras.models.load_model('/content/animall_person_other_v2_fine_tuned.h5')
converter = tf.lite.TFLiteConverter.from_keras_model(model)
tflite_model = converter.convert()
open("animall_person_other_v2_fine_tuned.tflite", "wb").write(tflite_model)
```

## Adding meta data 
```
pip install tflite_support_nightly
```



## Reference

1. [TensorFlow Lite repository](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/lite)
2. [Tensorflow setup for Bullseye os 11 ](https://qengineering.eu/install-tensorflow-on-raspberry-64-os.html)
3. [post-processing in pi](https://www.raspberrypi.com/documentation/computers/camera_software.html#post-peocessing-with-tensorflow-lite)
4. [change new camera module Bullseye os](https://www.tomshardware.com/how-to/use-raspberry-pi-camera-with-bullseye)
5. 

