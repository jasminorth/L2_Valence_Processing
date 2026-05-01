# Dataset Creation
The dataset contains *words* and *nonwords*.

For *words*, we used code to automatically retrieve fitting stimuli, and for *nonwords*, we used a combination of manual nonword-creation (Han) and manual selection from a nonword database (Jasmin).
Both were then checked by all team members to ensure that their respective stimuli conditions were met.

## Words
Conditions for words to be included:
* **length** maximum 7 characters
* **part-of-speech (POS)** noun
* **log frequency** higher than 2
* **non-cognates**


Datasets used in word collection:
* Stimuli and their valence: [`BRM-emot-submit.csv`](https://link.springer.com/article/10.3758/s13428-012-0314-x)
* Frequency: [`SUBTLEXusfrequencyabove1.xls`](https://www.ugent.be/pp/experimentele-psychologie/en/research/documents/subtlexus/overview.htm)
* Cognates: [`CogNet-v1.0.tsv`](https://github.com/kbatsuren/CogNet/blob/master/CogNet-v1.0.zip)

The aforementioned datasets were automatically parsed and only fitting instances were retained. These instances were then filtered into one of three categorical valences:
* **positive** (valence of 7 or higher)
* **negative** (valence of 3 or lower), and
* **neutral** (valence between (or equal to) 4.5 and 5.5). \

The remainder of words were not retained, as we did not want fuzzy edge cases, which would have made the analysis noisy.

> For more details see the explanations and documentation provided in the code: [`dataset_creation.ipynb`](https://github.com/jasminorth/indiv_diff/blob/main/dataset/dataset_creation.ipynb)

Additionally, counters per category (positive, negative, neutral) were implemented to ensure more than 30 instances each. \
The objective behind that was to leave room for potential deletion of faulty instances (instances that do not truly fit the conditions).

The resulting dataset was then manually checked to ensure that no faulty words were included. This could entail issues like the wrong assignment of "noun" as POS or "non-cognate" as cognate status as well as words that did not seem to truly fit their assigned valence. \
Consequently, thorough manual review and post-hoc deletions resulted in 30 words per category: positive, negative, and neutral (90 in total).

## Nonwords
Conditions:
* target language (English):
  * correspond to phonotactical and orthographical rules of the target language
  * correspond to formation rules of nouns in target language
* length maximum 7 characters

Some were obtained by manual perturbation of existing english words, e.g., replacing characters in existing words, e.g., "trouble" $\to$ "trooble".
Others by using the ARC nonword database from [Macquarie University (Sydney-Australia)](http://www.cogsci.mq.edu.au/research/resources/nwdb/nwdb.html), enabling:
* only orthographically existing onsets
* only orthographically existing bodies \
 with a maximum length of 7 characters.

Both were combined and the resulting nonwords were then also manually checked to ensure that all aforementioned conditions were met.

# Statistical Testing of the Dataset
ANOVA tests indicated that word frequency did not differ significantly across emotional valence categories, $F(2, 93) = 0.55, p = .579$. \
In contrast, words did show a significant effect of emotional valence, $F(2, 93) = 3.36, p = .039$. \
Post-hoc comparisons using Tukey's HSD revealed that negative words were slightly longer than neutral words ($p = .049$), while differences between positive and the other categories were not significant. Levene's test confirmed homogeneity of variances for word length ($F(2, 93) = 2.29, p = .107$), indicating that the variability in word length is similar across the valence groups; therefore, the ANOVA result is reliable and not biased by unequal spread. \
Accordingly, word length will be incorporated as a covariate in subsequent analyses.




