### Word Prediction with SwiftKey

**Author**
Ryan Summe

#### Executive summary
Typing on small UI keyboards is a nasty experience for all of us. I have been an iPhone user for over a decade and I feel like the typing experience has never improved. I have tried swiping keyboards, "gBoard" from Google, and even handwriting applications. The ability for our phones to predict what we want to type is a very challenging task and one that still has a lot to achieve.

SwiftKey is a company that built a software keyboard with autocomplete. They launched in early 2010s, and in 2016 rebuilt their predictions [using a recurrent neural network](https://www.forbes.com/sites/kevinmurnane/2016/09/26/why-swiftkeys-new-keyboard-with-an-artificial-neural-network-is-better-than-the-old-version/). This improved the predictions drastically, but in my opinion today in 2024, these keyboards are all still very poor at predicting our language.

I downloaded a [public data set](https://www.kaggle.com/datasets/crmercado/tweets-blogs-news-swiftkey-dataset-4million/data) of tweets from SwiftKey and built a recurrent neural network to attempt what they did in 2016.

I used only a small portion of the tweets given the computational load and time to train, but was able to achieve X% accuracy with Y loss after 20 epochs of training.

There is more work to be done with smart keyboards, unless this approach is abandoned entirely for something based on neural uplink (see Elon's Nueralink company) or visual signal. I have high hopes to reduce the strain on my thumbs in the future!

#### Rationale
Developing better models to improve typing on phone keyboards will have a major impact on users. People will be able to communicate more naturally, be more comfortable, and be less frustrated while using a phone. I believe it is one of the major features of phones that has not improved significantly since their release.

Getting this right will mean big bucks, Swiftkey was acquired by Microsoft for $250m.

#### Research Question
Can we use a recurrent neural network to accurately guess the next word a user wants to type? This is a multiclass classification challenge.

#### Data Sources
Swiftkey has published massive datasets of tweets on Kaggle [link](https://www.kaggle.com/datasets/crmercado/tweets-blogs-news-swiftkey-dataset-4million/data).

#### Methodology
I will read in english tweets, preprocess text with trimming, removing non-alphanumeric characters, and create an n-gram model of the text. This means I will use a sliding window across each tweet to generate features from the first word, the first 2 words, the first 3 words, etc. The following word after each of these arrays will be the target prediction class.

I don't think stemming or lemmatization is appropriate given we want the model to process the actual words written by the user, and predict actual words that are likely to come next. Stemming or lemmatizing would make this a very blunt tool for accurate predictions.

The model is trained on 20 epochs, with each taking about 7 minutes. Total training time took 140 minutes or over 2 hours.

#### Results
After 20 training epochs taking over 2 hours, the greatest accuracy achieved is 36% with a loss of 2.98 (categorical crossentropy). This is not a great result but I can see how this approach (RNNs) can be used to build more accurate models.

I test the prediction model at the end with a seed word of 'winner'. The result is 'winner will backup'! Not sure if that is helpful but it is at least a reasonable attempt.

#### Next steps
To further develop this model, we could do a number of things:
- Increase the training text. I chose the first 5,000 tweets due to how long it takes to build the training set and train the model.
- Use cross validation with different hyperparameters. Due to the computational cost of training (over 2 hours), I did not attempt a gridsearch.
- Increase training epochs. Even though the improvements slowed down after 9, there could be additional improvements with more training epochs.
- Try more or different layers.
- Try different optimization algorithms. I used `Adam`.

#### Outline of project

- [Link to notebook 1]()
