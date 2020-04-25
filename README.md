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

The Naive bayes classifier and the bidirectional LSTM have proved to be the most effective of the models used thus far. I had also tested GRUs and unidirectional LSTMs, but the bidirectional LSTM outperformed them both (although it outperformed the former by not much of a margin). The bidirectional LSTM consists of a singular bidirectional lstm layer with a 100 hidden units, an embedding size that is the size of the vocabulary, and an embedding dimension of 20, followed by multiple dense layers without dropouts to avoid the problem of overfitting, as the model tends to overfit on the training data very quickly, otherwise. Added regularization didn’t make much of a difference after adding the dropout layer, and so it was dropped from the model. Since the vocabulary size is large, it may not have enough data to work as effectively as we would hope for it to. For instance, a lot of the threads tagged as political tend to include proper nouns and other such words that imply that the post is related to politics, but it is likely that the embedding may not pick up on this. Pre-trained word embeddings did not prove to be very effective for similar reasons. In my opinion, the best way to go about this task would have been to include the body of the text as well, as it generally seems to contain more information that the model would be able to pick up on. However, for certain posts, especially ones tagged under AskIndia and such, the body is extremely large. An alternative in such cases would be to extract the relevant parts of this text, rather than processing it as a whole. 
