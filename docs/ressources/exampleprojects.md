# Example Projects
ActiveTigger has been applied to a variety of research projects in the social sciences. Below are a few of them:

## Estimating the extent of online hostility in politics

*Annina Claesson*
Article (in French): [Le prix de la visibilité
Une analyse computationnelle des interactions en ligne avec des député·es français·es (Revue française de science politique)](https://shs-cairn-info.scpo.idm.oclc.org/revue-revue-francaise-de-science-politique-2025-3-page-549?lang=fr)

This project sought to quantify various types of Twitter reactions targeting French MPs, distinguishing between political criticism, abuse, and expressions of support. With access to the total number of tweets mentioning French MPs in 2022-2023 (a dataset of over 30 million tweets), manual annotation of more than a small sample would have been impossible. At the same time, the criteria for each category were not straightforward to automate, requiring a human understanding of nuance, sarcasm, and subtility. While applying ready-made models for detecting negative sentiment or hate speech would have been possible, these were not well adapted to the specific context of the French political Twittersphere.  

**Solution**: fine-tuning three separate bespoke BERT classifier models using ActiveTigger.
The objective was to develop classifier models that could correctly identify diverse and creatively formulated types of tweets that could be classified into each category (criticism, abuse, support). This required a 

**Workflow**: 
- An iterative annotation process to improve coding scheme and understand dataset, regular consultation with colleagues.
- Active learning to facilitate annotation of rare categories.
- Final training/test dataset comprised of around 1000 tweets per category.
- Binary classifiers (criticism/not criticism, abuse/not abuse, support/not support) applied sequentially on full dataset (filtered down to 4,5 million tweets).

**F1 Scores**:
- Abuse: 0.77
- Criticism: 0.81
- Support: 0.74

**Lessons learned**
Distinguishing between these three categories of tweets was a complex task for both humans and machines alike - many subtilities made it difficult to draw clear lines between tweets that "crossed the line" into abuse. Spending a significant amount of time in the annotation phase to create a functional but flexible coding scheme helped to clarify the object of study for both the human researcher and for the models. Creating three binary models and running each one separately made it possible to look at cases that overlapped several categories at the analysis stage.

That said, many unexpected challenges arose in translating human logic to a model. For example, the "support" classifier was surprisingly the most challenging to develop due to the heavy presence of sarcasm in the corpus (contrast "bravo!" vs "bravo..."). Using active learning and regex functions to target these ambiguous cases (for example, by targeting tweets that contained different emojis that changed the semantic meaning of the tweet) was helpful in improving the model's understanding of what made a tweet sarcastic.

The F1 scores can be considered good but not perfect. This was largely due to the complexity of each category, which were intended to span many different kinds of expressions under the same umbrella (for example, the abuse category covered everything from subtle insults to overt hate speech). More targeted models focusing on more narrow forms of expression in tweets would likely have made for better-performing models.

Nevertheless, ActiveTigger made it possible to quantify different types of reactions targeting politicians, which had never been done for the French context. The final paper explores differences between political groups and sociodemographic characteristics in terms of which MPs become targets for which types of tweets, notably from a gender perspective.

---

## Building a corpus of environmental journalism
**Jules Brion**

This project sought to build a large-scale corpus of newspaper articles related to the environment and climate policies. With articles extracted from Europresse using keywords such as "climate" or "environment" (terms that by definition often carried multiple semantic meanings) manual sorting would have significantly limited the corpus size. ActiveTigger made it possible to skip the initial manual filtering and classify at scale.

**Solution**: Fine-tuning a bespoke BERT binary classifier model using ActiveTigger.
The objective was to develop a classifier capable of identifying environment-related journalism segments, distinguishing relevant articles from unrelated ones despite the broad and ambiguous nature of environmental vocabulary.

**Workflow**:
- Segmentation of articles into chunks of 300–700 characters (prioritising sentence boundaries), keeping texts under 500 characters intact.
- An iterative annotation process to stabilise the coding scheme and corpus structure.
- Active learning to surface ambiguous cases, visualisation tools used to identify and resolve annotation inconsistencies.
- A supplementary homogeneous training corpus created to compensate for imbalances across newspapers and time periods.
- A binary classifier (environment/not environment) applied on the full corpus.

**F1 Score**:
- Environment: > 0.95

**Lessons learned**:
The multiple meanings of environmental keywords made it impossible to rely on keyword-based filtering alone. Careful attention to corpus structure (particularly paragraph length and source diversity) was essential to model performance. Training the model on a homogeneous corpus before applying it to a more diverse one helped avoid biases introduced by uneven source representation.

A key challenge was understanding how BERT-based models learn. Early training runs suffered from overfitting due to insufficient familiarity with the model's parameters. Taking the time to understand technical distinctions (such as evaluation loss vs. validation loss) proved essential to improving results.

Once the annotations had been extended to the entire corpus, the article paragraphs were grouped together. A score was calculated, relating the number of environment-related paragraphs to the total number of paragraphs for each article. We decided not to keep articles with three paragraphs and only one related to the environment (the score of 0.33 is high, but adding them ran the risk of false positives because it was only based on one classification).


