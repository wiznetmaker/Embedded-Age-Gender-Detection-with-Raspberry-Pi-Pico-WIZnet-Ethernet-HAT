# Embedded Age & Gender Detection with Raspberry Pi Pico & WIZnet Ethernet HAT
![image](https://github.com/wiznetmaker/Embedded-Age-Gender-Detection-with-Raspberry-Pi-Pico-WIZnet-Ethernet-HAT/assets/115054808/a8dcc178-e5f5-43e0-a07c-3dcd46bf0b49)


Have you ever wondered about the demographics of people visiting your store or passing by your digital signage? This Raspberry Pi Pico-powered solution can help you detect the age group and gender of individuals in real-time. In this tutorial, we'll explore how computer vision and an embedded machine learning (ML) age and gender classification model can be deployed to an Arm Cortex-M0+ based Raspberry Pi Pico board with a WIZnet Ethernet HAT to analyze images captured by a camera.

The system will run continuously and:

1. Capture an image from a camera module connected to the Raspberry Pi Pico board.
2. Use the captured image as input to an ML model that detects the age group and gender of the person in the image.
3. Smooth the ML model's output using an exponential smoothing algorithm.
4. Send the processed data to a server or display it on a connected screen.

To preserve privacy, all ML inferencing will be done on the board's Arm Cortex-M0+ processor using the TensorFlow Lite for Microcontrollers (TFLM) library. The application running on the Pico board will only send the age group and gender data over Ethernet using the WIZnet Ethernet HAT.

## Camera input

The Raspberry Pi Pico will be connected to an Arducam 5MP Plus Camera Module, which will capture images at a resolution of 640x480 pixels. The camera module will be connected to the Pico board using the UART interface.

## Ethernet connectivity

The WIZnet Ethernet HAT will be used to provide Ethernet connectivity to the Raspberry Pi Pico. This will allow the Pico to send the processed age and gender data to a server or display it on a connected screen.

## Training the ML age and gender classification model

### Dataset

The ML model will be trained on the UTKFace dataset, which contains over 20,000 face images with annotations of age, gender, and ethnicity. The dataset will be preprocessed and split into training and validation sets.
  
  [UTKFace](https://susanqq.github.io/UTKFace/)
  ![image](https://github.com/wiznetmaker/Embedded-Age-Gender-Detection-with-Raspberry-Pi-Pico-WIZnet-Ethernet-HAT/assets/115054808/c8fb226c-ddd4-4ae4-a2f0-3ffca5e33771)

  

### Model Architecture

The ML model will use the MobileNet V1 architecture with an alpha of 0.25, similar to the person detection example in TensorFlow Lite for Microcontrollers (TFLM). The model will be modified to output the age group and gender of the detected face.
  ![image](https://github.com/wiznetmaker/Embedded-Age-Gender-Detection-with-Raspberry-Pi-Pico-WIZnet-Ethernet-HAT/assets/115054808/a25e33f3-e60a-433f-a8d6-9ba807e4905b)


### Training pipeline

A Jupyter Notebook will be used to train the custom MobileNet V1 model on the UTKFace dataset. The notebook will cover the following steps:

1. Dataset processing: Download and preprocess the UTKFace dataset, and split it into training and validation sets.
   ![image](https://github.com/wiznetmaker/Embedded-Age-Gender-Detection-with-Raspberry-Pi-Pico-WIZnet-Ethernet-HAT/assets/115054808/e177272e-0238-472d-bc57-0c0bb062eb14)

2. ML model creation: Create a MobileNet V1 model with an input size of (96, 96, 3), alpha of 0.25, dropout of 0.1, and output classes for age group and gender.
   ![image](https://github.com/wiznetmaker/Embedded-Age-Gender-Detection-with-Raspberry-Pi-Pico-WIZnet-Ethernet-HAT/assets/115054808/0febabd5-c758-40a1-8ee5-a1cd8a220bcc)

3. ML model exporting: Convert the trained model to TensorFlow Lite format using quantization for efficient inferencing on the Pico board.
  ![image](https://github.com/wiznetmaker/Embedded-Age-Gender-Detection-with-Raspberry-Pi-Pico-WIZnet-Ethernet-HAT/assets/115054808/6a4e5f15-1330-4f8c-a7a4-d539ae2c8c90)

## Final application

The application on the Pico board will perform the following steps:
// Initialize the camera and capture an image
initCamera();
captureImage();

// Perform ML inferencing with the captured image
runInference();

// Smooth the predictions from the ML model
smoothPredictions();

// Send the processed age group and gender data over Ethernet
sendDataOverEthernet();

## Conclusion

This guide demonstrated how a custom age and gender classification model could be trained on the UTKFace dataset and deployed to a Raspberry Pi Pico board with a WIZnet Ethernet HAT. The Pico board captures images from a camera module, performs on-device ML inferencing, and sends the processed age group and gender data over Ethernet. This project can be further extended to analyze customer demographics in retail stores or to provide targeted content on digital signage based on the age and gender of the audience.

For more details and in-depth information about this project, please visit: [https://maker.wiznet.io](https://maker.wiznet.io/Benjamin/projects/embedded%2Dage%2Dgender%2Ddetection%2Dwith%2Draspberry%2Dpi%2Dpico%2Dwiznet%2Dethernet%2Dhat/?serob=rd&serterm=month)
