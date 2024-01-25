title: " Bollworm counting"
excerpt: "Counting and classifiying Bollworm images - zindi competition overview <br/><img src='/images/PINN_arrh/ezgif-7-b76792b954.gif' style='height: 400px; width:400px;' class='center'>"
collection: portfolio
---

# Counting and classifiying Bollworm images - zindi competition overview.



 ![Alt text](/images/Competitions/bollworm.jpg)


# Title: Participating in the XYZ Computer Vision Competition

I recently participated in the Bollworm counting Computer Vision Competition on Zindi, a challenging event that provided a platform to showcase my expertise in computer vision and machine learning. 

# Objective and Challenges:
The competition's objective was to count worms of each class in the image.
The metric is Mean absolute error. 

 The data for this competition has been collected from cotton farms across India since 2018, consisting of approximately 13,000 images. These images were captured using various app versions by different farmers and farm extension workers, making the dataset challenging and unique compared to other agricultural pest datasets. The dataset includes two types of images: one with pests, accompanied by bounding boxes indicating pest locations and labels denoting either "PBW" (pink bollworm) or "ABW" (American bollworm); the other type of image doesn't contain pests and lacks bounding box information, representing real-world user behavior, such as taking photos in an office to understand how the app works. The competition's objective is to accurately identify and count the number of pink bollworms and American bollworms per class in each image. Competitors are expected to develop models that address the challenges posed by the diverse and real-world nature of the dataset, emphasizing the relevance of the solutions in practical agricultural settings.

# Approach and Techniques:
The main focus at begining was having a functionnal baseline model and having an evaluation strategy that returns a value close to the value obtained on the public test leaderboard.

To acheive these two objectives, I chose to use a yolov5 model using the ultralytics repo.


### Prepping the dataset
To do this the dataset had to be adapted to the yolov5 format, including the bounding boxes, the format in the default parameters is $(x_r,y_r,w,h)$ where $(x_r,y_r)$ is the upper right point of the bounding box and $(w,h)$ the width and height of the bounding box, while the format used by yolo is $(x_c,y_c,w,h)$ where $(x_c,y_c)$ is the center of the bounding box:

 $x_c = x_r - w/2$ 
 
 and
 
$y_c = y_r - h/2$

### Training image size
For training since I use Kaggle notebooks with two tesla T4's, 
I chose an image size of 1280 for training, which gives reasonable training time (10 hours with 12 epochs on 4 folds).

### Evalution stratergy

For evaluation I used a 4 fold cross validation and still the cross validation metric don't match theleaderboard value, looking for the problem I discovered that the training and teh public test set don't have the same distribution in fact the test set contains more empty images with no worms, to balance the dataset I injected empty images to balance things out which improved the CV MAE.

Baseline CV MAE: 1.87 - LB MAE 2.54
# Improvements:
## 

## Hyperparameters
NMS IOU threshold and proba thresh

A smaller IOU threshold will eliminate good bounding boxes in the case where worms are really close to each other which is the case in a lot of images. We thus chose a bigger threshold than usual which leaves use with a model more prone to detecting false positives, which makes the model especially bad on images where there is no worms thats why one the improvements is to filter the no worm images before reaching the model.

## Image augmentations
To reduce overfitting image augmentation is used and improve generalization, it's also used during evaluation (test time augmentation) which improves validation MAE slightly.


#training augmentations  | #testtime augmentation
## Filtering empty images
Trained an efficientdet model for classification of empty images to avoid false positives triggered 


# Results and Recognition:

# Takeaways and Learning:
