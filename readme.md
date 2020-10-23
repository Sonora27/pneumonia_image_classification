# Detecting Pneumonia from X-Ray Images Using Convolutional Neural Network

Jose Ramirez and Yasir Karim

Sources: [Kaggle](https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia)

## Social Case

Pneumonia is a common, but serious lung infection that disproportionately affects the young, the elderly, and
the immunocompromised. It is the leading cause of death among children under the age of 5. For the elderly, they have a significantly higher chance of being diagnosed with the disease and of dying from it as well. Although pneumonia vaccines exist for high-risk individuals, they are only available for some but not all causes of the disease.

Stunningly, the USA has shown negligible improvements in decreasing the death rate from pneumonia over the last half century even as antibiotics have become much more prevalent. To tackle this daunting illness, a system must be devised that can detect pneumonia in its early stages, so that it can be properly treated before it becomes more serious and harder to treat. We have been tasked to create such a system by using deep learning to detect pneumonia from X-Ray images.

## Repository Structure


## Data

To construct our pneumonia detection system, we utilized a dataset from Kaggle that contained 5,856 images. There was a significant class imbalance that we had to deal with as we had 3 times as many images that showed pneumonia in comparison to the healthy images:

<img src="https://raw.githubusercontent.com/Sonora27/pneumonia_image_classification/master/PNG/pneumonia_imbalance.png">

## Exploratory Data Analysis

<img src="https://raw.githubusercontent.com/Sonora27/pneumonia_image_classification/master/PNG/x-ray_scans.png">

As you can see from the above images, pneumonia is often indentified in X-rays as showing increased lung opacity. In other words, the lungs in the images with pneumonia are less transparent. In addition, a doctor looking for pneumonia in an X-ray looks for infiltrates, which are lines or streaks of opaque white within the lungs.

## Evaluation Metrics

For this project, our most important evaluation metric is recall. This is because we want to reduce false negatives as much as possible. The worst outcome for a doctor when evaluating an X-ray scan for pneumonia is to tell the patient they are healthy when in fact, they have pneumonia. We want to hold our pneumonia detection system to this same standard when evaluating X-rays.

In addition, we included accuracy as a second evaluation metric. Since our classes are heavily imbalanced, we wanted to make sure that our detection system is not simply getting good results based off the class imbalance alone. 

## Modeling

### SGD

### Adam

### AdamW

Our strongest overall model ended up being an AdamW model. The AdamW optimizer performs so well because it performs weight decay after controlling the parameter-wise step size. This model gave us an excellent recall score of 93.85% and an excellent accuracy score of 91.51%. It was able to accomplish this while minimizing overfitting better than our previous models. 