<div align="center">
<h1>Customer Complaint Analysis with Topic Modeling</h1>
</div>

<p align="center">
<img src="images\cover.png" class="center" width="60%"/>
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

Finally, two distinct topic modeling techniques were applied. The first model applied was LDA, using the Gensim module, and for visualization, the pyLDAvis package. As a second analytical methodology, the pre-trained model in Portuguese `rufimelo/bert-large-portuguese-cased-sts` was used to tokenize the text, and BERTopic for visualization. While in the first technique, we used the text with all preprocessing techniques, in the second, we used only the normalized text with stop-word removal.

The results can be seen below or, if you prefer, in the notebook `02. topic_modeling_customer_claim.ipynb`.

## Results and Conclusions
Classify and assign topics in a complaints dataset is quite challenging, as users can assign more than one subject in a single complaint, such as unauthorized charges and service interruption. Both techniques were able to assign more than one topic to the same complaint. Below, some insights.

### LDA
One issue with using LDA is that we need to specify in advance the number of topics that the algorithm needs to consider, making it a somewhat trial-and-error activity. Since the reclameaqui website has labels assigned by users themselves, we was able to use this information as a parameter in the model. The `pyLDAvis` module provides an interesting dashboard with grouped topics, along with the most relevant terms. This helped us to understand the nature of the complaint dataset, as in the case below where the topic 10 has the most relevant term as 'recarga' (recharge). By examining the other topics, we can see that LDA did a good job in separating the groups.

<p align="center">
  <img src="images\pyLDAvis.png" class="center" width="70%"/>
  <br><em>Figure 1 - pyLDAvis dashboard</em>
</p>

### BERTopic
While LDA works with term frequency, ignoring the semantic similarity between words, BERTopic operates with word embeddings, assigning similar vectors to words with the same semantic value. Semantic value can be highly valuable in this case, as it involves text collected from the internet with completely free-form writing.

Another advantage of BERTopic is that we can suggest the number of topics or let the model determine the value of this parameter. Additionally, the module offers more visualization options, which greatly enriches the analysis.

<p align="center">
  <img src="images\BERTopic_distance_map.png" class="center" width="90%"/>
  <br><em>Figure 2 - BERTopic Intertopic Distance Map and Topic Wors Scores</em>
</p>

Comparing labels with the topics assigned by BERTopic, we can see that the data presented by the model is quite consistent. Examples: Group 1, with the highest-scoring words 'recarga' and 'credito' (recharge and credit), has the most labels related to 'problema com recarga' (recharge issue), 'corte indevido de linha' (unauthorized line disconnection), and 'consumo de crédito' (credit consumption), which are closely related issues. We can say the same in relation to topic 5 with the words 'internet' and 'sinal' (signal) as the highest scoring - ignoring the word 'claro', which is the name of the operator - with the labels 'qualidade de internet' (internet quality) and 'instabilidade de sinal' (signal instability).

<p align="center">
  <img src="images\BERTopic_topic_per_class.png" class="center" width="90%"/>
  <br><em>Figure 3 - BERTopic Topics Per Class</em>
</p>

Another interesting option provided by the module is document-level analysis, where we can plot each of them and assess the interrelation between topics:

<p align="center">
  <img src="images\BERTopic_map.png" class="center" width="90%"/>
  <br><em>Figure 4 - BERTopic Map fo documents</em>
</p>

In summary, we can say that both methodologies are good text analysis tools. However, despite LDA being a more established methodology, we believe that BERTopic is a better option. This is because it is a transformer-based neural network model capable of capturing the semantic value between words, resulting in more consistent groups and offering various built-in perspectives for analysis without the need for additional code.

## References
* [1] https://blog.reclameaqui.com.br/reclame-aqui-bate-recorde-de-reclamacoes-em-dezembro-de-2021/
