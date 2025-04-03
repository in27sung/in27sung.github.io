---
layout: post
title: Day 2 - Classifying embeddings with Keras and the Gemini API
subtitle: Embeddings & Vector Stores
author: Insung
categories: [5-Day Gen AI Intensive Course]
tags: [Data Science, Kaggle, Google]
top:
---

**Copyright 2025 Google LLC.**

```python
# @title Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
```

## Day 2 - Classifying embeddings with Keras and the Gemini API

### Overview

Welcome back to the Kaggle 5-day Generative AI course. In this notebook, you'll learn to use the embeddings produced by the Gemini API to train a model that can classify newsgroup posts into the categories (the newsgroup itself) from the post contents.

This technique uses the Gemini API's embeddings as input, avoiding the need to train on text input directly, and as a result it is able to perform quite well using relatively few examples compared to training a text model from scratch.

### For help

**Common issues are covered in the [FAQ and troubleshooting guide](https://www.kaggle.com/code/markishere/day-0-troubleshooting-and-faqs).**



```python
!pip uninstall -qqy jupyterlab kfp 2>/dev/null  # Remove unused conflicting packages
!pip install -U -q "google-genai==1.7.0"
```


```python
from google import genai
from google.genai import types

genai.__version__
```




    '1.7.0'



#### Set up your API key

To run the following cell, your API key must be stored it in a [Kaggle secret](https://www.kaggle.com/discussions/product-feedback/114053) named `GOOGLE_API_KEY`.

If you don't already have an API key, you can grab one from [AI Studio](https://aistudio.google.com/app/apikey). You can find [detailed instructions in the docs](https://ai.google.dev/gemini-api/docs/api-key).

To make the key available through Kaggle secrets, choose `Secrets` from the `Add-ons` menu and follow the instructions to add your key or enable it for this notebook.


```python
from kaggle_secrets import UserSecretsClient

GOOGLE_API_KEY = UserSecretsClient().get_secret("GOOGLE_API_KEY")

client = genai.Client(api_key=GOOGLE_API_KEY)
```

If you received an error response along the lines of `No user secrets exist for kernel id ...`, then you need to add your API key via `Add-ons`, `Secrets` **and** enable it.

![Screenshot of the checkbox to enable GOOGLE_API_KEY secret](https://storage.googleapis.com/kaggle-media/Images/5gdai_sc_3.png)

### Dataset

The [20 Newsgroups Text Dataset](https://scikit-learn.org/0.19/datasets/twenty_newsgroups.html) contains 18,000 newsgroups posts on 20 topics divided into training and test sets. The split between the training and test datasets are based on messages posted before and after a specific date. For this tutorial, you will use sampled subsets of the training and test sets, and perform some processing using Pandas.


```python
from sklearn.datasets import fetch_20newsgroups

newsgroups_train = fetch_20newsgroups(subset="train")
newsgroups_test = fetch_20newsgroups(subset="test")

# View list of class names for dataset
newsgroups_train.target_names
```




    ['alt.atheism',
     'comp.graphics',
     'comp.os.ms-windows.misc',
     'comp.sys.ibm.pc.hardware',
     'comp.sys.mac.hardware',
     'comp.windows.x',
     'misc.forsale',
     'rec.autos',
     'rec.motorcycles',
     'rec.sport.baseball',
     'rec.sport.hockey',
     'sci.crypt',
     'sci.electronics',
     'sci.med',
     'sci.space',
     'soc.religion.christian',
     'talk.politics.guns',
     'talk.politics.mideast',
     'talk.politics.misc',
     'talk.religion.misc']



Here is an example of what a record from the training set looks like.


```python
print(newsgroups_train.data[0])
```

    From: lerxst@wam.umd.edu (where's my thing)
    Subject: WHAT car is this!?
    Nntp-Posting-Host: rac3.wam.umd.edu
    Organization: University of Maryland, College Park
    Lines: 15
    
     I was wondering if anyone out there could enlighten me on this car I saw
    the other day. It was a 2-door sports car, looked to be from the late 60s/
    early 70s. It was called a Bricklin. The doors were really small. In addition,
    the front bumper was separate from the rest of the body. This is 
    all I know. If anyone can tellme a model name, engine specs, years
    of production, where this car is made, history, or whatever info you
    have on this funky looking car, please e-mail.
    
    Thanks,
    - IL
       ---- brought to you by your neighborhood Lerxst ----
    
    
    
    
    


Start by preprocessing the data for this tutorial in a Pandas dataframe. To remove any sensitive information like names and email addresses, you will take only the subject and body of each message. This is an optional step that transforms the input data into more generic text, rather than email posts, so that it will work in other contexts.


```python
import email
import re

import pandas as pd


def preprocess_newsgroup_row(data):
    # Extract only the subject and body
    msg = email.message_from_string(data)
    text = f"{msg['Subject']}\n\n{msg.get_payload()}"
    # Strip any remaining email addresses
    text = re.sub(r"[\w\.-]+@[\w\.-]+", "", text)
    # Truncate each entry to 5,000 characters
    text = text[:5000]

    return text


def preprocess_newsgroup_data(newsgroup_dataset):
    # Put data points into dataframe
    df = pd.DataFrame(
        {"Text": newsgroup_dataset.data, "Label": newsgroup_dataset.target}
    )
    # Clean up the text
    df["Text"] = df["Text"].apply(preprocess_newsgroup_row)
    # Match label to target name index
    df["Class Name"] = df["Label"].map(lambda l: newsgroup_dataset.target_names[l])

    return df
```


```python
# Apply preprocessing function to training and test datasets
df_train = preprocess_newsgroup_data(newsgroups_train)
df_test = preprocess_newsgroup_data(newsgroups_test)

df_train.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Text</th>
      <th>Label</th>
      <th>Class Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>WHAT car is this!?\n\n I was wondering if anyo...</td>
      <td>7</td>
      <td>rec.autos</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SI Clock Poll - Final Call\n\nA fair number of...</td>
      <td>4</td>
      <td>comp.sys.mac.hardware</td>
    </tr>
    <tr>
      <th>2</th>
      <td>PB questions...\n\nwell folks, my mac plus fin...</td>
      <td>4</td>
      <td>comp.sys.mac.hardware</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Re: Weitek P9000 ?\n\nRobert J.C. Kyanko () wr...</td>
      <td>1</td>
      <td>comp.graphics</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Re: Shuttle Launch Question\n\nFrom article &lt;&gt;...</td>
      <td>14</td>
      <td>sci.space</td>
    </tr>
  </tbody>
</table>
</div>



Next, you will sample some of the data by taking 100 data points in the training dataset, and dropping a few of the categories to run through this tutorial. Choose the science categories to compare.


```python
def sample_data(df, num_samples, classes_to_keep):
    # Sample rows, selecting num_samples of each Label.
    df = (
        df.groupby("Label")[df.columns]
        .apply(lambda x: x.sample(num_samples))
        .reset_index(drop=True)
    )

    df = df[df["Class Name"].str.contains(classes_to_keep)]

    # We have fewer categories now, so re-calibrate the label encoding.
    df["Class Name"] = df["Class Name"].astype("category")
    df["Encoded Label"] = df["Class Name"].cat.codes

    return df
```


```python
TRAIN_NUM_SAMPLES = 100
TEST_NUM_SAMPLES = 25
# Class name should contain 'sci' to keep science categories.
# Try different labels from the data - see newsgroups_train.target_names
CLASSES_TO_KEEP = "sci"

df_train = sample_data(df_train, TRAIN_NUM_SAMPLES, CLASSES_TO_KEEP)
df_test = sample_data(df_test, TEST_NUM_SAMPLES, CLASSES_TO_KEEP)
```


```python
df_train.value_counts("Class Name")
```




    Class Name
    sci.crypt          100
    sci.electronics    100
    sci.med            100
    sci.space          100
    Name: count, dtype: int64




```python
df_test.value_counts("Class Name")
```




    Class Name
    sci.crypt          25
    sci.electronics    25
    sci.med            25
    sci.space          25
    Name: count, dtype: int64



### Create the embeddings

In this section, you will generate embeddings for each piece of text using the Gemini API embeddings endpoint. To learn more about embeddings, visit the [embeddings guide](https://ai.google.dev/docs/embeddings_guide).

**NOTE**: Embeddings are computed one at a time, so large sample sizes can take a long time!

#### Task types

The `text-embedding-004` model supports a task type parameter that generates embeddings tailored for the specific task.

Task Type | Description
---       | ---
RETRIEVAL_QUERY	| Specifies the given text is a query in a search/retrieval setting.
RETRIEVAL_DOCUMENT | Specifies the given text is a document in a search/retrieval setting.
SEMANTIC_SIMILARITY	| Specifies the given text will be used for Semantic Textual Similarity (STS).
CLASSIFICATION	| Specifies that the embeddings will be used for classification.
CLUSTERING	| Specifies that the embeddings will be used for clustering.
FACT_VERIFICATION | Specifies that the given text will be used for fact verification.

For this example you will be performing classification.


```python
from google.api_core import retry
import tqdm
from tqdm.rich import tqdm as tqdmr
import warnings

# Add tqdm to Pandas...
tqdmr.pandas()

# ...But suppress the experimental warning.
warnings.filterwarnings("ignore", category=tqdm.TqdmExperimentalWarning)

# Define a helper to retry when per-minute quota is reached.
is_retriable = lambda e: (isinstance(e, genai.errors.APIError) and e.code in {429, 503})

@retry.Retry(predicate=is_retriable, timeout=300.0)
def embed_fn(text: str) -> list[float]:
    # You will be performing classification, so set task_type accordingly.
    response = client.models.embed_content(
        model="models/text-embedding-004",
        contents=text,
        config=types.EmbedContentConfig(
            task_type="classification",
        ),
    )

    return response.embeddings[0].values


def create_embeddings(df):
    df["Embeddings"] = df["Text"].progress_apply(embed_fn)
    return df
```

This code is optimised for clarity, and is not particularly fast. It is left as an exercise for the reader to implement [batch](https://ai.google.dev/api/embeddings#method:-models.batchembedcontents) or parallel/asynchronous embedding generation. Running this step will take some time.


```python
df_train = create_embeddings(df_train)
df_test = create_embeddings(df_test)
```


    Output()



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"></pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




    Output()



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"></pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




```python
df_train.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Text</th>
      <th>Label</th>
      <th>Class Name</th>
      <th>Encoded Label</th>
      <th>Embeddings</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1100</th>
      <td>Re: Once tapped, your code is no good any more...</td>
      <td>11</td>
      <td>sci.crypt</td>
      <td>0</td>
      <td>[0.0005698981, 0.010181307, -0.04996942, 0.025...</td>
    </tr>
    <tr>
      <th>1101</th>
      <td>Re: Would "clipper" make a good cover for othe...</td>
      <td>11</td>
      <td>sci.crypt</td>
      <td>0</td>
      <td>[-0.01079407, 0.034755286, -0.035821073, 0.036...</td>
    </tr>
    <tr>
      <th>1102</th>
      <td>How to detect use of an illegal cipher?\n\nHow...</td>
      <td>11</td>
      <td>sci.crypt</td>
      <td>0</td>
      <td>[-0.011569814, 0.01329988, -0.044520363, 0.009...</td>
    </tr>
    <tr>
      <th>1103</th>
      <td>Re: **Sorry folks** (read this)\n\nIn article ...</td>
      <td>11</td>
      <td>sci.crypt</td>
      <td>0</td>
      <td>[0.0038344853, 0.01732308, -0.02393305, 0.0058...</td>
    </tr>
    <tr>
      <th>1104</th>
      <td>Screw the people, crypto is for hard-core hack...</td>
      <td>11</td>
      <td>sci.crypt</td>
      <td>0</td>
      <td>[0.00011560278, 0.0058189007, -0.047523465, 0....</td>
    </tr>
  </tbody>
</table>
</div>



### Build a classification model

Here you will define a simple model that accepts the raw embedding data as input, has one hidden layer, and an output layer specifying the class probabilities. The prediction will correspond to the probability of a piece of text being a particular class of news.

When you run the model, Keras will take care of details like shuffling the data points, calculating metrics and other ML boilerplate.


```python
import keras
from keras import layers


def build_classification_model(input_size: int, num_classes: int) -> keras.Model:
    return keras.Sequential(
        [
            layers.Input([input_size], name="embedding_inputs"),
            layers.Dense(input_size, activation="relu", name="hidden"),
            layers.Dense(num_classes, activation="softmax", name="output_probs"),
        ]
    )
```


```python
# Derive the embedding size from observing the data. The embedding size can also be specified
# with the `output_dimensionality` parameter to `embed_content` if you need to reduce it.
embedding_size = len(df_train["Embeddings"].iloc[0])

classifier = build_classification_model(
    embedding_size, len(df_train["Class Name"].unique())
)
classifier.summary()

classifier.compile(
    loss=keras.losses.SparseCategoricalCrossentropy(),
    optimizer=keras.optimizers.Adam(learning_rate=0.001),
    metrics=["accuracy"],
)
```


<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">Model: "sequential"</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━┓
┃<span style="font-weight: bold"> Layer (type)                    </span>┃<span style="font-weight: bold"> Output Shape           </span>┃<span style="font-weight: bold">       Param # </span>┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━┩
│ hidden (<span style="color: #0087ff; text-decoration-color: #0087ff">Dense</span>)                  │ (<span style="color: #00d7ff; text-decoration-color: #00d7ff">None</span>, <span style="color: #00af00; text-decoration-color: #00af00">768</span>)            │       <span style="color: #00af00; text-decoration-color: #00af00">590,592</span> │
├─────────────────────────────────┼────────────────────────┼───────────────┤
│ output_probs (<span style="color: #0087ff; text-decoration-color: #0087ff">Dense</span>)            │ (<span style="color: #00d7ff; text-decoration-color: #00d7ff">None</span>, <span style="color: #00af00; text-decoration-color: #00af00">4</span>)              │         <span style="color: #00af00; text-decoration-color: #00af00">3,076</span> │
└─────────────────────────────────┴────────────────────────┴───────────────┘
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold"> Total params: </span><span style="color: #00af00; text-decoration-color: #00af00">593,668</span> (2.26 MB)
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold"> Trainable params: </span><span style="color: #00af00; text-decoration-color: #00af00">593,668</span> (2.26 MB)
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold"> Non-trainable params: </span><span style="color: #00af00; text-decoration-color: #00af00">0</span> (0.00 B)
</pre>



### Train the model

Finally, you can train your model. This code uses early stopping to exit the training loop once the loss value stabilises, so the number of epoch loops executed may differ from the specified value.


```python
import numpy as np


NUM_EPOCHS = 20
BATCH_SIZE = 32

# Split the x and y components of the train and validation subsets.
y_train = df_train["Encoded Label"]
x_train = np.stack(df_train["Embeddings"])
y_val = df_test["Encoded Label"]
x_val = np.stack(df_test["Embeddings"])

# Specify that it's OK to stop early if accuracy stabilises.
early_stop = keras.callbacks.EarlyStopping(monitor="accuracy", patience=3)

# Train the model for the desired number of epochs.
history = classifier.fit(
    x=x_train,
    y=y_train,
    validation_data=(x_val, y_val),
    callbacks=[early_stop],
    batch_size=BATCH_SIZE,
    epochs=NUM_EPOCHS,
)
```

    Epoch 1/20
    [1m13/13[0m [32m━━━━━━━━━━━━━━━━━━━━[0m[37m[0m [1m1s[0m 29ms/step - accuracy: 0.3495 - loss: 1.3524 - val_accuracy: 0.6700 - val_loss: 1.2493
    Epoch 2/20
    [1m13/13[0m [32m━━━━━━━━━━━━━━━━━━━━[0m[37m[0m [1m0s[0m 12ms/step - accuracy: 0.7654 - loss: 1.1780 - val_accuracy: 0.6100 - val_loss: 1.1083
    Epoch 3/20
    [1m13/13[0m [32m━━━━━━━━━━━━━━━━━━━━[0m[37m[0m [1m0s[0m 11ms/step - accuracy: 0.8163 - loss: 0.9905 - val_accuracy: 0.8500 - val_loss: 0.9304
    Epoch 4/20
    [1m13/13[0m [32m━━━━━━━━━━━━━━━━━━━━[0m[37m[0m [1m0s[0m 10ms/step - accuracy: 0.9070 - loss: 0.7886 - val_accuracy: 0.8600 - val_loss: 0.7715
    Epoch 5/20
    [1m13/13[0m [32m━━━━━━━━━━━━━━━━━━━━[0m[37m[0m [1m0s[0m 9ms/step - accuracy: 0.9173 - loss: 0.6178 - val_accuracy: 0.8900 - val_loss: 0.6403
    Epoch 6/20
    [1m13/13[0m [32m━━━━━━━━━━━━━━━━━━━━[0m[37m[0m [1m0s[0m 10ms/step - accuracy: 0.9465 - loss: 0.4585 - val_accuracy: 0.9100 - val_loss: 0.5370
    Epoch 7/20
    [1m13/13[0m [32m━━━━━━━━━━━━━━━━━━━━[0m[37m[0m [1m0s[0m 10ms/step - accuracy: 0.9502 - loss: 0.3637 - val_accuracy: 0.9000 - val_loss: 0.4701
    Epoch 8/20
    [1m13/13[0m [32m━━━━━━━━━━━━━━━━━━━━[0m[37m[0m [1m0s[0m 9ms/step - accuracy: 0.9743 - loss: 0.2954 - val_accuracy: 0.9000 - val_loss: 0.4054
    Epoch 9/20
    [1m13/13[0m [32m━━━━━━━━━━━━━━━━━━━━[0m[37m[0m [1m0s[0m 10ms/step - accuracy: 0.9715 - loss: 0.2301 - val_accuracy: 0.9300 - val_loss: 0.3745
    Epoch 10/20
    [1m13/13[0m [32m━━━━━━━━━━━━━━━━━━━━[0m[37m[0m [1m0s[0m 10ms/step - accuracy: 0.9839 - loss: 0.1878 - val_accuracy: 0.9100 - val_loss: 0.3758
    Epoch 11/20
    [1m13/13[0m [32m━━━━━━━━━━━━━━━━━━━━[0m[37m[0m [1m0s[0m 9ms/step - accuracy: 0.9870 - loss: 0.1535 - val_accuracy: 0.9200 - val_loss: 0.3222
    Epoch 12/20
    [1m13/13[0m [32m━━━━━━━━━━━━━━━━━━━━[0m[37m[0m [1m0s[0m 9ms/step - accuracy: 0.9883 - loss: 0.1395 - val_accuracy: 0.9500 - val_loss: 0.3050
    Epoch 13/20
    [1m13/13[0m [32m━━━━━━━━━━━━━━━━━━━━[0m[37m[0m [1m0s[0m 9ms/step - accuracy: 0.9953 - loss: 0.1124 - val_accuracy: 0.9200 - val_loss: 0.2965
    Epoch 14/20
    [1m13/13[0m [32m━━━━━━━━━━━━━━━━━━━━[0m[37m[0m [1m0s[0m 10ms/step - accuracy: 1.0000 - loss: 0.0983 - val_accuracy: 0.9400 - val_loss: 0.2741
    Epoch 15/20
    [1m13/13[0m [32m━━━━━━━━━━━━━━━━━━━━[0m[37m[0m [1m0s[0m 9ms/step - accuracy: 0.9953 - loss: 0.0964 - val_accuracy: 0.9100 - val_loss: 0.2761
    Epoch 16/20
    [1m13/13[0m [32m━━━━━━━━━━━━━━━━━━━━[0m[37m[0m [1m0s[0m 10ms/step - accuracy: 0.9949 - loss: 0.0738 - val_accuracy: 0.9300 - val_loss: 0.2857
    Epoch 17/20
    [1m13/13[0m [32m━━━━━━━━━━━━━━━━━━━━[0m[37m[0m [1m0s[0m 9ms/step - accuracy: 0.9996 - loss: 0.0619 - val_accuracy: 0.9500 - val_loss: 0.2469


### Evaluate model performance

Use Keras <a href="https://www.tensorflow.org/api_docs/python/tf/keras/Model#evaluate"><code>Model.evaluate</code></a> to calculate the loss and accuracy on the test dataset.


```python
classifier.evaluate(x=x_val, y=y_val, return_dict=True)
```

    [1m4/4[0m [32m━━━━━━━━━━━━━━━━━━━━[0m[37m[0m [1m0s[0m 3ms/step - accuracy: 0.9446 - loss: 0.2381 





    {'accuracy': 0.949999988079071, 'loss': 0.24694035947322845}



To learn more about training models with Keras, including how to visualise the model training metrics, read [Training & evaluation with built-in methods](https://www.tensorflow.org/guide/keras/training_with_built_in_methods).

### Try a custom prediction

Now that you have a trained model with good evaluation metrics, you can try to make a prediction with new, hand-written data. Use the provided example or try your own data to see how the model performs.


```python
def make_prediction(text: str) -> list[float]:
    """Infer categories from the provided text."""
    # Remember that the model takes embeddings as input, so calculate them first.
    embedded = embed_fn(new_text)

    # And recall that the input must be batched, so here they are wrapped as a
    # list to provide a batch of 1.
    inp = np.array([embedded])

    # And un-batched here.
    [result] = classifier.predict(inp)
    return result
```


```python
# This example avoids any space-specific terminology to see if the model avoids
# biases towards specific jargon.
new_text = """
First-timer looking to get out of here.

Hi, I'm writing about my interest in travelling to the outer limits!

What kind of craft can I buy? What is easiest to access from this 3rd rock?

Let me know how to do that please.
"""

result = make_prediction(new_text)

for idx, category in enumerate(df_test["Class Name"].cat.categories):
    print(f"{category}: {result[idx] * 100:0.2f}%")
```

    [1m1/1[0m [32m━━━━━━━━━━━━━━━━━━━━[0m[37m[0m [1m0s[0m 51ms/step
    sci.crypt: 0.07%
    sci.electronics: 0.33%
    sci.med: 0.06%
    sci.space: 99.54%


### Further reading

To explore training custom models with Keras further, check out the [Keras guides](https://keras.io/guides/).

*- [Mark McD](https://linktr.ee/markmcd)*
