# The problem
People do not tweet about the same things all the time. Transformer models, however, are mostly applied to single-topic documents. Can we correctly infer a user's ideology from small, thematically diverse tweets using transformers and clustering? Can preprocessing tweets based on their similarity to each other help?

# The contributions 
Yes, we can. However, all tested combinations of methods hit an accuracy ceiling of 62-64%. 
Embedding with Sentence-BERT and filtering tweets based on cosine similarity can improve information capture by 20%. 
Transfomer-powered clustering (BERTopic) is no better than legacy clustering for this problem. 

# Structure

## Folder 'Data'
Contains 3 datasets: 
- ExtractedTweets, housing data downloaded from the Kaggle source ([43] in the thesis). 
- Dataset_versions, housing abridged versions of the original dataset generated through CSF. 
- Dataset_random_selection, housing a single abridged version of the dataset generated through random sampling.

## Folder 'CSF' 
Reducing volume of data to <= 256 tokens (embedding model ’all-MiniLM-L6-v2’). 

- "CSF" "Contextual Similarity Filtering". Processes the input dataset "ExtractedTweets" into "Dataset_versions" by filtering out least similar tweets. Contains a csv with different volumes of data corresponding to different filtering thresholds.

- "Random_selection" generates a random sample from "ExtractedTweets"  Serves as a baseline to check for effectiveness of CSF. Generates a csv file "Dataset_random_selection". 

## Folder 'Clustering' 
Clustering-related analysis (both embeddings- and BERTopic-based). Makes use of the DBCV file, credited to [30]. Makes use of two datasets: "Dataset_random_selection" and "Dataset_versions".  


## Folder 'Final_results' 
Visualisations from the Clustering folder, including those not used in the thesis. 
4 subfolders: 
- "random_BERTopic" - plots with BERTopic results on "Random_selection" 
- "random_embedding_clusters" - plots with embedding-based results on "Random_selection"
- "selected_BERTopic - plots with BERTopic results on CSF data (threshold_0.7 from "Dataset_versions")
- "selected_embedding_clusters" - plots with embedding-based results on CSF data (threshold_0.7 from "Dataset_versions"). 


#### References

[30] D. Moulavi, P. A. Jaskowiak, R. J. Campello, A. Zimek, and J. Sander, “Density-based clustering validation,” Proceedings of the 2014 SIAM International Conference on Data Mining, 2014. doi:10.1137/1.9781611973440.96 

[43] K. Pastor, 'Democrat Vs. Republican Tweets', Kaggle, 2018. [Online]. Available: https://www.kaggle.com/datasets/kapastor/democratvsrepublicantweets/data






