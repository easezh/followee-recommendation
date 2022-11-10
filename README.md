# Instructions to obtain the pre-processed datasets and to run the model PE-LDA

1. The original version of the dataset used in our study is an open dataset that can be downloaded at https://www.kaggle.com/datasets/hwassner/TwitterFriends/download?datasetVersionNumber=2 (login may be required). Detailed information on the dataset is available at https://www.kaggle.com/datasets/hwassner/TwitterFriends.
A data backup is also available at https://drive.google.com/file/d/13BLIS_eQTdz6XsHkERQYDAI3vWtDMM-p. 

2. Since both the original and pre-processed datasets exceed the maximum capacity of the platform (25MB), we provide interactive python notebook (.ipynb) files containing the pre-processing procedure and PELDA code to get the pre-processed datasets and the results used in our study. Please refer to src/data_preprocessing.ipynb and src/PELDA.ipynb for more details.

3. You must first run data_preprocessing.ipynb to obtain the pre-processed datasets before running PELDA.

4. If you use the code or the pre-processed datasets in this repository, please cite the paper "Integrating Users’ Contextual Engagements with Their General Preferences: An Interpretable Followee Recommendation Method". 
