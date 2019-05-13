# Lightweight fall detection based on human pose estimation

The goal is to be able to deploy it on a Raspberry 3 Model B+ with a webcam and an [Intel® Neural Compute Stick 2](https://software.intel.com/en-us/neural-compute-stick). It should push a warning on other devices if a person has fallen. In a further step, it is planned to create a web video surveillance dashboard, and having several live streams including pose estimation from several Raspberries.

This repository is based on [PINTO0309/MobileNetV2-PoseEstimation](https://github.com/PINTO0309/MobileNetV2-PoseEstimation) which itself is based on [ildoonet/tf-pose-estimation](https://github.com/ildoonet/tf-pose-estimation).

An interesting and simple approach using the Y-axis movement of the head position to detect falls: https://github.com/reigngt09/Pose-Estimation/tree/master/3.%20Fall%20Detection 

We hope that performance will be sufficient to work with these models, else we would have to go for more simpler models.

## Notes

* Installing *numba* on Raspberry: https://github.com/numba/numba/issues/3670#issuecomment-476071328

---

*Original README follows:*

# MobileNetV2-PoseEstimation
**[Caution] The behavior of RraspberryPi+NCS2 is very unstable.**  
**[Caution] The behavior of Tensorflow Lite+CPU is unstable.**  
**[Caution] May 06, 2019, The Google Edge TPU program and model are under construction.**  


## Introduction
This repository has its own implementation, impressed by ildoonet's achievements.  
Thank you, **[ildoonet](https://github.com/ildoonet)**.  
**https://github.com/ildoonet/tf-pose-estimation.git**  
  
I will make his implementation even faster with CPU only.  

## Environment
- Ubuntu 16.04 x86_64
- **[OpenVINO 2019 R1.0.1](https://github.com/PINTO0309/OpenVINO-bin.git)**
- **[Tensorflow v1.12.0 + Tensorflow Lite](https://github.com/PINTO0309/Tensorflow-bin.git)**
- USB Camera
- Neural Compute Stick 2 (NCS2)
- Google Edge TPU
- Python 3.5

## Environment construction and training procedure
**[Learn "Openpose" from scratch with MobileNetv2 + MS-COCO and deploy it to OpenVINO/TensorflowLite Part.1](https://qiita.com/PINTO/items/2316882e18715c6f138c)**  
  
**[Learn "Openpose" from scratch with MobileNetv2 + MS-COCO and deploy it to OpenVINO/TensorflowLite (Inference by OpenVINO/NCS2) Part.2](https://qiita.com/PINTO/items/c1889317bc16534a75cf)**

## Core i7 only + OpenVINO + Openpose Large model + Sync mode (disabled GPU)
![01](media/01.gif)  
## NCS2 x1 + OpenVINO + Openpose Large model + Async + Normal mode
![02](media/02.gif)  
## Core i7 only + OpenVINO + Openpose Small model + Sync + Boost mode (disabled GPU)
![03](media/03.gif)  
## NCS2 x1 + OpenVINO + Openpose Small model + Async + Boost mode
![04](media/04.gif)  

## Usage
```console
$ git clone https://github.com/PINTO0309/MobileNetV2-PoseEstimation.git
$ cd MobileNetV2-PoseEstimation
```
**CPU - Sync Mode**  
```console
$ python3 openvino-usbcamera-cpu-ncs2-sync.py -d CPU
```
**CPU - Sync + Boost Mode**  
```console
$ python3 openvino-usbcamera-cpu-ncs2-sync.py -d CPU -b True
```
**NCS2 - Sync Mode**  
```console
$ python3 openvino-usbcamera-cpu-ncs2-sync.py -d MYRIAD
```
  
**CPU - Async Mode**  
```console
$ python3 openvino-usbcamera-cpu-ncs2-async.py -d CPU
```
**NCS2 - Async - Single Stick Mode**  
```console
$ python3 openvino-usbcamera-cpu-ncs2-async.py -d MYRIAD
```
**NCS2 - Async - Multi Stick Mode**  
```console
$ python3 openvino-usbcamera-cpu-ncs2-async.py -d MYRIAD -numncs 2
```
**NCS2 - Async - Single Stick + Boost Mode**  
```console
$ python3 openvino-usbcamera-cpu-ncs2-async.py -d MYRIAD -b True
```
**GPU (Intel HD series only) - Async - Boost Mode**  
```console
$ python3 openvino-usbcamera-cpu-ncs2-async.py -d GPU -b True
```
## Reference articles, Very Thanks!!
**https://github.com/ildoonet/tf-pose-estimation.git**  
**https://www.tensorflow.org/api_docs/python/tf/image/resize_area**  
**[Python OpenCVの基礎 resieで画像サイズを変えてみる - Pythonの学習の過程とか - ピーハイ](http://peaceandhilightandpython.hatenablog.com/entry/2016/01/09/214333)**  
**[Blurring and Smoothing - OpenCV with Python for Image and Video Analysis 8](https://youtu.be/sARklx6sgDk?t=228)**  
**https://www.learnopencv.com/deep-learning-based-human-pose-estimation-using-opencv-cpp-python/**  
**https://teratail.com/questions/169393**  
