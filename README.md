# S.H.A.D.Y

Smart Human Activity Detection Using [YOLO](https://pjreddie.com/darknet/yolo/)

![Alt text](https://github.com/vibhorkrishna/S.H.A.D.Y/blob/main/Screenshots/SaftyNet.PNG?raw=true)

This is a project to perform fall detection, vehicle crash detection and social distancing detection from CCTV cameras in real-time.

## How YOLO works ?

![Alt text](https://cdn-images-1.medium.com/max/1024/1*bSLNlG7crv-p-m4LVYYk3Q.png)

YOLO stands for You Only Look Once. It is used for object detection
To perform object detection on an image it looks at an image only once in a very clever way unlike R-CNN which takes several instances of the same image to perform detection. 

YOLO divides an image into a grid and several bounding boxes are formed. Then a confidence score is taken for each boundary box to see whether an bounding box contains any object within it. The confidence score is high if the object inside the box matches the pre-trained YOLO dataset ( [COCO Dataset](https://cocodataset.org/) ). The higher the confidence score, the higher the probability that a bounding box contains an object. Now several bounding boxes will intersect with each other. More the bounding boxes intersect, more is the probability that there is an object inside that box. Now we only keep those bounding boxes whose confidence score is more than threshold value lets say 30%. Now we match these bounding boxes with already known features of an object like person, car and classify them.

The good thing about YOLO is that all the predictions in the boxes are made at the same time i.e. the neural networks just ran only once.
And that is why YOLO is powerful and fast.

## Installation

### Softwares Required
* Python: Language in which code is written
* CMake: For compiling openCV
* Visual Studio Code: For building openCV and darknet code
* Nvidia GPU Driver: For faster GPU performance
* CUDA: For parallel computing using GPU
* CuDNN: A GPU-accelerated library of primitives for deep neural networks
* OpenCV: For working on images/videos in python
* Darknet: Neural network framework for YOLO
### Installation of above softwares
You can follow the two part YouTube videos of [Augmented Startups](https://www.youtube.com/watch?v=5pYh1rFnNZs&ab_channel=AugmentedStartups)
#### [Note-1: Darknet library gets updated daily so this code won't work for future versions of darknet. This code works for May 2020 - June 2020 version of [Darknet](https://github.com/AlexeyAB/darknet). So download that version of darknet otherwise you will get a lot of errors which would be very difficult to remove.]
#### [Note-2: If you face some errors check the comments of the video of [Augmented Startups](https://www.youtube.com/watch?v=5pYh1rFnNZs&ab_channel=AugmentedStartups). You will get the solutions for most of them there. Also download only that versions of the software that has been told in the video.]
### Usage
After the above installation work is done and darknet libraries are working, place the python files inside [YOLO\darknet\build\darknet\x64]() folder.

There are four ways to perform detection on videos:
1. Video from Web Cam
2. Local Stored Video
3. YouTube video
4. Video from Mobile Camera ( [DroidCam](https://www.dev47apps.com/) )

See the code of the program and uncomment the line from which you want to take the  video to perform detection.

You can take the video from Sample dataset to perform detection.
#### [Note: If you want to perform the detection on a locally stored video then make sure that the video is stored inside the [YOLO\darknet\build\darknet\x64]() folder along with the python script]

## Object Detection
### Working
Simple YOLO program for object detection.

### Running the script:
```python
python Object_Detection.py
```
### Sample Output:
![Alt text](https://github.com/vibhorkrishna/S.H.A.D.Y/blob/main/Screenshots/object.PNG?raw=true)
## Fall Detection
### Working
We take the input video from a source and  divide the video into several frames. Now these frames are converted into black and white. On each frame a person is detected using YOLO. 

Now we write the code to draw rectangles on the detected persons. Whenever the height of the rectangle is greater than width of the rectangle Fall is not detected and when width is greater than height Fall is detected.

And this is how we classify the images into a fall and not fall and an alert is generated if a fall is detected.

All of the above process happens for a single frame. Now all of this is set in a loop for each frame of the video and Fall is detected.

### Alert Generation
If the fall is detected in 20 frames of a video simultaneously then an alert is generated by sending an email to the required person. That email also contains the photo of the fall that was detected.
#### [Note-1: Edit the sender's and receiver's email id in ```image_email_fall.py``` file]
#### [Note-2: Make sure that ```2 step verification``` is ```OFF``` and ```less secure app access``` is ```ON``` for your email account]

### Running the script:
```python
python Fall_Detection.py
```
### Sample Output:
![Alt text](https://github.com/vibhorkrishna/S.H.A.D.Y/blob/main/Screenshots/fall.PNG?raw=true)
### Email Alert:
![Alt text](https://github.com/vibhorkrishna/S.H.A.D.Y/blob/main/Screenshots/alert_fall.PNG?raw=true)

## Social Distancing Detection
### Working
We take the input video from a source and  divide the video into several frames. Now these frames are converted into black and white. On each frame a person is detected using YOLO. 

Now we write the code to draw rectangles on the detected persons. We check the distances between each detected person on the frame from each other. If the distance between the two persons is less than a particular value then we colour the box red and draw a line between these boxes and add the no. of social distancing violations in a variable and display it. 

All of the above process happens for a single frame. Now all of this is set in a loop for each frame of the video and People at Risks are detected.
### Running the script:
```python
python Social_Distance.py
```
### Sample Output:
![Alt text](https://github.com/vibhorkrishna/S.H.A.D.Y/blob/main/Screenshots/social_distance.PNG?raw=true)

## Vehicle Crash Detection
### Working
We take the input video from a source and  divide the video into several frames. Now these frames are converted into black and white. On each frame a car is detected using YOLO. 

Now we write the code to draw rectangles on the detected cars. We check the distances between each detected car on the frame from each other. If the distance between the two cars is less than a particular value and the rectangle boxes of any two cars intersect each other then we colour the box red display the message that Crash has been detected. 

All of the above process happens for a single frame. Now all of this is set in a loop for each frame of the video and Vehicle crash is detected.

### Alert Generation
If the car crash is detected in 20 frames of a video simultaneously then an alert is generated by sending an email to the required person. That email also contains the photo of the car crash that was detected.
#### [Note-1: Edit the sender's and receiver's email id in ```image_email_car.py``` file]
#### [Note-2: Make sure that ```2 step verification``` is ```OFF``` and ```less secure app access``` is ```ON``` for your email account]

### Running the script:
```python
python Vehicle_Crash.py
```
### Sample Output:
![Alt text](https://github.com/vibhorkrishna/S.H.A.D.Y/blob/main/Screenshots/crash.PNG?raw=true)
### Email Alert:
![Alt text](https://github.com/vibhorkrishna/S.H.A.D.Y/blob/main/Screenshots/alert_car.PNG?raw=true)

## Project Deployment
We have deployed our project using flask. When we run the below script, our website is hosted onto a local server and we can use that website to perform detections on videos.
### Running the script:
```python
python app.py
```

## SaftyNet Website

### Home Page
![Alt text](https://github.com/vibhorkrishna/S.H.A.D.Y/blob/main/Screenshots/home.PNG?raw=true)
### Object Detection Page
![Alt text](https://github.com/vibhorkrishna/S.H.A.D.Y/blob/main/Screenshots/object_detection.PNG?raw=true)
### Fall Detection Page
![Alt text](https://github.com/vibhorkrishna/S.H.A.D.Y/blob/main/Screenshots/fall_detection.PNG?raw=true)
### Social Distancing Detection Page
![Alt text](https://github.com/vibhorkrishna/S.H.A.D.Y/blob/main/Screenshots/social_distancing_detection.PNG?raw=true)
### Vehicle Crash Detection Page
![Alt text](https://github.com/vibhorkrishna/S.H.A.D.Y/blob/main/Screenshots/vehicle_crash_detection.PNG?raw=true)
### Object Detected Page
![Alt text](https://github.com/vibhorkrishna/S.H.A.D.Y/blob/main/Screenshots/object_detected.PNG?raw=true)
### Fall Detected Page
![Alt text](https://github.com/vibhorkrishna/S.H.A.D.Y/blob/main/Screenshots/fall_detected.PNG?raw=true)
### Social Distancing Detected Page
![Alt text](https://github.com/vibhorkrishna/S.H.A.D.Y/blob/main/Screenshots/social_distancing_detected.PNG?raw=true)
### Vehicle Crash Detected Page
![Alt text](https://github.com/vibhorkrishna/S.H.A.D.Y/blob/main/Screenshots/vehicle_crash_detected.PNG?raw=true)
### Contact Us Page
![Alt text](https://github.com/vibhorkrishna/S.H.A.D.Y/blob/main/Screenshots/contact_us.PNG?raw=true)

## Directory and File Structure
After installing darknet keep the github files according to this file structure
```
darknet
| 
| 
|───build
|   |
|   |
|   |───darknet
|   |	|
|   |	|
|   |	|───x64
|   |	|   |   
|   |	|   |   
|   |	|   |───app.py
|   |	|   |───Fall_Detection.py
|   |	|   |───Object_Detection.py
|   |	|   |───Social_Distance.py
|   |	|   |───Vehicle_Crash.py
|   |	|   |───image_email.py
|   |	|   |
|   |	|   |───templates
|   |	|   |   | 
|   |	|   |   | 
|   |	|   |   |───FallDetection.html
|   |	|   |   |───ObjectDetection.html
|   |	|   |   |───SaftyNet.html
|   |	|   |   |───SocialDistancingDetection.html
|   |	|   |   |───VehicleCrashDetection.html
|   |	|   |   |───Video.html
|   |	|   |
|   |	|   |───static
|   |	|   |   | 
|   |	|   |   | 
|   |	|   |   |───assets
|   |	|   |   |
|   |	|   |   |
|   |	|   |   |───...files...
|   |	|   |   |───fonts
|   |	|   |   |
|   |	|   |   |
|   |	|   |   |───...files...
|   |	|   |───...files...
|   |   |───...files...	
|   |───...files...
|───...files...
```

## Future Work
* Improve the vehicle crash detection model
* Currently website is deployed locally using flask and uses our own computer's GPU. As our code uses GPU, it would cost us money to deploy our website on cloud servers like Google Cloud and AWS. But our future goal is to deploy the website globally from Google Cloud by using their GPU's.