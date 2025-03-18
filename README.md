# Custom_Object_Detection_Using_YoloV8
**detection_single.py**

**Detailed Explanation of What the Program Does**
This program performs object detection on an image using a pre-trained YOLOv8 deep learning model from Ultralytics. It takes an image, detects objects in it, highlights those objects by drawing bounding boxes around them, and marks the center points of each detected object. Finally, it saves and displays the processed image showing all these annotations.

**🔹 Main Purpose**
The primary goal of the program is to automatically detect objects within a static image and visually represent those detections for analysis, verification, or further processing.

**✅ Step-by-Step Description of How the Program Works**
1. Input Image
  The program begins by loading an image (in this case, frame_1141.jpg) from the local storage.
  This image is the one that the program will analyze to detect objects.
2. YOLOv8 Model Loading
  It loads a pre-trained YOLOv8 model, which is a deep learning model specifically designed for real-time object detection.
  This model has already been trained on a dataset to recognize certain types of objects.
  The program loads the model from a file called best.pt. This file contains the weights and configuration of the trained YOLOv8 model.
3. Object Detection Process
  The program runs the YOLOv8 model on the input image.
  The model analyzes the image and predicts:
  Bounding boxes: The rectangular areas where it thinks an object is present.
  Class labels: What type of object it thinks is inside each box (e.g., person, car, dog).
  Confidence scores: How sure it is about each detection (expressed as a percentage or a decimal number between 0 and 1).
4. Filtering Results
  After detection, the program filters the objects based on their confidence scores.
  It keeps only the objects where the model is at least 10% confident in its prediction (this threshold can be increased for more reliable detections).
  This filtering ensures that very uncertain detections are ignored.
5. Center Point Calculation
  For each valid detection, the program calculates the center point of the bounding box.
  The center point represents the middle location of the detected object within the image.
  These center points can be useful in applications such as robotics, tracking, or navigation, where knowing the position of an object is important.
6. Drawing Annotations on the Image
  The program then draws on the original image:
  Bounding Boxes: Red rectangles around each detected object to indicate their location.
  Center Points: Small green circles at the center of each bounding box to show the central position of each object.
7. Output
  The processed image, now showing the bounding boxes and center points, is saved to a new file (Result_Image/detected_image01.jpg).
  The program also displays this annotated image in a separate window for visual inspection.
  It waits for the user to press a key (q key in this case) to close the display window.
8. Information Display
  The program prints useful information in the terminal, such as:
  The bounding box coordinates of each detected object.
  The center points of each object.
  The total number of objects detected.
  The time taken by the program to complete the detection and processing.
**✅ Summary of Features**
Feature	Explanation
  Single Image Processing	Works on one image at a time (the file specified in the code).
  Object Detection	Identifies objects and their locations in the image.
  Bounding Box Drawing	Draws rectangles around detected objects for visualization.
  Center Point Calculation	Marks the exact center of each detected object.
  Confidence Filtering	Only shows detections with confidence above a set threshold.
  Output Saving	Saves the final annotated image for later use.
  Real-Time Display	Shows the results in a pop-up window for immediate viewing.
  Timing Information	Displays how long the process took to complete.
**✅ Real-World Applications**
This type of program is commonly used in:
  Surveillance systems for identifying objects in security footage.
  Autonomous vehicles for recognizing pedestrians, vehicles, and obstacles.
  Robotics for locating and interacting with objects.
  Industrial automation for quality control or counting objects on a conveyor belt.
  Agriculture for detecting fruits, pests, or specific plant features.
**✅ Possible Improvements**
  Batch Processing: Process multiple images in a folder.
  Real-Time Video Detection: Apply the same detection on live video from a webcam or camera stream.
  Higher Confidence Threshold: Increase the threshold to improve detection quality.
  Label Display: Show the class name and confidence percentage on each bounding box.


**detect_compact.py**

**✅ Detailed Explanation of the Provided Python Code**

Purpose of the Program
  This program performs object detection on a series of images with different exposure levels using a YOLOv8 object detection model, and then aggregates the detections to highlight objects more reliably in a final annotated image.

It uses Intel RealSense camera streams (commented out in this case), processes static images for detection, and outputs both:
  A final image with bounding boxes around detected objects
  A list of unique center points of these objects after filtering duplicate detections
  The system also includes functionality to generate exposure-variant images and calculate 3D camera coordinates (commented).
**✅ How the Program Works: Step by Step**
1. Imports and Dependencies
  The program imports several Python libraries:
  cv2 (OpenCV): Image processing and computer vision.
  numpy: Handling arrays and matrices.
  ultralytics.YOLO: Using the YOLOv8 model for object detection.
  pyrealsense2: Interface with Intel RealSense cameras.
  math and os: For file handling and mathematical calculations.
2. DepthCamera Class (For RealSense Depth Camera Input)
  (Currently not active but ready for use in real-time systems)

This class is responsible for:

  Initializing and configuring the depth and color streams from an Intel RealSense camera.
  Capturing depth frames (distance data) and color frames (images).
  Getting camera intrinsics, which are internal parameters like focal length and principal points (used for calculating 3D coordinates).
  Calculating camera coordinates (x, y, z) from 2D pixel positions and depth values—important for 3D space mapping.
**🟢 Use case (if uncommented):**
  Capture real-time data, process frames, and calculate physical-world positions of detected objects.

3. Detection Function
  This is the core function for object detection and aggregation of results:
  Takes an image and runs YOLOv8 detection on it.
Extracts:
  Bounding boxes around detected objects.
  Classes, confidence scores, and object names.
  Filters detections based on confidence (set at 0.1 or 10%)—only keeping higher-confidence detections.
  Calculates center points of each bounding box.
Appends:
  Bounding boxes to l1
  Center points to l2
  Saves the annotated image to a folder (Result_Image) for reference.
**🟢 Purpose:**
  Accumulates reliable object detection results from multiple images of different exposures.
4. Exposure Function (exp)
This function:
  Takes the initial input image and generates multiple versions of it by altering its exposure/brightness levels.
  Saves these exposure-variant images in a directory (Exposure_Image).
**🟢 Purpose:**
  By creating different exposures, the system aims to improve object detection accuracy, especially in variable lighting conditions. Objects missed in one exposure might be detected in another.

5. Euclidean Distance Function
  Calculates the distance between two points in a 2D space using the Euclidean distance formula.

**🟢 Purpose:**
  Used later to filter out duplicate detections of the same object by ensuring the same object isn't counted multiple times due to variations in detections.

**✅ Main Program Flow (if __name__=="__main__":)**
Step 1: Initialization
  Starts a timer to measure total processing time.
  Initializes counter to count processed images.
  Loads the base image (frame_1141.jpg).
  Calls the exp function to generate exposure-variant images from the base image.
Step 2: YOLO Model Loading
  Loads the YOLOv8 model trained on a custom dataset (best.pt).
Step 3: Processing Exposure Images
  Loops through all generated exposure images in the folder.
  For each image:
  Runs the detection function.
  Aggregates all detected bounding boxes (l1) and center points (l2).
Step 4: Draw Final Bounding Boxes
  After processing all exposures:
  Draws red rectangles (bounding boxes) on the original base image for each detected object based on l1.
Step 5: Filter Center Points
  To eliminate duplicate center points, it:
  Iterates through all center points in l2.
  Adds a point to the unique_data list only if it's not within a threshold distance (8 pixels) of any existing point.
  This ensures unique object detections are recorded, reducing duplicates from multiple exposures.
Step 6: Final Output
Prints:
  Final bounding boxes (l1)
  Total count of bounding boxes detected.
  Unique center points (unique_data) after filtering.
  Draws optional lines (commented out) that could serve as reference axes on the image (center lines).
  Saves the final annotated image (detected_image02.jpg) in the Result_Image folder.
  Displays the final image in a window titled "YOLOv8 Inference".
  Waits for a key press; if the key 'q' is pressed, the window closes.
**✅ Key Concepts Implemented**
Feature	Explanation
  Object Detection	YOLOv8 model detects objects on images with different exposures.
  Exposure Augmentation	Improves detection reliability by generating various exposure levels.
  Bounding Box Aggregation	Collects bounding box data from all processed images.
  Center Point Calculation	Finds the middle point of each detected object.
  Duplicate Filtering	Uses Euclidean distance to remove redundant detections.
  Realsense Camera Integration (Optional)	Potential to include real-time RGB-D data and 3D localization.
**✅ Possible Use Cases**
  Robotics: The unique center points and bounding boxes can help guide robotic arms or autonomous systems to specific objects in 3D space.
  Inspection Systems: Multi-exposure detection helps improve object detection under challenging lighting conditions.
  Autonomous Navigation: Using center point information and 3D coordinates for obstacle avoidance or target tracking.
  Agriculture (like your tea project!): Detecting specific plant parts with improved reliability under varied lighting.
**✅ Suggestions for Next Steps**
  Integrate Realsense for Real-Time Detection: Capture live RGB and depth data and process them on the fly.
  3D Coordinate Mapping: Convert center points to real-world coordinates (x, y, z) using the Realsense camera.
  Movement Control: Use the calculated 3D positions to control robotic actuators for picking or interacting with objects.
  Confidence Threshold Optimization: Experiment with higher confidence levels for more accurate detections.
  
