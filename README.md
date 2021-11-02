# Duplicate-Image-Detector
A repository that helps to find the duplicate images in the dataset with the help of OpenCV and imutils library


The task given to me is to eliminate duplicate images in the given data set. It is important to look for duplicates in the dataset as they affect the performance of the model to large extent. Duplicate images make the model remember features instead of finding the patterns in the dataset. Duplicate images provide more ways for the network to remember features instead of learning and truncating the model’s ability to generalize. It also reduces the model ability to classify or detect an object during the test time. 
Detecting similar images using a manual approach is hard and more time-consuming. It is also prone to human errors. In many cases, humans introduce bias as well. So, manual inspection of the dataset is to be avoided. 
To do this, we need to perform operations based on the image contours area. The code is formatted in the way explained below.

Importing Libraries

Defining functions to perform preprocessing steps on Images

Helper Functions

Function to calculate minimum contour areas 

Loop to compare 2 images iteratively to remove if any duplicates are there in the directory.

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

Then a function to calculate the contour areas for all the contours in the image that have an area of more than 10.
I applied AdaptiveThreshold method before extracting contours from the image.

![Capture4](https://user-images.githubusercontent.com/55786239/139813328-1b714b1a-a442-445c-a340-b6a137684a27.PNG)

I have done experiments with different values to eliminate small contours in the image and considered value of 10.
From the statistics it is clear that more than 40% of the areas are smaller or equal to value of 10.

![Capture11](https://user-images.githubusercontent.com/55786239/139813582-b74627e7-1edb-4d5b-3e1-66edd1ddd306.PNG)

### Function to calculate minimum contour areas ###

As we are considering minimum contour areas, it is important to calculate them before we start comparing two images. This is because consider an example where we have 5 images in the directory. 
If we are comparing these 5 images, if we don’t calculate the contour areas before then we must calculate the same contours again and again which is computational burden, and this slows down the program. 

