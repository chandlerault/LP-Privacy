# LP_privacy
### Running the Program
The license plate privacy detection and blurring system can be tested for personal use on Google Colab. First, ensure that the proper packages are installed in the Colab runtime:
``` python 
!pip install opencv-contrib-python==4.4.0.44
!apt install tesseract-ocr
!apt install libtesseract-dev
!pip install pytesseract
!git clone https://github.com/Dreamweaver2k/LP_privacy.git 
```

Once these have finished loading, you will have all the necessary files to detect and blur license plates in your personal videos as well as the the dependent packages. Now, you can run detect.py to perform the privacy function on your specified video:
``` python
!python LP_privacy/LP_privacy/detect.py --source destination/to/video/folder --weights LP_privacy/LP_privacy/weights/best.pt  --conf-thres .2 
```
Note that the source flag must point to a folder containing your video file.

### Training New Weights
To train new weights, you will need to download YOLOv5. Once this is done, you can utilize the Chinese City Parking Dataset [^1] (CCPD) which I have annotated for use in a YOLO. See reference for original dataset. 
To download YOLOv5, run the following:
``` python 
!git clone https://github.com/ultralytics/yolov5
```
To train new weights, run the following:
``` python
%load_ext tensorboard
%tensorboard --logdir runs/

!python yolov5/train.py --img 416 --batch 4 --epochs 20 --data LP_privacy/LP_privacy/dataset/data.yaml --cfg yolov5/models/yolov5l.yaml --name lpmodel
```
