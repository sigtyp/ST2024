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
For tasks 1-3, we use [Universal Dependencies](https://universaldependencies.org/) v. 2.12 data (Zeman et al., 2023) in 11 ancient and historical languages, complemented by 5 Old Hungarian codices from the [MGTSZ](http://oldhungariancorpus.nytud.hu/en-codices.html) website (HAS Research Institute for Linguistics, 2018) that are annotated to the same standard as the corpora available through UD.  UD corpora containing less than 1K examples or having only a test set were not taken into account. For task 4, we add historical Irish data from [CELT](https://celt.ucc.ie/publishd.html) (Ó Corráin et al., 1997) and [Corpas Stairiúil na Gaeilge](http://corpas.ria.ie/index.php?fsg_function=1) (Acadamh Ríoga na hÉireann, 2017) as a case study of how performance may vary on different historical stages of the same language. A detailed list of text sources for each language in the dataset is provided [here](https://github.com/sigtyp/ST2024/blob/main/list_of_text_sources.md).

We set the upper temporal boundary to 1700 CE and do not include texts created later than this date in our dataset. The choice of this date is driven by the fact that most of the historical language data used in word embedding research dates back to the 18th century CE or later, and we would like to focus on the more challenging and yet uncovered data.

The following table provides a brief overview of the data. We use ISO 639-3 codes wherever they exist and special 4-letter codes based on them otherwise. The “Script” column refers to the scripts used in the dataset, not to the script(s) a particular language used (e.g. our Sanskrit corpus is transliterated from Devanagari into the Latin script). The “Dating” column describes the period when texts in the dataset were created, not when a particular language existed. Finally, we provide the size of each subset in sentences (S) and tokens (T).

**NB!** Our training, validation and test splits are different from those in the UD repositories.

|Language|Code|Family|Branch|Script|Dating|Train-T|Valid-T|Test-T|Train-S|Valid-S|Test-S|
|:-------|:--:|:-----|:-----|:-----|:-----|:-------:|:-------:|:-------:|:-------:|:------:|:------:|
|Ancient Greek|grc|Indo-European|Hellenic|Greek|VIII c. BCE – 110 CE|334,043|41,905|41,046|24,800|3,100|3,101|
|Ancient Hebrew|hbo|Afro-Asiatic|Semitic|Hebrew|X c. CE|40,244|4,862|4,801|1,263|158|158|
|Classical Chinese|lzh|Sino-Tibetan|Sinitic|Hanzi|47 – 220 CE|346,778|43,067|43,323|68,991|8,624|8,624|
|Coptic|cop|Afro-Asiatic|Egyptian|Coptic|I – II c. CE|57,493|7,282|7,558|1,730|216|217|
|Gothic|got|Indo-European|Germanic|Latin|V – VIII c. CE|44,044|5,724|5,568|4,320|540|541|
|Medieval Icelandic|islm|Indo-European|Germanic|Latin|1150 – 1680 CE|473,478|59,002|58,242|21,820|2,728|2,728|
|Classical and Late Latin|lat|Indo-European|Romance|Latin|I c. BCE – IV c. CE|188,149|23,279|23,344|16,769|2,096|2,097|
|Medieval Latin|latm|Indo-European|Romance|Latin|774 – early XIV c. CE|599,255|75,079|74,351|30,176|3,772|3,773|
|Old Church Slavonic|chu|Indo-European|Slavonic|Cyrillic|X – XI c. CE|159,368|19,779|19,696|18,102|2,263|2,263|
|Old East Slavic|orv|Indo-European|Slavonic|Cyrillic|1025 – 1700 CE|250,833|31,078|32,318|24,788|3,098|3,099|
|Old French|fro|Indo-European|Romance|Latin|1180 CE|38,460|4,764|4,870|3,113|389|390|
|Vedic Sanskrit|sanv|Indo-European|Indo-Aryan|Latin (transcr.)|1500 – 600 BCE|21,786|2,729|2,602|3,197|400|400|
|Old Hungarian|ohu|Finno-Ugric|Ugric|Latin|1440 – 1521 CE|129,454|16,138|16,116|21,346|2,668|2,669|
|Old Irish|sga|Indo-European|Celtic|Latin|600 – 900 CE|52,202|6,821|6,302|3,873|484|485|
|Middle Irish|mga|Indo-European|Celtic|Latin|900 – 1200 CE|206,096|26,447|25,298|12,192|1,524|1,524|
|Early Modern Irish|ghc|Indo-European|Celtic|Latin|1200 – 1700 CE|522,779|54,946|55,952|17,321|2,162|2,159|

The data for tasks 1-3 is the same and can be found in the *morphology* folder in `conllu` format. Tasks 4a and 4b have their own data folders: *fill_mask_word* and *fill_mask_char*, where each file is a two-column table in `tsv` format (`quotechar="^"`). Each file is named with a language code from the table above and a _train/valid/test_ prefix. 

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

|masked|src|
|:-----|:--|
|Cé [MASK] secht [MASK] im gin sóee suilgind, co bráth, mó cech delmaimm, issed ma do-ruirminn.|Cé betis secht tengtha im gin sóee suilgind, co bráth, mó cech delmaimm, issed ma do-ruirminn.|
|ѿ негоже рожает [MASK] с҃нъ преже всѣх вѣкъ|ѿ негоже рожает сѧ с҃нъ преже всѣх вѣкъ|
|豈人[MASK]之子孫則必不善哉|豈人主之子孫則必不善哉|

### Data format for task 4b
For languages with alphabetical writing systems, sentences were split into individual characters. For Classical Chinese, each Hanzi character was decomposed into individual strokes with the help of [hanzipy](https://pypi.org/project/hanzipy/) package (we used the deepest decomposition level available, "graphical"). Then, 5% of characters in each sentence were randomly replaced with a `[_]` token. Please keep in mind that some sentences have more than one masked character, and some (short) sentences have none.

|masked|src|
|:-----|:--|
|Cé betis se[\_]ht te[\_]gtha im gin s[\_]ee suilgind, co bráth, mó cech[\_]delmaimm, isse[\_] ma do-ruirminn.|Cé betis secht tengtha im gin sóee suilgind, co bráth, mó cech delmaimm, issed ma do-ruirminn.|
|ѿ негоже рожает с[\_] с҃нъ п[\_]еже всѣх вѣкъ|ѿ негоже рожает сѧ с҃нъ преже всѣх вѣкъ|
|丨凵一口丷一人一一[\_]一[\_]一一丨一丶戈㇝㇇亅一㇇亅一㇒㇛丶亅八[\_]二八亅丨𠁼㇃丿一丿丨丶一二丨丷丷一口一丨一戈口|豈人主之子孫則必不善哉|

## Evaluation Procedure
The shared task is hosted on CodaLab. Following the authors of GLUE and SuperGLUE (Wang et al., 2019, 2020), we weigh each task equally and provide a macro-average of per-task scores as an overall score. For tasks with multiple metrics (e.g., F1 and accuracy), we use an unweighted average of the metrics as the score for the task when computing the overall macro-average.

## Paper submission 
Paper submission instructions will be the same as for the workshop. Each team participating in the shared task is expected to submit a paper of 4 to 8 pages, plus additional pages for references, formatted according to the workshop guidelines. The paper should describe the system and the resources used along with the libraries used to develop the system. The methodology/strategy should be documented in such a way that the readers and other researchers are able to replicate the work from the system description in the paper. 

## Important Dates
 - **05 Nov 2023:** Release of training and validation data
 - **02 Jan 2024:** Release of test data
 - **08 Jan 2024:** Submission of the systems
 - **13 Jan 2024:** Notification of results
 - **20 Jan 2024:** Submission of shared task papers
 - **27 Jan 2024:** Notification of acceptance to authors
 - **03 Feb 2024:** Camera-ready
 - **15 Mar 2024:** Video recordings due
 - **21/22 Mar 2024:** SIGTYP workshop
 
## Important Links
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
2. Conneau, A., & Kiela, D. (2018). SentEval: An Evaluation Toolkit for Universal Sentence Representations. Proceedings of the Eleventh International Conference on Language Resources and Evaluation (LREC 2018). https://aclanthology.org/L18-1269/
3. Ge, H., Sun, C., Xiong, D., & Liu, Q. (2021). Chinese WPLC: A Chinese Dataset for Evaluating Pretrained Language Models on Word Prediction Given Long-Range Context. Proceedings of the 2021 Conference on Empirical Methods in Natural Language Processing, 3770–3778. https://doi.org/10.18653/v1/2021.emnlp-main.306
4. HAS Research Institute for Linguistics. (2018). Old Hungarian Codices. Hungarian Generative Diachronic Syntax. http://oldhungariancorpus.nytud.hu/en-codices.html
5. Hu, J., Ruder, S., Siddhant, A., Neubig, G., Firat, O., & Johnson, M. (2020). XTREME: A Massively Multilingual Multi-task Benchmark for Evaluating Cross-lingual Generalization. Proceedings of the 37th International Conference on Machine Learning (ICML 2020), 4411–4421.
6. Kondratyuk, D., & Straka, M. (2019). 75 Languages, 1 Model: Parsing Universal Dependencies Universally. Proceedings of the 2019 Conference on Empirical Methods in Natural Language Processing and the 9th International Joint Conference on Natural Language Processing (EMNLP-IJCNLP), 2779–2795. https://doi.org/10.18653/v1/D19-1279
7. Liang, Y., Duan, N., Gong, Y., Wu, N., Guo, F., Qi, W., Gong, M., Shou, L., Jiang, D., Cao, G., Fan, X., Zhang, R., Agrawal, R., Cui, E., Wei, S., Bharti, T., Qiao, Y., Chen, J.-H., Wu, W., … Zhou, M. (2020). XGLUE: A New Benchmark Dataset for Cross-lingual Pre-training, Understanding and Generation. Proceedings of the 2020 Conference on Empirical Methods in Natural Language Processing (EMNLP), 6008–6018. https://doi.org/10.18653/v1/2020.emnlp-main.484
8. McCann, B., Keskar, N. S., Xiong, C., & Socher, R. (2018). The Natural Language Decathlon: Multitask Learning as Question Answering (arXiv:1806.08730). arXiv. http://arxiv.org/abs/1806.08730
9. Ó Corráin, D., Morgan, H., Färber, B., Toner, G., Hazard, B., Purcell, E., Ó Dónaill, C., Lavelle, H., Ua Súilleabháin, S., Nyhan, J., & McCarthy, E. (1997). CELT: Corpus of Electronic Texts. University College Cork. http://www.ucc.ie/celt
10. Ruder, S., Clark, J. H., Gutkin, A., Kale, M., Ma, M., Nicosia, M., Rijhwani, S., Riley, P., Sarr, J.-M. A., Wang, X., Wieting, J., Gupta, N., Katanova, A., Kirov, C., Dickinson, D. L., Roark, B., Samanta, B., Tao, C., Adelani, D. I., … Talukdar, P. (2023). XTREME-UP: A User-Centric Scarce-Data Benchmark for Under-Represented Languages. arXiv; arXiv:2305.11938.
11. Ruder, S., Constant, N., Botha, J., Siddhant, A., Firat, O., Fu, J., Liu, P., Hu, J., Garrette, D., Neubig, G., & Johnson, M. (2021). XTREME-R: Towards More Challenging and Nuanced Multilingual Evaluation. Proceedings of the 2021 Conference on Empirical Methods in Natural Language Processing, 10215–10245. https://doi.org/10.18653/v1/2021.emnlp-main.802
12. Simon, E. (2014). Corpus building from Old Hungarian codices. In: Katalin É. Kiss (ed.): The Evolution of Functional Left Peripheries in Hungarian Syntax. Oxford: Oxford University Press.
13. Wang, A., Pruksachatkun, Y., Nangia, N., Singh, A., Michael, J., Hill, F., Levy, O., & Bowman, S. R. (2020, February 12). SuperGLUE: A Stickier Benchmark for General-Purpose Language Understanding Systems. Proceedings of the 33d Conference on Neural Information Processing Systems  (NeurIPS 2019).
14. Wang, A., Singh, A., Michael, J., Hill, F., Levy, O., & Bowman, S. R. (2019, February 22). GLUE: A Multi-Task Benchmark and Analysis Platform for Natural Language Understanding. Proceedings of the 7th  International Conference on Learning Representations  (ICLR 2019).
15. Zeman, D., Nivre, J., Abrams, M., Ackermann, E., Aepli, N., Aghaei, H., Agić, Ž., Ahmadi, A., Ahrenberg, L., Ajede, C. K., Akkurt, S. F., Aleksandravičiūtė, G., Alfina, I., Algom, A., Alnajjar, K., Alzetta, C., Andersen, E., Antonsen, L., Aoyama, T., … Ziane, R. (2023). Universal Dependencies 2.12 [dataset]. http://hdl.handle.net/11234/1-5150
