# cdiscount-image-classification-challenge

## Description

the challenge focuses on building a model that automatically classifies the products based on their images. As a quick tour of [Cdiscount.com's](https://www.cdiscount.com/) website can confirm, one product can have one or several images. The data set Cdiscount.com is making available is unique and characterized by superlative numbers in several ways:

- Almost 9 million products: half of the current catalogue
- More than 15 million images at 180x180 resolution
- More than 5000 categories: yes this is quite an extreme multi-class classification!

## Data Description
Data is provided in bson file structure in both train and test set in the format of dictonary i.e. Each dictionary contains a product id (key: _id), the category id of the product (key: category_id), and between 1-4 images, stored in a list (key: imgs).
This compettion has really big data (for one machine) that contains 58GB of Train data and 14GB of Test data with 7,069,896 rows in train data and  1,768,182 in test data.

## Workflow:

Although the training results can't be acheived as high, due to limitation of computation power, but following are the steps/achievement that are done for managing such a big data.

1. Data Management
  - mongodb
  -  batch processing
  - class encoding (5200)
2. Model Training
  - simple model
  - complex model
  - **Transfer Learning**
    In this processing, InceptionV3 model weights are used for Transfer Learning. The typical architeciture works on freezing  FC7 (Last layer of model) layer and learn new classes of data. Since InceptionV3 was trained on 150X150 image size; the images are resized to 150X150. One can see [code.](https://github.com/hamzafar/cdiscount-image-classification-challenge/blob/master/Transfer%20Learning%20with%20InceptionV3.ipynb)
  
  - Overfiting and underfiting
3. Results/Discussion
  - Overall experience
  - test result
  
