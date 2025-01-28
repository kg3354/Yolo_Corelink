# Yolo_Corelink

This repository contains the Yolo Corelink demo, which integrates YOLO (You Only Look Once) for object detection with Corelink for communication between devices and Kubernetes.

Before you start, make sure you install the necessary Python package to use Corelink.

```bash
pip install -r requirements.txt
```

## Overview

The demo involves two main components:
1. **Sender**: A device (such as a Raspberry Pi or other device) that captures video frames and sends them to a receiver for processing.
2. **Receiver**: A service deployed on Kubernetes that runs YOLO to process the frames and returns the object detection results back to the sender.

Two sender scripts are provided:
- **General sender**: Can be run on various devices.
- **Raspberry Pi sender**: Specifically designed for use with a Raspberry Pi.

## How to Run the Demo

### 1. Deploy the Receiver on Kubernetes

The receiver is responsible for running YOLO object detection on the frames received from the sender.

To deploy the receiver:
- Use the provided `Dockerfile` to build the receiver container.
- Create the Kubernetes deployment using the provided `.yaml` configuration file.
- The receiver will process incoming frames and return results back to the sender.


Make sure that your Kubernetes cluster is properly configured and running. The receiver will listen for incoming frames, so ensure it’s ready to receive data from the sender.

### 2. Start the Sender on Your Device

Once the receiver is deployed, start the sender script on your device (or Raspberry Pi, if you are using that version). The sender captures frames from the camera and sends them in real-time to the receiver for processing.

- For general devices, use `detectionSender.py`.
- For Raspberry Pi, use `detectionSenderPi.py`.

```bash
# Example: Start the general sender
python detectionSender.py

# Example: Start the Raspberry Pi sender
python detectionSenderPi.py
```

Ensure that the sender is configured to connect to the receiver's endpoint (e.g., the IP address of the Kubernetes service).

### 3. Processing the Frames

As the sender streams frames from the camera, the receiver processes each frame using YOLO to detect objects in real-time. After processing, the receiver returns the results (detected objects, bounding boxes, etc.) back to the sender.

