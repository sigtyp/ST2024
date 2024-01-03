# ST2024
## Shared Task on Word Embedding Evaluation for Ancient and Historical Languages
In 2024, SIGTYP is hosting a Shared Task on Word Embedding Evaluation for Ancient and Historical Languages.

Since the rise of word embeddings, their evaluation has been considered a challenging task that sparked considerable debate regarding the optimal approach. The two major strategies that researchers have developed over the years are intrinsic and extrinsic evaluation. The first amounts to solving specially designed problems like semantic proportions or “odd one out”, or comparing word/sentence similarity scores yielded by a model to human judgement. The second one focuses on solving downstream NLP tasks, such as sentiment analysis or question answering, probing word or sentence representations in real-world applications.

In recent years, sets of downstream tasks called benchmarks have become a very popular, if not default, method to evaluate general-purpose word and sentence embeddings. Starting with decaNLP (McCann et al., 2018) and SentEval (Conneau & Kiela, 2018), multitask benchmarks for NLU keep appearing and improving every year. However, even the largest multilingual benchmarks, such as XGLUE, XTREME, XTREME-R or XTREME-UP (Hu et al., 2020; Liang et al., 2020; Ruder et al., 2021, 2023), only include modern languages. When it comes to ancient and historical languages, scholars mostly adapt/translate intrinsic evaluation datasets from modern languages or create their own diagnostic tests. We argue that there is a need for a universal evaluation benchmark for embeddings learned from ancient and historical language data and view this shared task as a proving ground for it. 

The shared task involves solving the following problems for 12+ ancient and historical languages that belong to 4 language families and use 6 different scripts. 

## Subtasks

**A. Constrained**
  1. POS-tagging
  2. Full morphological annotation
  3. Lemmatisation

**B. Unconstrained**
  1. POS-tagging
  2. Full morphological annotation
  3. Lemmatisation
  4. Filling the gaps
      * Word-level
      * Character-level
    
For subtask A, participants are not allowed to use any additional data; however, they can reduce and balance provided training datasets if they see fit. For subtask B, participants are allowed to use any additional data in any language, including pre-trained embeddings and LLMs. 

## Data
For tasks 1-3, we use [Universal Dependencies](https://universaldependencies.org/) v. 2.12 data (Zeman et al., 2023) in 11 ancient and historical languages, complemented by 5 Old Hungarian codices from the [MGTSZ](http://oldhungariancorpus.nytud.hu/en-codices.html) website (HAS Research Institute for Linguistics, 2018) that are annotated to the same standard as the corpora available through UD.  UD corpora containing less than 1K examples or having only a test set were not taken into account. 

For task 4, we add historical Irish data from [CELT](https://celt.ucc.ie/publishd.html) (Ó Corráin et al., 1997), [Corpas Stairiúil na Gaeilge](http://corpas.ria.ie/index.php?fsg_function=1) (Acadamh Ríoga na hÉireann, 2017), and digital editions of the [St. Gall glosses](http://www.stgallpriscian.ie/) (Bauer et al., 2017) and the [Würzburg glosses](https://wuerzburg.ie/) (Doyle, 2018) as a case study of how performance may vary on different historical stages of the same language. Each Irish text taken from CELT is labelled "Old", "Middle" or "Early Modern" in accordance with the language labels provided in CELT metadata. We only include a CELT text in the dataset if it has a single Irish language label, and if it matches the dates (also provided in the metadata) of this period of the Irish language history. Some Irish texts may contain bits in Latin. 

A detailed list of text sources for each language in the dataset is provided [here](https://github.com/sigtyp/ST2024/blob/main/list_of_text_sources.md).

We set the upper temporal boundary to 1700 CE and do not include texts created later than this date in our dataset. The choice of this date is driven by the fact that most of the historical language data used in word embedding research dates back to the 18th century CE or later, and we would like to focus on the more challenging and yet uncovered data.

The following table gives a brief overview of the data. We use ISO 639-3 codes wherever they exist and special 4-letter codes based on them otherwise. The “Script” column refers to the scripts used in the dataset, not to the script(s) a particular language used (e.g. our Sanskrit corpus is transliterated from Devanagari into the Latin script). The “Dating” column describes the period when texts in the dataset were created, not when a particular language existed. The dates are cited according to the electronic editions/corpora these texts come from. Finally, we provide the size of each subset in sentences (S) and tokens (T).

**NB!** Our training, validation and test splits are different from those in the UD repositories. The `train : validation : test` proportion is `0.8 : 0.1 : 0.1` split by the number of sentences.  

|Language|Code|Family|Branch|Script|Dating|Train-T|Valid-T|Test-T|Train-S|Valid-S|Test-S|
|:-------|:--:|:-----|:-----|:-----|:-----|:-------:|:-------:|:-------:|:-------:|:------:|:------:|
|Ancient Greek|grc|Indo-European|Hellenic|Greek|VIII c. BCE – 110 CE|334,043|41,905|41,046|24,800|3,100|3,101|
|Ancient Hebrew|hbo|Afro-Asiatic|Semitic|Hebrew|X c. CE|40,244|4,862|4,801|1,263|158|158|
|Classical Chinese|lzh|Sino-Tibetan|Sinitic|Hanzi|47 – 220 CE|346,778|43,067|43,323|68,991|8,624|8,624|
|Coptic|cop|Afro-Asiatic|Egyptian|Coptic|I – II c. CE|57,493|7,282|7,558|1,730|216|217|
|Gothic|got|Indo-European|Germanic|Latin|V – VIII c. CE|44,044|5,724|5,568|4,320|540|541|
|Medieval Icelandic|isl|Indo-European|Germanic|Latin|1150 – 1680 CE|473,478|59,002|58,242|21,820|2,728|2,728|
|Classical and Late Latin|lat|Indo-European|Romance|Latin|I c. BCE – IV c. CE|188,149|23,279|23,344|16,769|2,096|2,097|
|Medieval Latin|latm|Indo-European|Romance|Latin|774 – early XIV c. CE|599,255|75,079|74,351|30,176|3,772|3,773|
|Old Church Slavonic|chu|Indo-European|Slavonic|Cyrillic|X – XI c. CE|159,368|19,779|19,696|18,102|2,263|2,263|
|Old East Slavic|orv|Indo-European|Slavonic|Cyrillic|1025 – 1700 CE|250,833|31,078|32,318|24,788|3,098|3,099|
|Old French|fro|Indo-European|Romance|Latin|1180 CE|38,460|4,764|4,870|3,113|389|390|
|Vedic Sanskrit|san|Indo-European|Indo-Aryan|Latin (transcr.)|1500 – 600 BCE|21,786|2,729|2,602|3,197|400|400|
|Old Hungarian|ohu|Finno-Ugric|Ugric|Latin|1440 – 1521 CE|129,454|16,138|16,116|21,346|2,668|2,669|
|Old Irish|sga|Indo-European|Celtic|Latin|600 – 900 CE|88,774|11,093|11,048|8,748|1,093|1,094|
|Middle Irish|mga|Indo-European|Celtic|Latin|900 – 1200 CE|251,684|31,748|31,292|14,308|1,789|1,789|
|Early Modern Irish|ghc|Indo-European|Celtic|Latin|1200 – 1700 CE|673,449|115,163|79,600|24,440|3,055|3,056|

The data for tasks 1-3 is the same and can be found in the *morphology* folder in `conllu` format. Tasks 4a and 4b have their own data folders: *fill_mask_word* and *fill_mask_char*, where each file is a two-column table in `tsv` format (`quotechar="^"`). Each file is named with a language code from the table above and a _train/valid/test_ prefix. 

**UPD.** For your convenience, we added extra information for tasks 4a and 4b: the indices of masked tokens and masked tokens themselves for each sentence. You can find this information in `json` files in *fill_mask_word* and *fill_mask_char* folders.

Please note that Old Hungarian texts come from diplomatic editions, i.e. they haven't been normalised and present some specific orthographic notation. We left this as is with the exception of punctuation: wherever a token in Old Hungarian data had a `PUNCT` POS-tag, we set its form to be equal to lemma, thus getting rid of `·Γ`, `:~`, `|Γ` etc. complex punctuation marks.

### Data format for tasks 1-3

**NB!** Old Hungarian files don't have any metadata (#source, #text etc.), only annotated sentences.

```
# source = Jerome's Vulgate, Revelation 9
# text = et cruciatus eorum ut cruciatus scorpii cum percutit hominem
# sent_id = 33745
1	et	et	CCONJ	C-	_	4	cc	_	ref=REV_9.5
2	cruciatus	cruciatus	NOUN	Nb	Case=Nom|Gender=Masc|Number=Sing	4	nsubj:outer	_	ref=REV_9.5
3	eorum	is	PRON	Pp	Case=Gen|Gender=Masc|Number=Plur|Person=3|PronType=Prs	2	det	_	ref=REV_9.5
4	ut	ut	ADV	Dq	PronType=Rel	0	root	_	ref=REV_9.5
5	cruciatus	cruciatus	NOUN	Nb	Case=Nom|Gender=Masc|Number=Sing	4	nsubj	_	ref=REV_9.5
6	scorpii	scorpios	NOUN	Nb	Case=Gen|Gender=Masc|Number=Sing	5	nmod	_	ref=REV_9.5
7	cum	cum	SCONJ	G-	_	8	mark	_	ref=REV_9.5
8	percutit	percutio	VERB	V-	Mood=Ind|Number=Sing|Person=3|Tense=Pres|VerbForm=Fin|Voice=Act	5	acl	_	ref=REV_9.5
9	hominem	homo	NOUN	Nb	Case=Acc|Gender=Masc|Number=Sing	8	obj	_	ref=REV_9.5
```

### Data format for task 4a
For this task, 10% of tokens in each sentence were randomly replaced with a `[MASK]` token. Please keep in mind that some sentences have more than one masked token, and some (short) sentences have none.

**NB!** Here and below we provide examples from different languages in one table, but in the dataset each language has its own data file(s). 

#### TSV
|masked|src|
|:-----|:--|
|Cé [MASK] secht [MASK] im gin sóee suilgind, co bráth, mó cech delmaimm, issed ma do-ruirminn.|Cé betis secht tengtha im gin sóee suilgind, co bráth, mó cech delmaimm, issed ma do-ruirminn.|
|ѿ негоже рожает [MASK] с҃нъ преже всѣх вѣкъ|ѿ негоже рожает сѧ с҃нъ преже всѣх вѣкъ|
|豈人[MASK]之子孫則必不善哉|豈人主之子孫則必不善哉|

#### JSON
```
[
    {
        "src": "Sith do denamh doib iar sin.",
        "masked": "Sith do denamh doib iar sin [MASK]",
        "masked_tokens": [
            {
                "mask_idx": 6,
                "masked_token": "."
            }
        ]
    },
   {
        "src": "\"Créd tucc ort cen teacht dá hiarraidh a cCarn Chaireadha theas mar ar gealladh dhuit í,\" ol Oisín.",
        "masked": "\"Créd tucc ort cen teacht dá hiarraidh a cCarn [MASK] [MASK] mar ar gealladh dhuit í,\" ol Oisín.",
        "masked_tokens": [
            {
                "mask_idx": 10,
                "masked_token": "Chaireadha"
            },
            {
                "mask_idx": 11,
                "masked_token": "theas"
            }
        ]
    }
]
```

### Data format for task 4b
For languages with alphabetical writing systems, sentences were split into individual characters. For Classical Chinese, each Hanzi character was decomposed into individual strokes with the help of [hanzipy](https://pypi.org/project/hanzipy/) package (we used the deepest decomposition level available, "graphical"). Then, 5% of characters in each sentence were randomly replaced with a `[_]` token. Please keep in mind that some sentences have more than one masked character, and some (short) sentences have none.

#### TSV
|masked|src|
|:-----|:--|
|Cé betis se[\_]ht te[\_]gtha im gin s[\_]ee suilgind, co bráth, mó cech[\_]delmaimm, isse[\_] ma do-ruirminn.|Cé betis secht tengtha im gin sóee suilgind, co bráth, mó cech delmaimm, issed ma do-ruirminn.|
|ѿ негоже рожает с[\_] с҃нъ п[\_]еже всѣх вѣкъ|ѿ негоже рожает сѧ с҃нъ преже всѣх вѣкъ|
|丨凵一口丷一人一一[\_]一[\_]一一丨一丶戈㇝㇇亅一㇇亅一㇒㇛丶亅八[\_]二八亅丨𠁼㇃丿一丿丨丶一二丨丷丷一口一丨一戈口|豈人主之子孫則必不善哉|

#### JSON
```
[
    {
        "src": "Sith do denamh doib iar sin.",
        "masked": "Sith do denamh doib iar [_]in.",
        "masked_tokens": [
            {
                "mask_idx": 24,
                "masked_token": "s"
            }
        ]
    }
]
```

## Evaluation Procedure
The shared task is hosted on CodaLab. Following the authors of GLUE and SuperGLUE (Wang et al., 2019, 2020), we weigh each task equally and provide a macro-average of per-task scores as an overall score. For tasks with multiple metrics (e.g., F1 and accuracy), we use an unweighted average of the metrics as the score for the task when computing the overall macro-average.

|Task|Metrics|
|:-----|:--|
|POS-tagging| Accuracy @1, F1|
|Detailed morphological annotation|Macro-average of Accuracy @1 per tag|
|Lemmatisation|Accuracy @1, Accuracy @3|
|Filling the gaps (word-level)|Accuracy @1, Accuracy @3|
|Filling the gaps (character-level)|Accuracy @1, Accuracy @3|

## Submission Format

### Unconstrained Subtask & Phase 1 of the Constrained Subtask
You should submit a `.zip` file with the following folder structure. Please make sure that your folder & file names are exactly as displayed below!

```
📂 fill_mask_char
    ├── chu.json
    ├── cop.json
    ├── fro.json
    └── ...
📂 fill_mask_word
    ├── chu.json
    ├── cop.json
    ├── fro.json
    └── ...
📂 pos_tagging
    ├── chu.json
    ├── cop.json
    ├── fro.json
    └── ...
📂 morph_features
    ├── chu.json
    ├── cop.json
    ├── fro.json
    └── ...
📂 lemmatisation
    ├── chu.json
    ├── cop.json
    ├── fro.json
    └── ...

```

### Phase 2 of the Constrained Subtask

For the Phase 2 of the constrained subtask, you should upload your pretrained embeddings as binary files and a Python function to load them. Your code should be compatible with `Python 3.9`. Your function should take a path to the model file as input and return a loaded model object, where vectors can be accessed by keys (= words from the model's vocabulary). If any additional libraries are required to load your embedding models, please specify them and their versions in the `requirements.txt` file. We kindly ask you to provide a short description of your models in the `metadata.txt` file.

```
📂 embeddings
    ├── load_embeddings.py
    ├── requirements.txt
    ├── metadata.txt
    ├── chu.bin
    ├── cop.bin
    ├── fro.bin
    └── ...
```

Here is an example of a load function (uses `gensim==4.3.0`):

```
import gensim

def load_model(model_path, binary=True):
    """
    Loads a pretrained word2vec model.
    :param model_path: str, path tot the model file
    :param binary: if the model is compressed, is it in binary or text format
    :return: KeyedVectors object
    """
    return gensim.models.KeyedVectors.load_word2vec_format(model_path, binary=binary)
```

Here is an example of how we should be able to use your function:

```
> model = load_model(model_path)
> model['ocus']

[Out]: array([ 1.5733392 , -0.8281076 ,  3.14848   ,  0.2219027 ,  0.5242622 ,
        1.6347595 , -0.4801302 , -0.47291416, -0.2864287 ,  1.4071647 ,
        0.5106803 ,  0.63692063, -0.23320669,  0.94002354, -0.5531442 ,
        1.7095504 ,  0.7174922 , -1.8853649 ,  0.9951415 ,  2.1806333 ,
       -1.1936942 ,  0.23348695,  0.7454169 ,  0.44898587,  2.4976215 ,
        0.53814757,  2.072146  ,  1.2090036 , -0.10769089,  0.97834873,
       -0.20169446, -1.7276735 ,  0.36428085,  0.8504869 , -1.2741064 ,
       -0.7176749 ,  1.2578478 ,  1.4141568 ,  2.3510249 , -1.2755529 ,
        0.3206452 ,  0.6595537 , -1.3546827 ,  0.45805138, -0.1383015 ,
        0.21479964, -0.4529127 , -1.0392785 , -1.9884776 , -1.7070132 ,
        0.4793383 , -2.1326056 , -1.457751  ,  0.10569981, -2.7827444 ,
       -0.57717484, -1.9276508 ,  0.71045595, -0.41069573,  0.48718056,
       -1.2526991 , -0.79434067,  2.0833015 , -2.0765586 , -2.348544  ,
        1.0221741 ,  0.6412075 , -0.19687717,  0.7608868 , -0.6060138 ,
        2.066918  ,  0.25159642, -1.186929  ,  1.5634978 ,  0.31453454,
       -2.011479  ,  0.11616329,  1.073292  , -1.5631199 ,  0.21954271,
       -2.356843  , -1.2546052 , -0.3317857 , -0.894448  ,  2.7144961 ,
       -0.51580656,  2.1599793 ,  1.7939224 ,  2.3818297 , -0.33923644,
       -0.25269115,  0.32848105, -0.37058732,  0.06037209,  0.682728  ,
       -1.103239  ,  0.705506  , -1.9009618 , -1.4850595 ,  0.58235765],
      dtype=float32)
```

### POS-tagging
You should submit a `.json` file with a list of sentences. Each sentence is a list of `(token, POS-tag)` tuples.

```
[
    [
        ["quem", "PRON"],
        ["me", "PRON"],
        ["arbitramini", "VERB"],
        ["non", "ADV"],
        ["sum", "AUX"],
        ["ego", "PRON"]
    ],
    [
        ["hospitalitatem", "NOUN"],
        ["sectantes", "VERB"]
    ],
    [
        ["secundum", "ADP"],
        ["hominem", "NOUN"],
        ["dico", "VERB"]
    ]
]
```

### Detailed morphological annotation
Your submission is a `.json` file again, but with a bit more complicated structure. It is a list of sentences, and each sentence is a list of tokens, while each token is a dictionary that contains the form, its POS-tag and all morphological features. The inventory of morphological feautures, as well as their names, are specific to each language (please refer to the training data). `UPOS` and `Form` keys are universal, i.e. valid for every language. **NB!** You have to submit UPOS in this task, but you don't have to submit lemma.

```
[
    [
        {
            "Case": "Acc",
            "Gender": "Fem",
            "Number": "Sing",
            "UPOS": "NOUN",
            "Form": "hospitalitatem"
        },
        {
            "Case": "Nom",
            "Gender": "Masc",
            "Number": "Plur",
            "Tense": "Pres",
            "VerbForm": "Part",
            "Voice": "Act",
            "UPOS": "VERB",
            "Form": "sectantes"
        }
    ],
    [
        {
            "UPOS": "ADP",
            "Form": "secundum"
        },
        {
            "Case": "Acc",
            "Gender": "Masc",
            "Number": "Sing",
            "UPOS": "NOUN",
            "Form": "hominem"
        },
        {
            "Mood": "Ind",
            "Number": "Sing",
            "Person": "1",
            "Tense": "Pres",
            "VerbForm": "Fin",
            "Voice": "Act",
            "UPOS": "VERB",
            "Form": "dico"
        }
    ]
]
```

### Lemmatisation
Similarly to POS-tagging, you should submit a `.json` file with a list of sentences, but in this case each sentence is a list of `(token, (lemma1, lemma2, lemma3))` tuples. The second element of this tuple is another tuple/list of your top-3 lemma predictions. Remember that the order of your predictions is important!  If you have less than 3 predictions, you can submit empty strings.

```
[
    [
        ["quem", ["quis", "ques", "que"]],
        ["me", ["ego", "me", "messe"]],
        ["arbitramini", ["arbitror", "arbitrar", "arbitramini"]],
        ["esse", ["sum", "esse", "ego"]],
        ["non", ["non", "no", ""]],
        ["sum", ["sum", "esse", "sunt"]],
        ["ego", ["ego", "me", "esse"]]
    ],
    [
        ["hospitalitatem", ["hospitalitas", "hospitalis", "hospitalitus"]],
        ["sectantes", ["secto", "sectum", "sectant"]]
    ],
    [
        ["secundum", ["secundum", "secundus", "secund"]],
        ["hominem", ["homo", "homus", "hominem"]],
        ["dico", ["dico", "dixi", ""]]
    ]
]
```

### Fill-mask tasks
Submissions should be `json` files with a list of sentences, where each sentence is a dictionary. The key "masked" is a masked sentence provided, the key "text" is a restored sentence, and the key "masked_tokens" is a list of your predictions for masked tokens. We advise to provide your top-3 predictions for each masked token, but if you have less, you can submit empty strings. **NB!** The order of masked tokens and the order within your top-3 predictions is important! In the example below, `["ni", "na", ""]` is a list of top-3 predictions for the first masked token, where `"ni"` is the one with the highest probability; `["⁊", "&", "ocus"]` is a list of top-3 predictions for the second masked token etc.

#### Word-level
```
[
  {
    "text": "‘Sech ni ricfe iluc, ⁊ ni toruis húc’.",
    "masked": "‘Sech [MASK] ricfe iluc, [MASK] ni toruis húc’.",
    "masked_tokens": [
                      ["ni", "na", ""],
                      ["⁊", "&", "ocus"]
                     ]
  },
  {
    "text": ".i. ni fiad chách",
    "masked": "[MASK] ni fiad chách",
    "masked_tokens": [
                      [".i.", "i.e.", "éd"]
                     ]
  }
]
```

#### Character-level
```
[
  {
    "text": "Ó domun co brait ar Zedechias mac Iosias."
    "masked": "Ó do[_]un co brait ar Zedechias mac[_]Iosias.",
    "masked_tokens": [
                      ["m", "n", ""],
                      [" ", "-", "c"]
                     ]
  }
]
```

## Paper submission 
Participants will be invited to describe their system in a paper for the SIGTYP workshop proceedings. The task organisers will write an overview paper that describes the task and summarises the different approaches taken, and analyses their results. 

Paper submission instructions will be the same as for the workshop. Each team participating in the shared task is expected to submit a paper of 4 to 8 pages, plus additional pages for references, formatted according to the workshop guidelines. The paper should describe the system and the resources used along with the libraries used to develop the system. The methodology/strategy should be documented in such a way that the readers and other researchers are able to replicate the work from the system description in the paper. 

## Important Dates
 - **05 Nov 2023:** Release of training and validation data
 - **02 Jan 2024:** Release of test data
 - **09 Jan 2024:** Submission of results for the unconstrained task and phase 1 of the constrained subtask
 - **12 Jan 2024:** Submission of results for phase 2 of the constrained subtask
 - **13 Jan 2024:** Notification of results
 - **20 Jan 2024:** Submission of shared task papers
 - **27 Jan 2024:** Notification of acceptance to authors
 - **03 Feb 2024:** Camera-ready
 - **15 Mar 2024:** Video recordings due
 - **21/22 Mar 2024:** SIGTYP workshop
 
## Important Links

Constrained subtask on CodaLab

[**Constrained**](https://codalab.lisn.upsaclay.fr/competitions/16822)

Unconstrained task on CodaLab

[**Unconstrained**](https://codalab.lisn.upsaclay.fr/competitions/16818)

To register for the Shared Task, please fill in the form on the link below.

[**Registration**](https://docs.google.com/forms/d/e/1FAIpQLSdINgMfzzZGIZ-uBVQhvyndB6yeaaj-wT7v45A6UB4F2h6QBQ/viewform?usp=sf_link)

Please cite these if you are using the dataset (APA-style citations can be found in the list of references below).

[**Bibliography**](https://github.com/sigtyp/ST2024/blob/main/bibliography.bib)

## Task Organizers 
* **Oksana Dereza**, Insight SFI Research Centre for Data Analytics, Data Science Institute, University of Galway 
* **Priya Rani**, SFI Centre for Research and Training in AI, Data Science Institute, University of Galway 
* **Atul Kr. Ojha**, Insight SFI Research Centre for Data Analytics, Data Science Institute, University of Galway 
* **Adrian Doyle**, Insight SFI Research Centre for Data Analytics, Data Science Institute, University of Galway 
* **Pádraic Moran**, School of Languages, Literatures and Cultures, Moore Institute, University of Galway
* **John P. McCrae**, Insight SFI Research Centre for Data Analytics, Data Science Institute, University of Galway

## References 
1. Acadamh Ríoga na hÉireann. (2017). Corpas Stairiúil na Gaeilge 1600-1926. Acadamh Ríoga na hÉireann. http://corpas.ria.ie/index.php?fsg_function=1
2. Bauer, B., Hofman, R., & Moran, P. (2017). St. Gall Priscian Glosses, version 2.0. http://www.stgallpriscian.ie/
3. Conneau, A., & Kiela, D. (2018). SentEval: An Evaluation Toolkit for Universal Sentence Representations. Proceedings of the Eleventh International Conference on Language Resources and Evaluation (LREC 2018). https://aclanthology.org/L18-1269/
4. Doyle, A. (2018). Würzburg Irish Glosses. https://wuerzburg.ie/
5. Ge, H., Sun, C., Xiong, D., & Liu, Q. (2021). Chinese WPLC: A Chinese Dataset for Evaluating Pretrained Language Models on Word Prediction Given Long-Range Context. Proceedings of the 2021 Conference on Empirical Methods in Natural Language Processing, 3770–3778. https://doi.org/10.18653/v1/2021.emnlp-main.306
6. HAS Research Institute for Linguistics. (2018). Old Hungarian Codices. Hungarian Generative Diachronic Syntax. http://oldhungariancorpus.nytud.hu/en-codices.html
7. Hu, J., Ruder, S., Siddhant, A., Neubig, G., Firat, O., & Johnson, M. (2020). XTREME: A Massively Multilingual Multi-task Benchmark for Evaluating Cross-lingual Generalization. Proceedings of the 37th International Conference on Machine Learning (ICML 2020), 4411–4421.
8. Kondratyuk, D., & Straka, M. (2019). 75 Languages, 1 Model: Parsing Universal Dependencies Universally. Proceedings of the 2019 Conference on Empirical Methods in Natural Language Processing and the 9th International Joint Conference on Natural Language Processing (EMNLP-IJCNLP), 2779–2795. https://doi.org/10.18653/v1/D19-1279
9. Liang, Y., Duan, N., Gong, Y., Wu, N., Guo, F., Qi, W., Gong, M., Shou, L., Jiang, D., Cao, G., Fan, X., Zhang, R., Agrawal, R., Cui, E., Wei, S., Bharti, T., Qiao, Y., Chen, J.-H., Wu, W., … Zhou, M. (2020). XGLUE: A New Benchmark Dataset for Cross-lingual Pre-training, Understanding and Generation. Proceedings of the 2020 Conference on Empirical Methods in Natural Language Processing (EMNLP), 6008–6018. https://doi.org/10.18653/v1/2020.emnlp-main.484
10. McCann, B., Keskar, N. S., Xiong, C., & Socher, R. (2018). The Natural Language Decathlon: Multitask Learning as Question Answering (arXiv:1806.08730). arXiv. http://arxiv.org/abs/1806.08730
11. Ó Corráin, D., Morgan, H., Färber, B., Hazard, B., Purcell, E., Ó Dónaill, C., Lavelle, H., Nyhan, J., & McCarthy, E. (1997). CELT: Corpus of Electronic Texts. University College Cork. http://www.ucc.ie/celt
12. Ruder, S., Clark, J. H., Gutkin, A., Kale, M., Ma, M., Nicosia, M., Rijhwani, S., Riley, P., Sarr, J.-M. A., Wang, X., Wieting, J., Gupta, N., Katanova, A., Kirov, C., Dickinson, D. L., Roark, B., Samanta, B., Tao, C., Adelani, D. I., … Talukdar, P. (2023). XTREME-UP: A User-Centric Scarce-Data Benchmark for Under-Represented Languages. arXiv; arXiv:2305.11938.
13. Ruder, S., Constant, N., Botha, J., Siddhant, A., Firat, O., Fu, J., Liu, P., Hu, J., Garrette, D., Neubig, G., & Johnson, M. (2021). XTREME-R: Towards More Challenging and Nuanced Multilingual Evaluation. Proceedings of the 2021 Conference on Empirical Methods in Natural Language Processing, 10215–10245. https://doi.org/10.18653/v1/2021.emnlp-main.802
14. Simon, E. (2014). Corpus building from Old Hungarian codices. In: Katalin É. Kiss (ed.): The Evolution of Functional Left Peripheries in Hungarian Syntax. Oxford: Oxford University Press.
15. Wang, A., Pruksachatkun, Y., Nangia, N., Singh, A., Michael, J., Hill, F., Levy, O., & Bowman, S. R. (2020, February 12). SuperGLUE: A Stickier Benchmark for General-Purpose Language Understanding Systems. Proceedings of the 33d Conference on Neural Information Processing Systems  (NeurIPS 2019).
16. Wang, A., Singh, A., Michael, J., Hill, F., Levy, O., & Bowman, S. R. (2019, February 22). GLUE: A Multi-Task Benchmark and Analysis Platform for Natural Language Understanding. Proceedings of the 7th  International Conference on Learning Representations  (ICLR 2019).
17. Zeman, D., Nivre, J., Abrams, M., Ackermann, E., Aepli, N., Aghaei, H., Agić, Ž., Ahmadi, A., Ahrenberg, L., Ajede, C. K., Akkurt, S. F., Aleksandravičiūtė, G., Alfina, I., Algom, A., Alnajjar, K., Alzetta, C., Andersen, E., Antonsen, L., Aoyama, T., … Ziane, R. (2023). Universal Dependencies 2.12 [dataset]. http://hdl.handle.net/11234/1-5150
