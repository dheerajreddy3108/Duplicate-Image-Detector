# Duplicate-Image-Detector
A repository that helps to find the duplicate images in the dataset with the help of OpenCV and imutils library


The task given to me is to eliminate duplicate images in the given data set. It is important to look for duplicates in the dataset as they affect the performance of the model to large extent. Duplicate images make the model remember features instead of finding the patterns in the dataset. Duplicate images provide more ways for the network to remember features instead of learning and truncating the model’s ability to generalize. It also reduces the model ability to classify or detect an object during the test time. 
Detecting similar images using a manual approach is hard and more time-consuming. It is also prone to human errors. In many cases, humans introduce bias as well. So, manual inspection of the dataset is to be avoided. 
To do this, we need to perform operations based on the image contours area. The code is formatted in the way explained below.

i.Importing Libraries

ii.Defining functions to perform preprocessing steps on Images

iii.Helper Functions

iv.Function to calculate minimum contour areas 

v.Loop to compare 2 images iteratively to remove if any duplicates are there in the directory.

### Importing Libraries ###

The versions of the libraries I used are

NumPy - 1.19.2

OpenCV - 4.5.3

imutils - 0.5.4

tqdm - 4.62.0


### Helper Functions ###

I have defined few helper functions to perform the task. First is a function to load all images in the data directory to a list along with the name of image file.
The function only considers the .png files in the data directory. 

![Capture3](https://user-images.githubusercontent.com/55786239/139812846-353b8d6d-8b54-4b89-9dd5-f74d541da44c.PNG)

Next a function to give gray scale images with gaussian blur applied to each image

![Capture5](https://user-images.githubusercontent.com/55786239/139813066-a7763f7b-334a-4166-8012-ede4936e8ca1.PNG)

### Function to calculate minimum contour areas ###

To calculate contours I have applied AdaptiveThreshold method first to the image. Adaptive Threshold considers a small region of neighbouring picels to compute threshold value for the local region of an image. This helps us to avoid the issue of manually setting up the range of values for thresholding.
A loop is taken to calculate areas for all the contours in the image that have an area of more than 10.

![Capture4](https://user-images.githubusercontent.com/55786239/139813328-1b714b1a-a442-445c-a340-b6a137684a27.PNG)

I have done experiments with different values to eliminate small contours in the image and considered value of 10.
From the statistics it is clear that more than 40% of the areas are smaller or equal to value of 10.

![Capture11](https://user-images.githubusercontent.com/55786239/139814249-537b4e33-cd78-4f25-80c8-0e2b89f616b5.PNG)


The final step is to take the predefined function and compare two images. To compare a single image to all other images it is also important to check if we are comparing same images more than once. So, it has been checked and no two images are compared more than once. Also, same image is not compared. 

![Capture7](https://user-images.githubusercontent.com/55786239/139814742-ce9c73cf-e1c4-46f7-9046-b5a74486fe6a.PNG)

Outer for loop is used to take the first image into consideration. The inner loop takes all the images other than the image taken in the outer loop. Here we name the first image as prev_frame along with the file name. Then we take the minimum contour areas we calculated beforehand. We take the average of two values. If the two images are the same, then the two images will have the same contour area and the score from the function compare_frames_change_detection will be zero. If the two images are different the score will be greater than 0. The more the two images are different the higher the score will be. We increase the value of the variable called count by 1 and then the prev_frame_name is appended into the duplicate_images_list.

If there are any duplicate images in the directory all the file names are in the list, and we remove the duplicate images in the directory.

![Capture9](https://user-images.githubusercontent.com/55786239/139814886-261af741-f122-42fd-a403-3529591c4b6a.PNG)


## Testing the Program ##

I have manually copied few images to a new directory and renamed the duplicate images. I have ran the program with that data directory and by considering all the images in the data directory. The program was 100 % able to detect all the duplicate images and the duplicate images are appended into the list. The results are attached in the image below.

![Capture12](https://user-images.githubusercontent.com/55786239/139815378-fb3769e0-00e3-4b8d-b029-cf7850ea46fe.PNG)
