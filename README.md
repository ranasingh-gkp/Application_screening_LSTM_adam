# Application_screening_LSTM_adam
Task is to predict whether teachers' project proposals are accepted or rejected. 

2. Split the data into train, cv, and test
3. After step 2 you have to train 3 types of models as discussed below. 
4. For all the model use 'auc' as a metric. check this for using auc as a metric. you need to print the AUC value for each epoch. Note: you should NOT use the tf.metric.auc
5. You are free to choose any number of layers/hiddden units but you have to use same type of architectures shown below. 
6. You can use any one of the optimizers and choice of Learning rate and momentum, resources: cs231n class notes, cs231n class video. 
7. You should Save the best model weights.
8. For all the model's use TensorBoard and plot the Metric value and Loss with epoch. While submitting, take a screenshot of plots and include those images in .ipynb notebook and PDF. 
9. Use Categorical Cross Entropy as Loss to minimize.
10. try to get AUC more than 0.8 for atleast one model



ref: https://i.imgur.com/w395Yk9.png
Input_seq_total_text_data --- You have to give Total text data columns. After this use the Embedding layer to get word vectors. Use given predefined glove word vectors, don't train any word vectors. After this use LSTM and get the LSTM output and Flatten that output.
Input_school_state --- Give 'school_state' column as input to embedding layer and Train the Keras Embedding layer.
Project_grade_category --- Give 'project_grade_category' column as input to embedding layer and Train the Keras Embedding layer.
Input_clean_categories --- Give 'input_clean_categories' column as input to embedding layer and Train the Keras Embedding layer.
Input_clean_subcategories --- Give 'input_clean_subcategories' column as input to embedding layer and Train the Keras Embedding layer.
Input_clean_subcategories --- Give 'input_teacher_prefix' column as input to embedding layer and Train the Keras Embedding layer.
Input_remaining_teacher_number_of_previously_posted_projects._resource_summary_contains_numerical_digits._price._quantity ---concatenate remaining columns and add a Dense layer after that.
For LSTM, you can choose your sequence padding methods on your own or you can train your LSTM without padding, there is no restriction on that.
Below is an example of embedding layer for a categorical columns. In below code all are dummy values, we gave only for referance.


1. Go through this blog, if you have any doubt on using predefined Embedding values in Embedding layer - https://machinelearningmastery.com/use-word-embedding-layers-deep-learning-keras/
2. Please go through this link https://keras.io/getting-started/functional-api-guide/ and check the 'Multi-input and multi-output models' then you will get to know how to give multiple inputs.


# https://stats.stackexchange.com/questions/270546/how-does-keras-embedding-layer-work
input_layer = Input(shape=(n,))
embedding = Embedding(no_1, no_2, input_length=n)(input_layer)
flatten = Flatten()(embedding)




====================================================

#Model 2

Use the same model as above but for 'input_seq_total_text_data' give only some words in the sentance not all the words. Filter the words as below.

1. Train the TF-IDF on the Train data feature 'essay' 

2. Get the idf value for each word we have in the train data. 

3. Remove the low idf value and high idf value words from our data. Do some analysis on the Idf values and based on those values choose the low and high threshold value. Because very frequent words and very very rare words don't give much information. (you can plot a box plots and take only the idf scores within IQR range and corresponding words)

4. Train the LSTM after removing the Low and High idf value words. (In model-1 Train on total data but in Model-2 train on data after removing some words based on IDF values)










Model 3

input_seq_total_text_data:
  . Use text column('essay'), and use the Embedding layer to get word vectors. 

  . Use given predefined glove word vectors, don't train any word vectors. 

  . Use LSTM that is given above, get the LSTM output and Flatten that output. 

  . You are free to preprocess the input text as you needed. 

Other_than_text_data:
  . Convert all your Categorical values to onehot coded and then concatenate all these onehot vectors 

  . Neumerical values and use CNN1D as shown in above figure. 

  . You are free to choose all CNN parameters like kernel sizes, stride.
