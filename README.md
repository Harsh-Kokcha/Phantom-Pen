# Phantom-Pen
Gesture-controlled real-time drawing system using MediaPipe and OpenCV that lets users write, erase and annotate directly on a live webcam feed using finger-gestures.

## Introduction
The application enables users to `draw and write on a live video feed using their finger movements`. It can be used for quick explanations during meetings or maybe online classes. The input feed is captured through a webcam and processed using a python-based pipeline.

Using Google's `mediapipe` framework, the user's hand is detected and then represented using 21 distinct landmark points. These coordinates are then used to perfoem various actions such as drawing, eraing, clicking screenshot of drawing, or navigation based on the gesture mode. The user can change the color as well the sizes of the brush and the eraser.

The gestures as follows:

1. `Index finger:` Used to draw on the video
2. `Index + middle finger:` Used to move around the video and navigate through the navigation bar
3. `Index + middle + ring finger:`  save drawing (black background + your drawing)
4. `Index + middle + ring + pinky finger:` Used to erase the written text. 
5. `Index + middle + pinky finger (hold 3 seconds):` Clear the whole screen

## How to run
1. Make sure python is installed in your system.
2. Install the required dependencies.
3. Connect a webcam or use the built-in camera of your laptop/monitor.
4. Run the main application - python Deploy.py
5. Use the finger gestures to draw, erase, navigate, and save drawings in real time.
6. You can use the navigation bar as well on top of the video feed to perform various operations.
7. Press 'X' to exit the application.

## System Implementation

1. `Video Capture and Preprocessing:` This is done through the webcam and it is accessed using the OpenCV module available in python. The video must be inverted as the default feed is free of lateral inversion and if we write on this video, the text will be inverted.

2. `Gesture Recognition Using Hand Landmarks:` Using the mediapipe module, we create a class object capable of detecting the user’s hand and return the list of 21 landmark points. By manipulating the coordinates, we can specify the gesture and hence assign functionalities accordingly.

3. `Drawing on the video feed:` Using the coordinates, we can accurately draw through the OpenCV module. The thickness of the brush, eraser etc. can be adjusted.

## Technical challenges

1. `Drawing in a smooth and continuous manner:` To draw on the video feed, the simplest method would be to use the cv2.circle() function present in the OpenCV module. However, drawing a circle is a computationally expensive process and hence, doing it in real time causes the curve to become discontinuous. The solution to this was to store the list of coordinates obtained for every frame and make very small line segments between every subsequent coordinates. This resulted in these very small lines joining to form a smooth curve. An analogy would be the method of plotting a curve using closely spaced points on a coordinate graph.

2. `Drawing on the video feed:` While drawing on another canvas itself was easy, there was a neat trick involved to implementing it on the video itself. This can be done by applying the concepts of masking and bitwise operations. 

## Why not a self-trained model?

1. The main problem with training one's own model is the `procurement of a dataset large and balanced enough to accurately detect hands.` For the model to properly work accurately without any bias, we need a lot of varieties in the dataset, this is almost impossible to achieve on a personal basis. We also need to tackle the problem of handling noise in the background.

2. Then, arises the problem of `accurately locating the coordinates of the fingertips.` The actions involved require high precision, to draw, erase etc. The reason why the mediapipe module works so well is because Google manually annotated more than 30,000 training images with the landmark points. For training a deep neural network with that many images, we requires huge computational resources, and hence is not feasible.

3. We also need to keep in mind the `latency` as it is real-time in nature. A video generates a lot of frames per second and the model must be capable of handling that.

## Roadmap

The plan ahead would be to make the project more dynamic and user-friendly, we believe it has a lot of potential Implement a proper GUI for better user experience than what it is capable of providing now. 
Add more functionalities based on more gestures and make it a proper application capable of running on any user’s system.
