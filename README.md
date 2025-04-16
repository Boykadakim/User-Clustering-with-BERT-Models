# The problem
People do not tweet about the same things all the time. Transformer models, however, are mostly applied to single-topic documents. Can we correctly infer a user's ideology from small, thematically diverse tweets using transformers and clustering? Can preprocessing tweets based on their similarity help achieve that? 

# The contributions 
Yes, we can. However, all tested combinations of methods hit an accuracy ceiling of 62-64%.  
Embedding with Sentence-BERT and filtering tweets based on cosine similarity can improve information capture by 20%. 
Transfomer-powered clustering (BERTopic) is no better than legacy clustering for this problem; even worse, BERTopic's own clustering algorithm may fail to capture data relationships right. 

# Structure

## Data
3 datasets in .zip "Data": 
- ExtractedTweets, housing data downloaded from the Kaggle source ([43] in the thesis). 
- Dataset_versions, housing abridged versions of the original dataset generated through CSF.
<img width="1086" alt="Data" src="https://github.com/user-attachments/assets/568dd0ac-2ad4-4553-8ba9-4e41130e0ee6" />
- Dataset_random_selection, housing a single abridged version of the dataset generated through random sampling.

## Tweet processing
Reducing volume of data to <= 256 tokens (embedding model ’all-MiniLM-L6-v2’). 

- "CSF" "Contextual Similarity Filtering". Processes the input dataset "ExtractedTweets" into "Dataset_versions" by filtering out least similar tweets. Contains a csv with different volumes of data corresponding to different filtering thresholds.

- "Random_selection" generates a random sample from "ExtractedTweets"  Serves as a baseline to check for effectiveness of CSF. Generates a csv file "Dataset_random_selection". 

## Clustering 
Clustering-related analysis (both embeddings- and BERTopic-based) is gathered in "Clustering". Makes use of the DBCV file, credited to [30]. Makes use of two datasets: "Dataset_random_selection" and "Dataset_versions".  


## Results 
<img width="536" alt="Results table" src="https://github.com/user-attachments/assets/b771d767-706d-4664-88a6-2706bf534a44" />

### Legacy clustering on SBERT embeddings: 

Cluster accuracy for unprocessed data
![random_agglo_clusters](https://github.com/user-attachments/assets/059a0c89-db4b-46a6-979a-0348847fc05a)

VS   

Cluster accuracy for CSF-processed data (threshold_0.7 from "Dataset_versions"). 
![selected_agglo_clusters](https://github.com/user-attachments/assets/bca2dd80-2d9b-49e1-a8dd-ba9cad348f22)

### Clustering with BERTopic:  

Cluster accuracy for unprocessed data 
![random_single_BERTopic_NN_clusters](https://github.com/user-attachments/assets/96ea580a-7bda-42df-b600-565ffa37e162)

Cluster accuracy for CSF-processed data (threshold_0.7 from "Dataset_versions"). 
![select_single_BERTopic_NN_clusters](https://github.com/user-attachments/assets/983166c2-07a9-4967-9854-dc4b3495c565)





#### References

[30] D. Moulavi, P. A. Jaskowiak, R. J. Campello, A. Zimek, and J. Sander, “Density-based clustering validation,” Proceedings of the 2014 SIAM International Conference on Data Mining, 2014. doi:10.1137/1.9781611973440.96 

[43] K. Pastor, 'Democrat Vs. Republican Tweets', Kaggle, 2018. [Online]. Available: https://www.kaggle.com/datasets/kapastor/democratvsrepublicantweets/data






