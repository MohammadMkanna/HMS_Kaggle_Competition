# HMS_Kaggle_Competition
The Harmful Brain Activity Classification competition, hosted by Kaggle, aims to identify seizures and other patterns of harmful brain activity in critically ill patients through analysis of EEG signal data and its corresponding spectrograms. In this repository, I developed a classification model capable of detecting six types of harmful brain activities (seizures, LPD, GPD, LRDA, GRDA, and others) using only EEG time signal data. This was achieved by utilizing scalograms generated via Complex Wavelet Transform. The model achieved a public score of 0.4, evaluated using the KL divergence metric on Kaggle notebooks with unseen data.
 
![Model](https://github.com/MohammadMkanna/HMS_Kaggle_Competition/assets/158570470/c99db432-585e-4dcb-bfde-b5e148271278)

This repository contains 3 notebooks:
•	Explanatory Data Analysis (EDA) for the training data.
•	Building and Training The model.
•	Inference on test unseen data (this step is executed on [Kaggle notebook](https://www.kaggle.com/code/mohammadmkanna/inference-hms/notebook))

Throughout the development process, several strategies were explored that did not yield significant improvements: 

• Building a dataset of non-log scale scalogram images:

I built a dataset containing IMAGE scalograms of each EEG data, but I did not use the log scale and I took 128 scales, it turns out that using log scale is important when creating scalograms according to the following paper [C. Torrence and G. Compo: “A Practical Guide to Wavelet Analysis”, Bulletin of the American Meteorological Society, vol. 79, no. 1, pp. 61-78, January 1998]( https://paos.colorado.edu/research/wavelets/bams_79_01_0061.pdf). Furthermore, using 128 scales resulted in capturing a wide range of frequencies, ultimately consuming unnecessary memory. Additionally, this approach represents images that are taken from the scalograms coefficients, not directly taking the coefficients leading to reduce the information in the scalograms. 
You can check the code [here]( https://www.kaggle.com/code/mohammadmkanna/eeg-scalograms) for forming the [dataset](https://www.kaggle.com/datasets/mohammadmkanna/all-eeg-spectrogram).

•	Building 2 input model from EfficientNet blocks:

The idea is from a paper published for OWL sound classification, However, the features utilized in the paper are spectrograms and MFCC features, which differ from those applicable in my case.

•	Fine Tuned the model on Ideal cases:

The dataset we possess includes ideal cases characterized by confident scores assigned to labeled classes, indicating widespread agreement among experts regarding specific classifications. Despite training the model with this data, no significant improvement was observed. However, it resulted in a certain degree of bias within the model.

Areas for further investigation:

• Change efficientV2B2 model to another model that contain attention layers (MaxVit for example which performed well as mentioned by one of the contributors).

• Alongside the 2D classification model, we can build 1D model that deals with EEG raw signal data.

