# Multilabel Classification of Skill Sets

### 01.11.2020 - Houssam AlRachid
─
## Introduction

A job title says a lot about a person's role, responsibilities and skills. It says if they manage a team, if they control a budget, their level of specialization and many other things.
Another example, we are currently in the area of ​​digitizing job search or integrating artificial intelligence into various job sites dedicated to connecting job seekers and employers. But this online market is still very fragmented and inefficient. Job seekers find it difficult to know what skills are desired, while employers have consistently run out of qualified candidates by searching the CV database. To fill the information gap, we seek to find connections between the job descriptions and the requested skills.
The major aspect of this project is to develop a best suited algorithm that can predict the skills of a job by going through the title and the description provided. We will implement Natural Language Processing (NLP), a Convolutional Autoencoder (AE), and a Deep Neural Network (DNN).​

## Exploratory Data Analysis

We used several databases containing a lot of information about jobs, titles, skills ...
We aggregate in a new dataframe all needed datas from these files. The created dataframe 226493 entry.

The data set features can be summarized as follow:

- job_id: a unique index for each type of jobs;

- Description: a text describing the job;

- Title: The job title;

- Skill: The associated skill.

## Feature Engineering and ETL

### Data Collection

We cleaned our dataframe from empty values and we checked that nothing is missing.

### Data Engineering

We created new features by generating text features, part of speech features, and finally collected all the job tags for each job id to remove duplicate rows.

### Feature Processing

We reduced the number of words and therefore the number of variables for input into our model by reducing words down to their root form. We do this through cleaning, stripping, and stemming. We then use feature hashing so our input space can recognize new words it has not seen. We then add all the features we created and the text data into one dataframe and send it to our model.

## Methodology

In this present project, we will focus on developing a best suited algorithm to detect skills from a job's description and title. The methodology can be resumed in the following steps:
1. We first trained an autoencoder to reduce the dimensionality of our input data to 100 columns ;
2. We used a Deep Neural Network to predict data encoded. Analysis

### Autoencoder (AE)

#### Building the model:
We first trained an autoencoder to reduce the dimensionality of our input data (X) to 100 columns (Dimension reduction). We train a convolutional Autoencoder with 4 convolution/pooling steps and 3 hidden layers that is symmetric around the center of the network. The input to the network is the same as the output of the network. This way our network is trained to learn a representation of the data. This essentially compresses the data with some losses.
After we train the autoencoder on our dataset we can then cut off the decoder and use the encoder as the first step in our model.

### Deep Neural Network (DNN)

#### Building the model

The Autoencoder is trained. We will use it to predict data encoded that will be used in the Deep Neural Network. Next, we use a Deep Neural Network with 5 hidden layers :
Input->200->150->100->50->25->Output.
We use Rectified Linear Units ('relu') for the activation of each hidden layer and apply a dropout.

### Evaluation

After encoding the Descriptions, we send the data into the DNN. We scored an 99.74% accuracy on both the training and testing set. We can visualize accuracy and loss during training in Tensorboard.

   
 5
 Conclusion
Our project studied the problem of predicting job skills based on titles and descriptions sets as a multiclass classification problem in Deep Learning. After performing data analysis and feature engineering, we applied an Autoencoder model followed by a Deep Neural Network model.
Overall the model was successfully able to predict job tags at ​99.74%​ accuracy. We think that this is very satisfying accuracy. We think that having bigger databases could decrease this value, but at least we can trust our model for bigger and more complex datasets.
