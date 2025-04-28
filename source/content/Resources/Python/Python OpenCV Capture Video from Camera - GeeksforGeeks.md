---
title: "Python OpenCV: Capture Video from Camera - GeeksforGeeks"
source: "https://www.geeksforgeeks.org/python-opencv-capture-video-from-camera/"
author:
  - "[[GeeksforGeeks]]"
published: 2020-01-26
created: 2025-03-19
description: "A Computer Science portal for geeks. It contains well written, well thought and well explained computer science and programming articles, quizzes and practice/competitive programming/company interview Questions."
tags:
  - "clippings"
---
Last Updated : 05 Sep, 2024

With [[OpenCV]], we can capture a video from the camera. It lets you create a video capture object which is helpful to capture videos through webcam and then you may perform desired operations on that video.

****Steps to capture a video:****

- Use `cv2.VideoCapture(`) to create a video capture object for the camera.
- Create a VideoWriter object to save captured frames as a video in the computer.
- Set up an infinite while loop and use the `read()` method to read the frames using the above created object.
- Use `cv2.imshow()` method to show the frames in the video.
- Breaks the loop when the user clicks a specific key.

Below is the implementation.

```python
import cv2  

# Open the default camera 
cam = cv2.VideoCapture(0)  

# Get the default frame width and height 
frame_width = int(cam.get(cv2.CAP_PROP_FRAME_WIDTH)) frame_height = int(cam.get(cv2.CAP_PROP_FRAME_HEIGHT)) 

# Define the codec and create VideoWriter object 
fourcc = cv2.VideoWriter_fourcc(*'mp4v') 
out = cv2.VideoWriter('output.mp4', fourcc, 20.0, (frame_width, frame_height))  

while True:     
	ret, frame = cam.read()      
	# Write the frame to the output file     
	out.write(frame)      
	# Display the captured frame     
	cv2.imshow('Camera', frame)      
	# Press 'q' to exit the loop
	if cv2.waitKey(1) == ord('q'):
		break  
# Release the capture and writer objects 
cam.release() 
out.release() 
cv2.destroyAllWindows() 
```

#### Explanation:

First, we import the OpenCV library for python i.e. cv2. We use the VideoCapture() class of OpenCV to create the camera object which is used to capture photos or videos. The constructor of this class takes an integer argument which denotes the hardware camera index. Suppose the devices has two cameras, then we can capture photos from first camera by using VideoCapture(0) and if we want to use second camera, we should use VideoCapture(1).

The dimensions of the frame and the recorded video must be specified. For this purpose, we use the camera object method which is cam.get() to get cv2.CAP\_PROP\_FRAME\_WIDTH and cv2.CAP\_PROP\_FRAME\_HEIGHT which are the fields of cv2 package. The default values of these fields depend upon the actual hardware camera and drivers which are used.

We are creating a VideoWriter object to write the captured frames to a video file which is stored in the local machine. The constructor of this class takes the following parameters:

- ****Filepath/Filename:**** The file would be saved by specified name and at the specified path. If we mention only the file name, then the video file would be saved at the same folder where the python script for capturing video is running.
- ****Four Character Code:**** A four-letter word to denote the specific encoding and decoding technique or format which must be used in order to create the video. Some popular codecs include ‘MJPG’ = Motion JPEG codec, ‘X264’ = H.264 codec, ‘MP4V’ = [MPEG](https://www.geeksforgeeks.org/mpg-video-format/)\-4 video codec
- ****Frame rate:**** Frame rate determines the number of frames or individual images which are shown in a second. Higher frame rates produce smoother video, but it will also take more storage space as compared to lower frame rates.
- ****Video Dimension:**** The height and width of the video which are passed as a tuple.

Inside an infinite while loop, we use the read() method of the camera object which returns two values, the first value is boolean and describes whether the frame was successfully captured or not. The second value is a 3D numpy array which represents the actual photo capture. In order to represent an image, we need two-dimensional data structure and for representing color information, we must add another dimension to it making it three dimensional.

Then, we are writing the individual frames to the video file using the VideoWriter object which was previously created using the write() method which takes the captured frame as the argument. To display the captured frame, we are using cv2.imshow() function, which takes window name and the captured frame as arguments. This process is repeated infinitely to produce continuous video stream which consists of these frames.

In order to exit the application, we have break out of this infinite while loop. Hence we are assigning a key which can be used to quit the application. Here the cv2.waitKey() function takes and integer argument which denotes the number of milliseconds the program waits for to check whether the user has pressed any button. We can use this function to adjust the frame rate of the captured video by providing certain delay. We have assigned “q” as the quit button and we are checking every millisecond whether it is pressed in order to break out of the while loop. The ord() function returns the [ASCII](https://www.geeksforgeeks.org/ascii-table/) value of the character which is passed to it as an argument.

****Output:****

[video](https://media.geeksforgeeks.org/wp-content/uploads/20240722165408/freecompress-output_no_audio.mp4?_=2)
