# Reddit-Flair-Detector

Collection of data: Using praw and psaw (from the PushShift API), filtered by flair, and the length of the title of the post. 
All the notebooks were run on Google Colab
Extracted data from all posts from April 2019 onward, till around April 10th, 2020


| Method | Accuracy |
|--------|---------|
| Multinomial Naive Bayes | 65.075 % |
| Random Forest | 63.163 % |
| Linear SVM | 64.886 % |
| Logistic Regression | 53.189 % |
| Multilayer perceptron | 53.673 % |
| Bidirectional LSTM (not using pre-trained  word embeddings) | 65.41% |

The dataset consisted of around 16000 posts, with 9 flairs (Coronavirus, AskIndia, Non-Political, Sports, Food, Science/Technology, Business/Finance, Policy/Economy and Politics). The number of posts for each flair were limited so that the resulting dataset wouldn’t be too imbalanced. 
TF-IDF and CountVectorizer were used for feature extraction, and then tested to see which one worked better. 
Only the title was used as the feature as the data from the body could not be extracted (as for certain posts, it was too long and wasn’t feasible for the purpose of upload) and the url contains more or less the same text as the title does. The numeric data provided doesn’t give much conclusive evidence when classifying the post, which is why I avoided using it as a feature. 
The test set contains about 800 posts. 
Details about the classifiers are in the report file.

Libraries/frameworks made use of :
psaw
praw
nltk
csv
pandas
tensorflow
tf.keras
sklearn
numpy

