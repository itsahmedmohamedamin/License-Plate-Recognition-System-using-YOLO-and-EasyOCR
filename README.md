# License-Plate-Recognition-System-using-YOLO-and-EasyOCR

## Introduction

> This project develops a robust License Plate Recognition system built on the Ultralytics YOLO model and EasyOCR for text extraction. It utilizes Google Colab for execution, ensuring access to powerful computing resources and a seamless development environment.

## Features

* Object Detection: Uses YOLO (You Only Look Once) for fast and accurate object detection, specifically tuned for license plate recognition.
* Text Extraction: Implements EasyOCR to extract alphanumeric characters from the detected license plates.
* Interactive Visualization: Provides real-time image display functionality within Google Colab using cv2_imshow.
* Data Handling: Integrates with Roboflow for efficient data management and version control of datasets.
* Customizable Training: Allows for easy customization of training epochs, image size, and batch sizes.

## Installation

> Before running the application, install the necessary Python libraries by executing the following commands in your Google Colab notebook:

```
!pip install ultralytics
!pip install roboflow
!pip install easyocr
```
> Additionally, mount your Google Drive to access datasets and model files:
```
from google.colab import drive
drive.mount('/content/drive')
```

## Usage

### Step 1: Initialize the Image Processor
> Instantiate the ImageProcessor with the path to the pre-trained YOLO model:
```
processor = ImageProcessor('/content/drive/MyDrive/Licence_Plate_Model.pt')
```

### Step 2: Load and Predict
> Load an image and predict objects using the model:
```
image_path = '/content/path_to_your_image.jpg'
results = processor.load_and_predict(image_path)
```

### Step 3: Annotate and Crop
> Annotate detected objects and optionally crop them from the image:
```
cropped_images = processor.annotate_and_crop(cv2.imread(image_path), results, display=True, save_crops=True)
```

### Step 4: Extract Text
> Extract text from the cropped images using EasyOCR:
```
extracted_texts = processor.extract_text(cropped_images)
for text in extracted_texts:
    print(text)
```

## Dataset
> The license plate dataset can be downloaded from Roboflow:
```
rf = Roboflow(api_key="your_api_key")
project = rf.workspace("roboflow-universe-projects").project("license-plate-recognition-rxg4e")
version = project.version(4)
dataset = version.download("yolov8-obb")
```
## Model Training
> Train a YOLO model using the following parameters:
```
model = YOLO('yolov8l.pt')
train_results = model.train(data='/content/data.yaml', epochs=100, imgsz=640)
```

## Conclusion
> This system is ideal for developers and researchers looking to implement and enhance License Plate Recognition technologies using deep learning. It offers a foundation for further customization and scalability according to specific requirements.
