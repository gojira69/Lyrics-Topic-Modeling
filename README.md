# TOPIC MODELING OF LYRICS

Topic modeling is an unsupervised learning technique used to explore large text corpora. It is often confused with clustering, another unsupervised learning method. They both serve different purposes and operate under distinct assumptions.

| Feature                  | Clustering                                         | Topic Modelling                                                   |
| ------------------------ | -------------------------------------------------- | ----------------------------------------------------------------- |
| **Purpose**              | Groups texts by similarity                         | Discovers hidden semantic themes (topics) in text data            |
| **Basis of Grouping**    | Similarity (not necessarily semantic)              | Semantic similarity                                               |
| **Output**               | Discrete clusters of similar documents             | Topics as word distributions; documents as mixtures of topics     |
| **Document Association** | Each document belongs to one cluster only          | A document can belong to multiple topics with varying proportions |
| **Interpretability**     | Cluster labels often require manual interpretation | Topics are interpretable directly via top keywords                |

## DATASETS

2 primary datasets were used for this analysis:

- Genius Lyrics: A collection of nearly 5 million song lyrics scraped from Genius, including content as recent as 2022. Only a subset of songs (~ 30k) were used due to computational constraints.

- Wasabi Song Corpus: A curated dataset containing summaries of song lyrics for approximately 50,000 English-language songs.

## LATENT DIRICHLET ALLOCATION (LDA)

Latent Dirichlet Allocation was implemented on the Genius lyrics dataset to extract underlying themes from song lyrics. LDA operates on a bag-of-words approach, treating documents as random mixtures over latent topics, where each topic is characterized by a distribution over words. The model parameters (num topics, alpha, beta) were fine-tuned to optimize coherence scores.

### Optimal Number of Topics

LDA Parameter Tuning Figure 8 presents the coherence scores for different numbers of topics, both with and without profanity. The coherence analysis revealed that:

- With profanity: The optimal number of topics was 8, with a notable spike in coherence score around this value
- Without profanity: The optimal number was 3, with the highest coherence score at k=3

This significant difference in optimal topic count (8 vs. 3) demonstrates how profanity
substantially influences the thematic structure identified in lyrics.

<p float="left">
  <img src="figures/with_cuss_words/hyperparam_tuning/topic_coherence.png" alt="With Cuss Words" width="45%" />
  <img src="figures/without_cuss_words/hyperparam_tuning/topic_coherence.png" alt="Without Cuss Words" width="45%" />
</p>

### Effect of Profanity

A key aspect of this analysis was examining how profanity affects topic modeling results. Two parallel analyses were conducted:

- With profanity: Keeping all original lyrics intact
- Without profanity: Removing profane terms before topic modeling

### Thematic Structure With Profanity

With profanity included, the LDA model identified 8 dominant themes with artists as shown below.

<table>
  <tr>
    <td><img src="figures/with_cuss_words/artist_wordclouds/artist_wordcloud_topic_0.png" width="200"/></td>
    <td><img src="figures/with_cuss_words/artist_wordclouds/artist_wordcloud_topic_1.png" width="200"/></td>
    <td><img src="figures/with_cuss_words/artist_wordclouds/artist_wordcloud_topic_2.png" width="200"/></td>
    <td><img src="figures/with_cuss_words/artist_wordclouds/artist_wordcloud_topic_3.png" width="200"/></td>
  </tr>
  <tr>
    <td><img src="figures/with_cuss_words/artist_wordclouds/artist_wordcloud_topic_4.png" width="200"/></td>
    <td><img src="figures/with_cuss_words/artist_wordclouds/artist_wordcloud_topic_5.png" width="200"/></td>
    <td><img src="figures/with_cuss_words/artist_wordclouds/artist_wordcloud_topic_6.png" width="200"/></td>
    <td><img src="figures/with_cuss_words/artist_wordclouds/artist_wordcloud_topic_7.png" width="200"/></td>
  </tr>
</table>

The themes extracted include:

- Southern/Gangsta Rap: Dominated by artists like Lil Wayne, 2Pac, and Master P
- Mainstream/Pop Crossover: Characterized by Drake, Kanye West, and Nicki Minaj
- Conscious/Alternative: Artists include Atmosphere, Lauryn Hill, and Kid Cudi
- Party/Crunk: Associated with Lil Jon and Busta Rhymes
- French Rap: Featuring IAM, Orelsan, and others

The word clouds demonstrate how these themes manifest in vocabulary distributions, with significant overlap observed between artists across different themes.

### Thematic Structure Without Profanity

When profanity was removed, the LDA model identified 3 dominant themes, as shown below.

<p float="left">
  <img src="figures/without_cuss_words/artist_wordclouds/artist_wordcloud_topic_0.png" width="30%" />
  <img src="figures/without_cuss_words/artist_wordclouds/artist_wordcloud_topic_1.png" width="30%" />
  <img src="figures/without_cuss_words/artist_wordclouds/artist_wordcloud_topic_2.png" width="30%" />
</p>

The themes identified were:

- Conscious/Abstract Rap: Associated with Nas, Common, KRS-One, and De La Soul
- Gangsta/West Coast: Dominated by 2Pac, Dr. Dre, Ice Cube, and Snoop Dogg
- Experimental/Alternative: Including Kanye West, Erykah Badu, and Beastie Boys

Notably, censorship altered some artist groupings while preserving core genre distinctions. This suggests that while profanity contributes to thematic differentiation, fundamental stylistic differences remain detectable even after removing profane vocabulary.

The most significant finding is how profanity affects the optimal number of topics. With profanity included, the model identified 8 distinct themes; without it, only 3 remained prominent. This suggests that profane vocabulary contributes substantially to the linguistic differentiation between musical subgenres, particularly within hip-hop.

### GENRE ANALYSIS

The heat maps below illustrate the relationship between identified topics and music genres.

<p float="left">
  <img src="figures/with_cuss_words/genre/genre_topic_analysis.png" width="49%" />
  <img src="figures/without_cuss_words/genre/genre_topic_analysis.png" width="49%" />
</p>

Key observations:

- Without profanity (left): Strong correlations appear between specific genres and topics, with more distinct boundaries
- With profanity (right): A more complex distribution emerges, with topic 2 showing high correlation across multiple genres

This suggests that profanity serves as a cross-cutting linguistic feature that transcends traditional genre boundaries, while its removal allows more fundamental stylistic differences to become apparent.

Despite changes in topic structure, core genre distinctions remained recognizable after profanity removal. This indicates that fundamental stylistic differences transcend vocabulary choices, with distinct musical communities maintaining coherence even after significant vocabulary filtering.

### TEMPORAL EVOLUTION

Heatmaps below present the evolution of topic prevalence from 1970 to 2024.

<p float="left">
  <img src="figures/with_cuss_words/hyperparam_tuning/topic_evolution.png" width="49%" />
  <img src="figures/without_cuss_words/hyperparam_tuning/topic_evolution.png" width="49%" />
</p>

Key observations:

- Topic 0: Shows significant volatility with peaks in the early 1980s and 2010s, followed by a sharp decline
- Topic 1: Demonstrates a gradual increase from 1980 onward, with a dramatic surge in recent years
- Topic 2: Peaked in the early 1980s with declining prevalence toward the present

These temporal patterns reflect the evolution of musical trends and lyrical content over five decades, capturing the rise and fall of different stylistic approaches.

## BERTopic

BERTopic was implemented on the Wasabi lyrical summaries dataset to extract underlying themes from song lyrics. 

BERTopic offers several advantages over traditional LDA:

- Context-aware: Uses BERT embeddings to understand semantic meaning beyond word co-occurrence
- Auto-detection: Automatically determines optimal topic count through clustering
- Improved coherence: Produces more interpretable topics with clear semantic relationships

![alt text](figures/bertopic.png)

The word distributions reveal highly coherent topics:

- Topic 4: Alcohol-related vocabulary (drink, whiskey, wine)
- Topic 5: Fire imagery (fire, burn, flame)
- Topic 12: Loneliness themes (lonely, alone, lonesome)
- Topic 16: Financial vocabulary (money, cash, dime)
- Topic 1: Love and relationships
- Topic 2: Contains profanity
- Topic 7: Truth and deception themes (lie, truth, lies)

The artist distributions across topics show distinct musical communities:

- Topic 1: Soul and R&B artists (Michael Bolton, Mary J. Blige, Stevie Wonder)
- Topic 2: Hip-hop artists (DMX, Migos, Lil Wayne)
- Topic 7: Rock and alternative (A Perfect Circle, Billy Talent, Seether)
- Topic 8: Pop and contemporary R&B (Mary J. Blige, Kelly Clarkson, Paramore)
- Topic 3: Country and classic rock (Willie Nelson, Van Morrison, Roy Orbison)

### BERTopic vs. LDA

BERTopic demonstrated superior topic coherence compared to LDA, producing more interpretable themes with clearer semantic relationships. The context-aware embeddings cap
tured nuanced relationships between words and artists that would be missed by traditional bag-of-words approaches. BERTopic’s superior performance underscores the importance of context-aware approaches in understanding the semantic complexity of musical expression.

Topic modeling of song lyrics reveals how linguistic features, particularly profanity, shape the thematic landscape of popular music. The significant reduction in topic diversity when profanity is removed highlights its role in creating stylistic differentiation. However, the preservation of core genre distinctions suggests that fundamental musical communities remain detectable regardless of vocabulary filtering.
