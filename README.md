# Mining the UK Web Archive for Semantic Change Detection (Dataset)
## Spacy models

This repository contains the [Semantic_Change zenodo dataset](https://zenodo.org/record/3383660) converted to Spacy 2 models.

### Install

Download the models from this repository's releases using the following release tags:


- [v1.0.1 for Spacy 2](https://github.com/martysteer/Semantic_Change/releases/tag/1.0.1) or `pip install -r requirements-spacy2.txt` file.
- [v1.0.2 for Spacy 3](https://github.com/martysteer/Semantic_Change/releases/tag/1.0.2) or `pip install -r requirements-spacy3.txt` file.



### Use

```python
import spacy
nlp = spacy.load('en_ukwa_2000_semchange')
```



---

***Commands to convert the original CSV files***

The shape of the csv files are all the same (47886 words, vector length 100), so we manually add the word2vec header line to each file and transpose the commas to spaces:

```bash
for f in *.csv; do
sed '1 i\
47886 100
' $f | tr ',' ' ' > ${f%%.*}.txt
done
```

You can also download the format converted vector .txt files here: [vectors_2000-13.txt.zip](https://github.com/martysteer/Semantic_Change/releases/download/1.0.1/vectors_2000-13.txt.zip).



---

***Commands to build Spacy 2 models***

Convert the word vectors to a [Spacy model](https://v2.spacy.io/api/cli#init-model) using the command line. Have changed the naming convention of the models:

```bash
spacy init-model en ukwa_2000_semchange -v vectors_2000.txt --vectors-name ukwa_2000_semchange.vectors
```

Manually edit the meta.json file to add version, description, authors, urls, attributions etc.


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

[Package the models as python packages](https://v2.spacy.io/api/cli#package)

```bash
mkdir output
spacy package ukwa_2000_semchange output
cd output/en_ukwa_2000_semchange-1.0.1
python setup.py sdist
```





---

***Commands to build Spacy 3 models***

Convert the word vectors to a [Spacy model](https://spacy.io/api/cli#init-vectors) using the command line:

```bash
spacy init vectors en vectors_2000.txt ukwa_2000_semchange --name ukwa_2000_semchange.vectors
```

1. Manually edit the meta.json file to add version, description, authors, urls, attributions etc.


```json
{
  "lang":"en",
  "name":"ukwa_2000_semchange",
  "version":"1.0.2",
  "spacy_version":">=3.1.1,<3.2.0",
  "description":"UKWeb Archive Semantic Change word vectors for the year 2000",
  "author":"Tsakalidis, Adam, Bazzi, Marya, Cucuringu, Mihai, Basile, Pierpaolo, & McGillivray, Barbara. (2019). Mining the UK Web Archive for Semantic Change Detection (Dataset) [Data set]. Zenodo. https://doi.org/10.5281/zenodo.3383660",
  "email":"",
  "url":"https://github.com/martysteer/Semantic_Change",
  "license":"https://creativecommons.org/licenses/by/4.0/legalcode",
  "spacy_git_version":"ffaead8fe",
  "vectors":{
    "width":100,
    "vectors":47886,
    "keys":47886,
    "name":"ukwa_2000_semchange.vectors"
  },
  "labels":{

  },
  "pipeline":[

  ],
  "components":[

  ],
  "disabled":[

  ]
}
```

[Package the models as python packages](https://spacy.io/api/cli#package)

```bash
mkdir output
spacy package ukwa_2000_semchange output --build sdist
```

