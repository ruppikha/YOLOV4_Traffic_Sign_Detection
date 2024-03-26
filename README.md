**YOLOv4 Traffic Sign Detection**

**Introduction:**
This README provides instructions for setting up and using YOLOv4 for traffic sign detection using Google Colab. The YOLOv4 model is trained to detect various traffic signs in images.

**Setup Instructions:**
1. **Mount Google Drive:**  
   Run the following code in a Google Colab notebook to mount your Google Drive:
   ```
   from google.colab import drive
   drive.mount('/content/gdrive')
   ```

2. **Clone Repository:**  
   Clone the darknet repository for YOLOv4:
   ```
   !git clone https://github.com/AlexeyAB/darknet
   ```

3. **Prepare Dataset:**  
   Download the dataset given in the data folder containing images and corresponding labels for traffic sign detection.

4. **Configure Darknet:**  
   Inside the `darknet` directory, modify the `Makefile` to enable GPU and OpenCV support:
   ```
   %cd darknet/
   !sed -i 's/OPENCV=0/OPENCV=1/' Makefile
   !sed -i 's/GPU=0/GPU=1/' Makefile
   !sed -i 's/CUDNN=0/CUDNN=1/' Makefile
   !sed -i 's/CUDNN_HALF=0/CUDNN_HALF=1/' Makefile
   !sed -i 's/LIBSO=0/LIBSO=1/' Makefile
   ```

5. **Compile Darknet:**  
   Compile darknet with the modified configuration:
   ```
   !make
   ```

6. **Download Pre-trained Weights:**  
   Download pre-trained weights for YOLOv4:
   ```
   !wget https://github.com/AlexeyAB/darknet/releases/download/darknet_yolo_v3_optimal/yolov4.conv.137
   ```

**Usage Instructions:**
1. **Training:**
   - To train the model, use the following command:
     ```
     !./darknet detector train data/data.obj cfg/yolov4-custom.cfg yolov4.conv.137 -dont_show
     ```
   - Training progress can be monitored through the `chart.png` file generated in the `darknet` directory.

2. **Inference:**
   - To perform inference on a single image, use:
     ```
     img_path = "data/test.jpg"
     !./darknet detector test data/data.obj cfg/yolov4-custom.cfg backup/yolov4-custom_1000.weights {img_path} -dont-show
     ```
   - Adjust the `img_path` variable to the path of the image you want to test.

**Additional Notes:**
- Results of inference will be saved as `predictions.jpg` in the `darknet` directory.
- Displaying images using matplotlib can be achieved with the provided helper function `imShow()`.

**Important Considerations:**
- Ensure proper dataset organization and label format for successful training.
- Monitor training progress to ensure model convergence.
- Adjust inference commands for different images as needed.

**Conclusion:**
This README provides a concise guide for setting up and using YOLOv4 for traffic sign detection in Google Colab. For further assistance or inquiries, refer to the documentation or contact the repository owner.
