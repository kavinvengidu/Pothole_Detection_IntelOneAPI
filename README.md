Pothole Detection via ResNet50
==============================

This whole Project was primarly build for the **__Intel OneAPI competition 2023
Pothole Detection__**


## Abstract
This Project is based upon collection of images from phone application's and usinng Deep Learning
Technique( Mask RCNN ), we have trained a custom machine learning model for detection of potholes
inside images and plot them on google maps,which includes the size of the pothole inside image.

Pothole detection Accuracy **__81%__** in different environments

The main files are ````Final_file_for_tata_innoverse.ipnb````

if you require to train your own custom Machine learning model from the same dataset
run this simple command referenced from the 
```
python3 custom.py train --dataset=customImages --model=/path/to/weights.h5
```

![Pothole Detected](https://media.giphy.com/media/Xc9DFuCIIiouihgfzZ/giphy.gif)  ![Original Images Link](https://media.giphy.com/media/jpKRIVzNVJv3VEegTZ/giphy.gif)


## Team

- [Kavin V](https://www.linkedin.com/in/kavin-v-8028b9229/)
- [Harish R](https://www.linkedin.com/in/harish-r-b6b045229/)


## SETUP
We have used variety of Datasets  :

Install **youtube-dl** to __download files from google drive__ directly in terminal
```
https://github.com/ytdl-org/youtube-dl#installation
```
#### Training Dataset
To increase the model accuracy , For the training dataset we have trained them _5 types of dataset.._
- Original Dataset Links
```
Sunny Dataset
Anue Dataset
Road Damage Dataset (Adachi)
Rick_set6
Kitti image Dataset
```
If you want to add your own dataset into our dataset. We have **resized all the images** for faster processing to **800x800**, Please do same with your images too
```python
from PIL import Image
import os
from resizeimage import resizeimage

count = 0

for f in os.listdir(os.getcwd()):
    try:
        with Image.open(f) as image:
            count +=1
            cover = resizeimage.resize_cover(image, [800,800])
            cover.save('pgm-1_{}.jpg'.format(count),image.format)
            print(count)
            os.remove(f)
    except(OSError) as e:
        print('Bad Image {}{}'.format(f,count))
```


We have also done annotion of all the images present there,
Annotion images

- For Annotation of images we have used roboflow
````
https://roboflow.com/
````
**__After annotion around 1000 images then we create this dataset__**


**Download these files**

| Folder Name        | Download Link           |
| -------------------|:-----------------------:|
| Train | [Gdrive link](https://drive.google.com/file/d/1PGhXUnaJDpcjgoLEhNn9gRvGZGRCzWUt/view?usp=sharing) |
| Val      | [Gdrive link](https://drive.google.com/file/d/1PGhXUnaJDpcjgoLEhNn9gRvGZGRCzWUt/view?usp=sharing)     |

We have created this Dataset for final testing of the model
This folder contains videos and photos that we recorded in May 2019
**[Test Dataset Download Link](https://drive.google.com/drive/u/2/folders/1duZ9O0If8mpHk8lZkFHQifv5R8z4dcKx)**
```

**For custom Training Process**
````
extract the zip files and create a folder named as "customImages" and move both folders
(train) & (val) folder directly inside it and then run the command

Structure for the whole Test Dataset Links
````
├── test_dataset
├──----- Photos
├──----- IMG_7300.MOV
├──----- IMG_7301.MOV
├──----- IMG_7310.MOV
├──----- IMG_7311.MOV
├──----- IMG_7312.MOV
````
#### We have trained model till 160 epoch
- As our accuracy of our model is 81% people who want to replicate in between and can take it
  the higher accuracy feel free to download
- we are also providing the different stage of trained model so that people who want to consider
  it to use in transfer learning can also use this

- If you are retraining the model then specify path from the epoch h5 else give a base model path provided on github 


| Epochs        | Download Link           |
| -------------------|:-----------------------:|
| base model | [Github link](https://github.com/matterport/Mask_RCNN/releases)|


**Custom Training Process**
```bash
python3 custom.py train --dataset=customImages --weights=mask_rcnn_damage_0160.h5 --logs logs/
```

**Background Training Process**
````bash
nohup python3 custom.py train --dataset=customImages --weights=mask_rcnn_damage_0160.h5 --logs logs/&
````









## References used
- [Matterport MaskRCNN](https://github.com/matterport/Mask_RCNN)
- [Priya Diwani](https://www.analyticsvidhya.com/blog/2018/07/building-mask-r-cnn-model-detecting-damage-cars-python/)
- [CrowdAi](https://www.crowdai.org/)


_Feel free to contact me if you have any questions and/or suggestions _
**_[pradyumg@gmail.com](mailto:pradyumg@gmail.com)_**
