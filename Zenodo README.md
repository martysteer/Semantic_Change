# Mining the UK Web Archive for Semantic Change Detection (Dataset)

To download the dataset that was introduced in [1], visit the following link (~330MB):

https://zenodo.org/record/3383660

The dataset contains the following files:

  - **word_labels.csv**: 47,886 *{word, label}* pairs; the label indicates whether the corresponding word has undergone semantic change ("change") or not ("static"). There are 65 words that have been marked as "change", as extracted from the Oxford English Dictionary.

  - **vectors_YEAR.csv**: for every file (YEAR in *{2000, ..., 2013}*), there are 47,886 rows in the form of *{word, dimension_1, ..., dimension_100}*. The dimensions correspond to the word2vec vector representation of the given word in a certain YEAR. For more details on the implementation, refer to [1].
  
  
  **References**

[1] Adam Tsakalidis, Marya Bazzi, Mihai Cucuringu, Pierpaolo Basile, Barbara McGillivray, 2019. "Mining the UK Web Archive for Semantic Change Detection". In *RANLP*.
