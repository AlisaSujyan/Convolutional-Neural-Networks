## YOLOv8 Object Detection on Pascal VOC 2012 – Experiment Comparison

This project compares two YOLOv8 training experiments on the Pascal VOC 2012 dataset. Both experiments use the same architecture (yolov8n) and evaluation script, but differ in training configuration:

### Experiment Setup
| Feature           | First Experiment  | Second Experiment |
| ----------------- | ----------------- | ----------------- |
| Dataset Split     | train/val split   | combined train+val |
| Epochs            | 30                | 60                |
| Data Augmentation | Basic             | Strong            |
| Batch Size        | 8                 | 16                |
| Training Mode     | normal            | best              |

### Evaluation Metrics
Both models were evaluated on the Pascal VOC 2012 validation set, using a unified evaluation pipeline that calculates:

* mAP@0.5 and mAP@0.5:0.95

* Detection Accuracy

* Classification Accuracy

* Precision, Recall, F1-score

* Mean IoU


### Result Summary
| Metric                  | First Experiment | Second Experiment |
| ----------------------- |------------------|---------------|
| mAP\@0.5                | **0.7109**       | **0.7109**    |
| mAP\@0.5:0.95           | 0.5176           | **0.5177**    |
| Detection Accuracy      | 0.5617           | **0.5776**    |
| Classification Accuracy | **0.8133**       | 0.7139        |
| Precision               | **0.8133**       | 0.7139        |
| Recall                  | 0.6448           | **0.7516**    |
| F1 Score                | 0.7193           | **0.7323**    |
| Mean IoU                | **0.8704**       | 0.8359        |
| Evaluated Detections    | 295              | 295           |


### Conclusion
This comparative analysis shows that increasing training epochs, augmentations, and batch size leads to significant improvement in detection and classification performance using YOLOv8.
___

### Inference & Visualization with Webcam and Video

This project also includes scripts for running YOLOv8 object detection live on a webcam feed or on a video file, using the trained model weights (yolo_voc_final.pt).

Key Features
* Real-time object detection on webcam input with bounding boxes and class labels.

* Offline video detection with the option to save the output annotated video.

* Uses predefined Pascal VOC classes and colors for clear visualization.


#### How to Use
1. Load the trained model
```
from ultralytics import YOLO

model = YOLO("yolo_voc_final.pt")
```

2. Run Webcam Inference

Launch a live webcam window with detected objects overlayed. Press q to quit.
```
run_webcam(model, conf=0.5)
```

3. Run Video Inference

Detect objects in a video file, display the annotated frames live, and optionally save the output video with detections.

```
run_video(model, "path/to/video.mp4", conf=0.5, save_output=True)
```
* The output video will be saved as output_<original_video_name>.mp4 in the current directory.

* Press q to stop the video window.

#### Dependencies
* OpenCV (cv2) for video capture, display, and saving output.

* ultralytics package for YOLOv8 inference.

* Make sure your system has a working webcam for live detection.