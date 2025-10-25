Vehicle Tracking and Counting using YOLOv3 and SORT
This project implements a real-time object tracking and counting system for vehicles in a video stream. It combines the powerful YOLOv3 deep learning model for initial object detection with the SORT (Simple Online and Realtime Tracking) algorithm for persistent tracking across frames.

The system is designed to count objects (vehicles) as they cross a defined virtual line within the video feed.

Key Features
Object Detection: Utilizes a pre-trained YOLOv3 model on the COCO dataset for accurate detection of objects (vehicles).

Object Tracking: Implements the SORT algorithm for stable, frame-to-frame tracking of detected objects, assigning a unique ID to each.

Counting Mechanism: Tracks when the trajectory of a detected and tracked object intersects a defined virtual line, incrementing a counter.

Visualization: Draws bounding boxes, unique ID labels, object paths, the virtual counting line, and the total count directly onto the video frames.

Dependencies: Built using Python, OpenCV, and NumPy.

Prerequisites
You need the following files for the YOLO model, which should be placed in a directory specified by the --yolo argument:

yolov3.cfg (YOLO model configuration file)

yolov3.weights (YOLO pre-trained weights)

coco.names (Class labels file)

Installation
Clone the repository:

Bash

git clone <repository_link>
cd <repository_name>
Install dependencies: The project relies on standard Python computer vision libraries. Make sure to include the sort.py file (which should contain the SORT tracker implementation) in your project directory.

Bash

pip install numpy opencv-python imutils
How to Run the Script
The script uses command-line arguments to specify the video files and the YOLO model path.

Bash

python main.py \
    --input "path/to/input/video.mp4" \
    --output "path/to/output/video.avi" \
    --yolo "path/to/yolo/files" \
    --confidence 0.5 \
    --threshold 0.3
Arguments:
Argument	Description	Required	Default
-i, --input	Path to the input video file.	Yes	
-o, --output	Path to save the processed output video file.	Yes	
-y, --yolo	Base path to the directory containing YOLO files (yolov3.cfg, yolov3.weights, coco.names).	Yes	
-c, --confidence	Minimum probability to filter weak object detections.	No	0.5
-t, --threshold	Threshold for Non-Maxima Suppression (NMS).	No	0.3

Export to Sheets

Code Details
Detection: YOLOv3 is loaded using cv2.dnn.readNetFromDarknet.

Tracking: The SORT algorithm (from sort import *) is initialized as tracker = Sort(). It updates based on detections filtered by NMS.

Counting Logic: The script defines a virtual line line = [(43, 543), (550, 655)] and uses a geometric intersect(A, B, C, D) function to determine when a tracked object's trajectory crosses this line.

Memory: The memory dictionary stores the last known bounding box coordinates for each tracked ID, allowing the script to draw the object's movement path.
