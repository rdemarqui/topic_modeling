<div align="center">
<h1>Customer Complaint Analysis with Topic Modeling</h1>
</div>

<p align="center">
<img src="images\cover.png" class="center" width="45%"/>
</p>

## Overview
Analyzing large datasets of customer complaint texts is a challenging and essential task for companies looking to improve the quality of their products and services. As the internet becomes an increasingly influential space for customer interactions, organizations accumulate massive volumes of feedback, reviews, and complaints from consumers, making the extraction of meaningful insights from this data a complex endeavor. The diversity of words, topics, and sentiments expressed in such texts can overwhelm analysts. This is where topic modeling emerges as a valuable tool. This text analysis approach allows for the automatic extraction of underlying topics from vast amounts of unstructured text, simplifying the identification of issues and trends, providing a clearer view of customer needs, and assisting companies in making informed decisions to enhance their products and services. 

In this context, this work will explore how topic modeling can be an effective solution for analyzing large customer complaint datasets, highlighting its applications and benefits. We will extract and analyse customer complaint data from a telecommunications provider by scraping data from the website [reclamequi.com.br](https://www.reclameaqui.com.br/).

## Objectives
Develop webscraping script, analyze user complaints, aggregate them into topics, and extract important insights through two distinct methodologies of topic modeling, namely Latent Dirichlet Allocation (LDA) and transformer networks BERTopic.

## Tecnologies Used
* `selenium 4.14.0`
* `BeautifulSoup 4.11.2`
* `pandas 1.5.3`
* `nltk 3.8.1`
* `spacy 3.6.1`
* `pyLDAvis 2.1.2`
* `bertopic 0.15.0`

## About the Data
The data was collected from the website [reclameaqui.com](www.reclameaqui.com.br), which is a Brazilian website with over 30 million registered consumers and 500,000 registered companies on the platform, where 1.5 billion pageviews occur annually [1]. A total of 7,000 distinct complaints from a telecommunications provider were collected. This complaints was classified by the users into 14 unique categories, therefore, we have a balanced dataset with 500 complaints per category.

## Methodology
First, a script was created to scrape company data, and for this task, Python packages Selenium and BeautifulSoup were used. The script is available in the repository with the name `01. webscrapping_reclameaqui.ipynb`

After obtaining the data, we performed text cleaning, using normalization techniques (punctuation, lowercase, accents, special characters), removal of stop words, lemmatization, and the removal of words with low TF-IDF scores. Removing low TF-IDF words is essential in topic modeling because these words probably provide little discriminatory power and can dominate topics. By excluding them, the model focuses on more meaningful and distinctive terms, improving topic quality and helping to identify relevant keywords that truly characterize the underlying topics in a corpus.

Finally, two distinct topic modeling techniques were applied. The first model applied was LDA, using the Gensim module, and for visualization, the pyLDAvis package. As a second analytical methodology, the pre-trained model in Portuguese rufimelo/bert-large-portuguese-cased-sts was used to tokenize the text, and BERTopic for visualization. While in the first technique, we used the text with all preprocessing techniques, in the second, we used only the normalized text with stop-word removal.

The results can be seen below or, if you prefer, in the notebook `02. topic_modeling_customer_claim.ipynb`.

## Results and Conclusions
To do

## References
* [1] https://blog.reclameaqui.com.br/reclame-aqui-bate-recorde-de-reclamacoes-em-dezembro-de-2021/
* https://k3ybladewielder.medium.com/topic-modelling-682f74fc5e63
* https://medium.com/@romanegger1/list/b66c8d01f326
* https://medium.com/@power.up1163/visualizing-topic-models-with-topicwizard-ee5b4428405e
* https://towardsdatascience.com/topic-modeling-with-lsa-plsa-lda-nmf-bertopic-top2vec-a-comparison-5e6ce4b1e4a5
