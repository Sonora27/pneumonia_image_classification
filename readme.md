# Detecting Pneumonia from X-Ray Images Using Convolutional Neural Network

Jose Ramirez and Yasir Karim

Sources: [Kaggle](https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia)

## Social Case

Pneumonia is a common, but serious lung infection that disproportionately affects the young, the elderly, and
the immunocompromised. It is the leading cause of death among children under the age of 5. For the elderly, they have a significantly higher chance of being diagnosed with the disease and of dying from it as well. Although pneumonia vaccines exist for high-risk individuals, they are only available for some but not all causes of the disease.

Stunningly, the USA has shown negligible improvements in decreasing the death rate from pneumonia over the last half century even as antibiotics have become much more prevalent. To tackle this daunting illness, a system must be devised that can detect pneumonia in its early stages, so that it can be properly treated before it becomes more serious and harder to treat. We have been tasked to create such a system by using deep learning to detect pneumonia from X-Ray images.

## Repository Structure

pngs - folder that contains visualizations that were utilized in our analysis

CNN_modeling_v1.ipynb - jupyter notebook that contains EDA and initial models

AdamW_modeling.ipynb - jupyter notebook that contains AdamW models as well as post model analysis

presentation.pdf - contains pdf version of project presentation

README.md


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

To address our class imbalance, we used both data augmentation as well as class_weights.

### Stochastic Gradient Descent

This prelimnary model achieved a promising recall of 93.33%, but accuracy lagged behind at 82.05%. In addition, the model vastly overfitted to the data.

### Adam

Using the Adam optimizier, we were able to rectify our overfitting issues somewhat and achieve an excellent recall of 98.72%, but our accuracy suffered at 79.33%.

### AdamW

Our strongest overall model ended up being an AdamW model. The AdamW optimizer performs so well because it performs weight decay after controlling the parameter-wise step size. This model gave us an excellent recall score of 93.85% and an excellent accuracy score of 91.51%. It was able to accomplish this while minimizing overfitting better than our previous models. Overfitting ended up being best handled in this models by simplfying our previous layers.

### Results

<img src="https://raw.githubusercontent.com/Sonora27/pneumonia_image_classification/master/PNG/confusion_matrix.png">

<img src="https://raw.githubusercontent.com/Sonora27/pneumonia_image_classification/master/PNG/adamw.png">

As you can see from the above visualizations, this model was able to combine excellent recall and accuracy while controlling for overfitting better than any other model.

## False Prediction Analysis
<img src="https://raw.githubusercontent.com/Sonora27/pneumonia_image_classification/master/PNG/false_negatives.png">
<img src="https://raw.githubusercontent.com/Sonora27/pneumonia_image_classification/master/PNG/false_positives.png">

When we analyzed where our model mispredicted, we found there to be an issue with the images themselves moreso than the actual model being faulty. To the naked eye, the false negative images look to be in fact negative even though they are truly positive. There is very little opacity present in these photos. The fact that the images seem to be rather dark seems to be playing a large role in the misclassification.

Similarly with the false positives, the images look to be in fact positive. There appears to be a high amount of opacity present in these photos and yet, they are in fact negative.  The high amount of brightness of the photos seems to be contributing to the misclassification as well.

## Next Steps

Although our model shows very promising results in its ability to detect pneumonia, it might not be the surest method in detecting pneumonia in its early stages. Upon consultation with industry professionals, we have leaned that radiological evidence of pneumonia often lags behind clinical synptoms of pneumonia. Building a similar pneumonia detection system using CT scans might further help us in our goal of detecting pneumonia as early as possible because a CT scan of the chest is significantly more sensitive for detecting pneumonia in its early stages.

