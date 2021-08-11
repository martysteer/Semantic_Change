# Mining the UK Web Archive for Semantic Change Detection (Dataset)
## Spacy models

This repository contains the [Semantic_Change zenodo dataset](https://zenodo.org/record/3383660) converted to Spacy 2 models.

### Install

Download the models from this repository's releases using the following links:


- [en_ukwa_2000_semchange](https://github.com/martysteer/Semantic_Change/releases/download/1.0.1/en_ukwa_2000_semchange-1.0.1.tar.gz)
- [en_ukwa_2001_semchange](https://github.com/martysteer/Semantic_Change/releases/download/1.0.1/en_ukwa_2000_semchange-1.0.1.tar.gz)
...

Or `pip install -r requirements.txt` file.

You can also download the format converted vector .txt files here: [vectors_2000-13.txt.zip](https://github.com/martysteer/Semantic_Change/releases/download/1.0.1/vectors_2000-13.txt.zip).

### Use

```python
import spacy
nlp = spacy.load('en_ukwa_2000_semchange')
```





---

*Commands to convert the original CSV files are noted below, so they can be reprocessed for Spacy 3 (at some point).*

1. The shape of the csv files are all the same (47886 words, vector length 100), so we manually add the word2vec header line to each file and transpose the commas to spaces:

```bash
for f in *.csv; do
sed '1 i\
47886 100
' $f | tr ',' ' ' > ${f%%.*}.txt
done
```

1. Convert the word vectors to a [Spacy model](https://v2.spacy.io/api/cli#init-model) using the command line. Have changed the naming convention of the models:

```bash
spacy init-model en ukwa_2000_semchange -v vectors_2000.txt --vectors-name ukwa_2000_semchange.vectors
spacy init-model en ukwa_2001_semchange -v vectors_2001.txt --vectors-name ukwa_2001_semchange.vectors
spacy init-model en ukwa_2002_semchange -v vectors_2002.txt --vectors-name ukwa_2002_semchange.vectors
spacy init-model en ukwa_2003_semchange -v vectors_2003.txt --vectors-name ukwa_2003_semchange.vectors
spacy init-model en ukwa_2004_semchange -v vectors_2004.txt --vectors-name ukwa_2004_semchange.vectors
spacy init-model en ukwa_2005_semchange -v vectors_2005.txt --vectors-name ukwa_2005_semchange.vectors
spacy init-model en ukwa_2006_semchange -v vectors_2006.txt --vectors-name ukwa_2006_semchange.vectors
spacy init-model en ukwa_2007_semchange -v vectors_2007.txt --vectors-name ukwa_2007_semchange.vectors
spacy init-model en ukwa_2008_semchange -v vectors_2008.txt --vectors-name ukwa_2008_semchange.vectors
spacy init-model en ukwa_2009_semchange -v vectors_2009.txt --vectors-name ukwa_2009_semchange.vectors
spacy init-model en ukwa_2010_semchange -v vectors_2010.txt --vectors-name ukwa_2010_semchange.vectors
spacy init-model en ukwa_2011_semchange -v vectors_2011.txt --vectors-name ukwa_2011_semchange.vectors
spacy init-model en ukwa_2012_semchange -v vectors_2012.txt --vectors-name ukwa_2012_semchange.vectors
```

1. Manually edit the meta.json file to add version, description, authors, urls, attributions etc.


```json
{
  "lang":"en",
  "name":"ukwa_2000_semchange",
  "version":"1.0.1",
  "spacy_version":">=2.3.7",
  "description":"UKWeb Archive Semantic Change word vectors for the year 2000",
  "author":"Tsakalidis, Adam, Bazzi, Marya, Cucuringu, Mihai, Basile, Pierpaolo, & McGillivray, Barbara. (2019). Mining the UK Web Archive for Semantic Change Detection (Dataset) [Data set]. Zenodo. https://doi.org/10.5281/zenodo.3383660",
  "email":"",
  "url":"https://github.com/martysteer/Semantic_Change",
  "license":"https://creativecommons.org/licenses/by/4.0/legalcode",
  "spacy_git_version":"cae72e46d",
  "vectors":{
    "width":100,
    "vectors":47886,
    "keys":47886,
    "name":"ukwa_2000_semchange"
  },
  "pipeline":[

  ],
  "factories":{

  },
  "labels":{

  }
}
```




1. [package the models as python packages](https://v2.spacy.io/api/cli#package)

```bash
mkdir output
spacy package ukwa_2000_semchange output
cd output/en_ukwa_2000_semchange-1.0.1
python setup.py sdist
```

