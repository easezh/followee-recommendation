![INFORMS_Journal_on_Computing_Header](https://user-images.githubusercontent.com/44605491/208304431-b02fb847-3ca7-4dd5-9f27-06535ec90737.jpeg)

# Preference-Engagement Latent Dirichlet Allocation (PE-LDA) Model: An Interpretable Followee Recommendation Method

## Citation
If you use the code in this repository, please cite the paper "Ran Y, Liu J, Zhang Y (2022) Integrating users’ contextual engagements with their general preferences: An interpretable followee recommendation method. INFORMS Journal on Computing, accepted." Below is the BibTex for citing this version of the matirial. 
```
@article{PELDA2022,
    author    = {Yaxuan Ran, Jiani Liu, and Yishi Zhang},
    publisher   = {INFORMS Journal on Computing}
    title     = {Integrating Users’ Contextual Engagements with Their General Preferences: An Interpretable Followee Recommendation Method},
    year      = {2022},
    doi       = {10.5281/zenodo.7454449},
    url       = {https://github.com/easezh/followee-recommendation}   
}
```

## Abstract
Users’ contextual engagements can affect their decisions about who to follow on online social networks because engaged (vs. disengaged) users tend to seek more information about the interested topic and are more likely to follow relevant accounts successively. However, existing followee recommendation methods neglect to consider contextual engagement by only relying on users’ general preferences. In the light of the chronological characteristic of the user’s following behavior, we draw on the engagement theory and propose an interpretable algorithm, namely Preference-Engagement Latent Dirichlet Allocation (PE-LDA), which integrates users’ contextual engagements with their general preferences for followee recommendation. Specifically, we suggest that if a user is engaged in the current interest, he/she will be more likely to select a followee relevant to that interest. If not, the user tends to select a followee according to his/her general preference. To implement this framework, we extend the original LDA by (1) introducing an indicator to represent whether the user is engaged in the current interest or not, and (2) allowing a potential dependency between a user’s successive interests to describe the condition of contextual engagement. We conduct extensive experiments using a real-world Twitter dataset. Results demonstrate the superior performance of PE-LDA compared with several existing methods.

## Data and instructions to run PE-LDA model
The original version of the dataset used in our study is an open dataset. You can find and download the raw dataset at https://www.kaggle.com/datasets/hwassner/TwitterFriends/download?datasetVersionNumber=2 (login may be required). Detailed information on this dataset is also available at https://www.kaggle.com/datasets/hwassner/TwitterFriends. A data backup is also available at https://drive.google.com/file/d/13BLIS_eQTdz6XsHkERQYDAI3vWtDMM-p. 

Since both the original and pre-processed datasets exceed the maximum capacity of the platform (25MB), we provide interactive python notebook (.ipynb) files containing the pre-processing procedure and PE-LDA code to get the pre-processed datasets and the results used in our study. Please be aware that if you want to run the PE-LDA model, you must first download this dataset and pre-process it with `data_preprocessing.ipynb` in the src folder. 

The code `PELDA.ipynb` implements PE-LDA model, makes followee recommendations, and generates evaluation results. Specifically, in this implementation, we first define four sampling functions to draw samples from Beta, Binomial, Dirichlet, and Multinomial distributions. Then, we train Gibbs sampler to estimate latent variables. Detailed derivations are given in `appendix.pdf`. In our paper, PE-LDA was implemented in C in our experiments. It is available based on reasonable request. Finally, we evaluate the recommendation performance of PE-LDA using Conversion Rate@N ($CR@N$) and Normalized Discounted Cumulative Gain@N ($NDCG@N$), both metrics are widely adopted in previous literature. 

## Prerequisties (please install the following packages before you run our PE-LDA model)
- python 3.6
- numpy 1.19.2
- pandas 1.1.3
- gensim 3.8.3
- tqdm 4.50.0

## Appendix
The appendix.pdf is the online supplementary material for the paper "Integrating Users’ Contextual Engagements with Their General Preferences: An Interpretable Followee Recommendation Method". It includes: 
- The Preliminary Study in the Theoretical Foundation Section
- Literature Summary on LDA-based Followee Recommendation
- Derivation of Equations (2) - (3), i.e., the update equation from which the Gibbs sampler draws the hidden variable in our PE-LDA model
- Summary of the Recommendation Methods Applied in Our Experiments
- Convergence Analysis
- Sensitivity Analysis: Impacts of $\alpha$ and $\beta$

## Experimental results 
Table 3 in the paper shows the performance comparison of our PE-LDA and various other benchmark methods
<img width="1000" alt="Results; Table 3" src="https://user-images.githubusercontent.com/44605491/205712612-9aa9e26d-3630-442d-a7df-d4515491d1e8.png">

Figure 5 shows the comparison of the execution time (i.e., computation cost) of PE-LDA and other benchmarks.
<img width="693" alt="Results; Figure 5" src="https://user-images.githubusercontent.com/44605491/205713990-d121fab3-28f1-4e70-8ab8-1e9c3f24cb9c.png">

Figure 6 shows the results of sensitivity analysis w.r.t the number of interests (i.e., topic). 
<img width="810" alt="Results; Figure 6" src="https://user-images.githubusercontent.com/44605491/205714840-4f2abd63-4c2f-443c-876e-fb6bdcf09dd3.png">

You can access more results from the original paper. 

## Contributions
The present study makes several contributions. 
- First, to the best of our knowledge, it represents the first attempt to incorporate contextual engagement, a critical factor determining users’ following behaviors, to make interpretable followee recommendation. 
- Second, it contributes to the literature on user representation learning that seeks to represent a user as a vector based on his/her historical behaviors. By modeling the dependencies of users’ successive following decisions, the representation of the user can be interpreted as his/her general preference with the state of contextual engagement. Owing to the extensibility of hierarchical Bayesian framework of the topic model, our realization of dynamic representation learning requires less investment because the representation only relies on the order of the user’s historical following behaviors rather than external timing information (e.g., the timestamp of each behavior) utilized in some extant studies. 
- Third, we attempt to perform long-tail recommendation through the introduction of users’ contextual engagements. In followee recommendation, the “tail” items refer to less popular or niche followees (Kim et al. 2019). Inspired by Figure 1 showing that the popularity of followees gradually decreases when the user is continuously engaged in the current interest, we propose that contextual engagement is relevant to user preference for long-tail information.
