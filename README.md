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

### 1. Data Management ###
  - **MongoDB & Batch Processing:**
    Since data is really big for playing with only one machine with considerably low computational power, there must be efficient way to read data in python, and then build Deep learning model on the data. MongoDB is excellent for this purpose; where whole training data is loaded to mongoDB and then data in form of batches was read. We can also change the datasize by specifying the batch size by defining number of row in *batch* variable in the [code.](https://github.com/hamzafar/cdiscount-image-classification-challenge/blob/master/training/Train%20Simple%20Model%20on%20all%20data.ipynb)
  - **Class Encoding:**
    The number of class for the problem were *5200* that is really high multi-class classification problem, and single row might have (1,5200) values at output layer for encoding purpose. So, we first converted all labels values to respective encoding values ie. each row and (1,5200) shape, and instead of reading for disk each time, we have saved whole processed label data to mongodb with row_id and encode values, and during read time instead of reading and converting to encode whole class labels, we just read it from mongodb by comparing product_id in train dataset and encode dataset. [Encode class ipython notebook](https://github.com/hamzafar/cdiscount-image-classification-challenge/blob/master/preprocessing/Encode%20Class%20Labels.ipynb) contains all procedure.
  
### 2. Model Training ###
  - **Simple Model & Complex model:**
    We just tried two type of custom deep learning architecture. In first approach we made a [simple strucutre](https://github.com/hamzafar/cdiscount-image-classification-challenge/blob/master/training/Train%20Simple%20Model%20on%20all%20data.ipynb) of CNN with only convolutional layer with 40 filters and this training is done only for two epochs. Then more and more layers are included to reduce training error on sample data to ~0. The [bigger network](https://github.com/hamzafar/cdiscount-image-classification-challenge/blob/master/training/Train%20Simple%20Model%20on%20all%20data.ipynb) contains ~3 million parameters. We have focused on bais-variance trade of by simple trick i.e. reduce error near to zero on sample data and include more and more data to reduce high variance. Since we have penalty of data so we need to worry much about this.
  
  - **Transfer Learning:**
    In this processing, InceptionV3 model weights are used for Transfer Learning. The typical architeciture works on freezing  FC7 (Last layer of model) layer and learn new classes of data. Since InceptionV3 was trained on 150X150 image size; the images are resized to 150X150. One can see [code.](https://github.com/hamzafar/cdiscount-image-classification-challenge/blob/master/training/Transfer%20Learning%20with%20InceptionV3.ipynb)
---
### Results/Discussion ###
- Training on such big data is really a big challenging when you don't have enough resuorces. Although we only can train on 2 million rows and had to stop it because of memory crash but this is the awesome competition that make muscle strong with playing with complex problems like Cdiscount.

- To see how we are obtaining results, we just simply worked on 200,000 dataset and get predictions to see how accurately our [model](https://github.com/hamzafar/cdiscount-image-classification-challenge/blob/master/training/Train%20on%20Sample%20data%20and%20get%20prediction%20on%20same%20data.ipynb) is acheiving. 

- Further, The model that was trained on 2 million rows; the weight of this model were saved and we get predictions on the [test-set](https://github.com/hamzafar/cdiscount-image-classification-challenge/blob/master/prediction/predict.ipynb) for kaggle submission

