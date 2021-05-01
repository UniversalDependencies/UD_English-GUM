# Summary

Universal Dependencies syntax annotations from the GUM corpus (https://corpling.uis.georgetown.edu/gum/)

# Introduction

GUM, the Georgetown University Multilayer corpus, is an open source collection of richly annotated texts from multiple text types. The corpus is collected and expanded by students as part of the curriculum in the course LING-367 "Computational Corpus Linguistics" at Georgetown University. The selection of text types is meant to represent different communicative purposes, while coming from sources that are readily and openly available (usually Creative Commons licenses), so that new texts can be annotated and published with ease.

The dependencies in the corpus up to GUM version 5 were originally annotated using Stanford Typed Depenencies (de Marneffe & Manning 2013) and converted automatically to UD using DepEdit (https://corpling.uis.georgetown.edu/depedit/). The rule-based conversion took into account gold entity annotations found in other annotation layers of the GUM corpus (e.g. entity annotations), and has since been corrected manually in native UD. The original conversion script used can found in the GUM build bot code from version 5, available from the (non-UD) GUM repository. Documents from version 6 of GUM onwards were annotated directly in UD, and subsequent manual error correction to all GUM data has also been done directly using the UD guidelines. Enhanced dependencies were added semi-automatically from version 7.1 of the corpus. For more details see the [corpus website](https://corpling.uis.georgetown.edu/gum/).

# Additional annotations in MISC

The MISC column contains **entity, coreference, Wikification and discourse** annotations from the full GUM corpus, encoded using the annotations `Entity`, `Split`, `Bridge` and `Discourse`. The `Entity` annotation uses the CoNLL 2012 shared task bracketing format, which identifies potentially coreferring entities using round opening and closing brackets as well as a unique ID per entity, repeated across mentions. In the following example, actor Jared Padalecki appears in a single token mention, labeled `(person-1-Jared_Padalecki)` indicating the entity type (`person`) combined with the unique ID of all mentions of Padalecki in the text (`person-1`). Because Padalecki is a named entity with a corresponding Wikipedia page, the Wikification identifier corresponding to his Wikipedia page is given after the second hyphen, resulting in the unique entity ID (`person-1-Jared_Padalecki`). The labels for each part of the hyphen-separated annotation is given at the top of each document in a comment `# global.Entity = entity-GRP-identity`, indicating that these annotations consist of the entity type, coreference group and named entity identity. 

Multi-token mentions receive opening brackets on the line in which they open, such as `(person-97-Jensen_Ackles`, and a closing annotation `person-97-Jensen_Ackles)` at the token on which they end. Multiple annotations are possible for one token, corresponding to nested entities, e.g. `(time-175)time-189)` below corresponds to the last token of the time entities "2015" and "April 2015" respectively. 

```
# global.Entity = entity-GRP-identity
...
1	For	for	ADP	IN	_	4	case	4:case	Discourse=sequence:104->98
2	the	the	DET	DT	Definite=Def|PronType=Art	4	det	4:det	Bridge=abstract-173<event-188|Entity=(event-188
3	second	second	ADJ	JJ	Degree=Pos|NumType=Ord	4	amod	4:amod	_
4	campaign	campaign	NOUN	NN	Number=Sing	16	obl	16:obl:for	_
5	in	in	ADP	IN	_	10	case	10:case	_
6	the	the	DET	DT	Definite=Def|PronType=Art	10	det	10:det	_
7	Always	Always	ADV	NNP	Number=Sing	8	advmod	8:advmod	Entity=(abstract-173
8	Keep	Keep	PROPN	NNP	Number=Sing	10	compound	10:compound	_
9	Fighting	Fighting	PROPN	NNP	Number=Sing	8	xcomp	8:xcomp	_
10	series	series	NOUN	NN	Number=Sing	4	nmod	4:nmod:in	Entity=abstract-173)
11	in	in	ADP	IN	_	12	case	12:case	_
12	April	April	PROPN	NNP	Number=Sing	4	nmod	4:nmod:in	Entity=(time-189
13	2015	2015	NUM	CD	NumForm=Digit|NumType=Card	12	nmod:tmod	12:nmod:tmod	Entity=(time-175)event-188)time-189)|SpaceAfter=No
14	,	,	PUNCT	,	_	4	punct	4:punct	_
15	Padalecki	Padalecki	PROPN	NNP	Number=Sing	16	nsubj	16:nsubj	Entity=(person-1-Jared_Padalecki)
16	partnered	partner	VERB	VBD	Mood=Ind|Number=Sing|Person=3|Tense=Past|VerbForm=Fin	0	root	0:root	_
17	with	with	ADP	IN	_	18	case	18:case	_
18	co-star	co-star	NOUN	NN	Number=Sing	16	obl	16:obl:with	Entity=(person-97-Jensen_Ackles
19	Jensen	Jensen	PROPN	NNP	Number=Sing	18	appos	18:appos	_
20	Ackles	Ackles	PROPN	NNP	Number=Sing	19	flat	19:flat	Entity=person-97-Jensen_Ackles)
21	to	to	PART	TO	_	22	mark	22:mark	Discourse=purpose:105->104
22	release	release	VERB	VB	VerbForm=Inf	16	advcl	16:advcl:to	_
23	a	a	DET	DT	Definite=Ind|PronType=Art	24	det	24:det	Entity=(object-190
24	shirt	shirt	NOUN	NN	Number=Sing	22	obj	22:obj	Entity=object-190)
25	featuring	feature	VERB	VBG	VerbForm=Ger	24	acl	24:acl	Discourse=elaboration:106->105
26	both	both	PRON	DT	_	25	obj	25:obj	Entity=(object-191
27	of	of	ADP	IN	_	29	case	29:case	_
28	their	their	PRON	PRP$	Number=Plur|Person=3|Poss=Yes|PronType=Prs	29	nmod:poss	29:nmod:poss	Entity=(person-192)|Split=person-1-Jared_Padalecki<person-192,person-97-Jensen_Ackles<person-192
29	faces	face	NOUN	NNS	Number=Plur	26	nmod	26:nmod:of	Entity=object-191)|SpaceAfter=No
```

The additional annotations `Split` and `Bridge` mark non-strict identity anaphora (see the [Universal Anaphora](http://universalanaphora.org/) project for more details). For example, at token 28 in the example, the pronoun "their" refers back to two non-adjacent entities, requiring a split antecedent annotation. The value `Split=person-1-Jared_Padalecki<person-192,person-97-Jensen_Ackles<person-192` indicates that `person-192` (the pronoun "their") refers back to two previous Entity annotations, with pointers separatated by a comma: `person-1-Jared_Padalecki` and `person-97-Jensen_Ackles`. Bridging anaphora is annotated when an entity has not been mentioned before, but is resolvable in context by way of a different entity: for example, token 2 has the annotation `Bridge=abstract-173<event-188`, which indicates that although `event-188` ("the second campaign...") has not been mentioned before, its identity is mediated by the previous mention of another entity, `abstract-173` (the project "Always Keep Fighting", mentioned earlier in the document, to which the campaign event belongs).

Discourse annotations are given in RST dependencies following the conversion from RST constituent trees as suggested by Li et al. (2014) - for the original RST constituent parses of GUM see the [source repo](https://github.com/amir-zeldes/gum/). At the beginning of each Elementary Discourse Unit (EDU), and annotation `Discourse` gives the discourse function of the unit beginning with that token, followed by a colon, the ID of the current unit, and an arrow pointing to the ID of the parent unit in the discourse parse. For instance, `Discourse=purpose:105->104` at token 21 in the example below means that this token begins discourse unit 105, which functions as a `purpose` to unit 104, which begins at token 1 in this sentence ("Padalecki partnered with co-star Jensen Ackles --purpose-> to release a shirt..."). The unique `ROOT` node of the discourse tree has no arrow notation, e.g. `Discourse=ROOT:2` means that this token begins unit 2, which is the Central Discourse Unit (or discourse root) of the current document. 

More information and additional annotation layers can be found in the GUM [source repo](https://github.com/amir-zeldes/gum/).

# Metadata

Document metadata is given at the beginning of each new document in key-value pair comments beginning with the prefix `meta::`, as in:

```
# newdoc id = GUM_bio_padalecki
# global.Entity = entity-GRP-identity
# meta::dateCollected = 2019-09-10
# meta::dateCreated = 2004-08-14
# meta::dateModified = 2019-09-11
# meta::shortTitle = padalecki
# meta::sourceURL = https://en.wikipedia.org/wiki/Jared_Padalecki
# meta::speakerCount = 0
# meta::title = Jared Padalecki
```

# Documents and splits

The training, development and test sets contain complete, contiguous documents, balanced for genre. Test and dev contain similar amounts of data, usually around 1,800 tokens in each genre in each, and the rest is assigned to training. For the exact file lists in each split see:

https://github.com/UniversalDependencies/UD_English-GUM/tree/master/not-to-release/file-lists

# Acknowledgments

GUM annotation team (so far - thanks for participating!)

Adrienne Isaac, Akitaka Yamada, Alex Giorgioni, Alexandra Berends, Alexandra Slome, Amani Aloufi, Amelia Becker, Andrea Price, Andrew O\'Brien, Anna Runova, Anne Butler, Arianna Janoff, Ayan Mandal, Aysenur Sagdic, Bertille Baron, Bradford Salen, Brandon Tullock, Brent Laing, Candice Penelton, Chenyue Guo, Colleen Diamond, Connor O\'Dwyer, Cristina Lopez, Dan Simonson, Didem Ikizoglu, Edwin Ko, Emily Pace, Emma Manning, Ethan Beaman, Felipe De Jesus, Han Bu, Hana Altalhi, Hang Jiang, Hannah Wingett, Hanwool Choe, Hassan Munshi, Helen Dominic, Ho Fai Cheng, Hortensia Gutierrez, Jakob Prange, James Maguire, Janine Karo, Jehan al-Mahmoud, Jemm Excelle Dela Cruz, Jessica Kotfila, Joaquin Gris Roca, John Chi, Jongbong Lee, Juliet May, Jungyoon Koh, Katarina Starcevic, Katelyn MacDougald, Katherine Vadella, Khalid Alharbi, Lara Bryfonski, Leah Northington, Lindley Winchester, Linxi Zhang, Logan Peng, Lucia Donatelli, Luke Gessler, Mackenzie Gong, Margaret Borowczyk, Margaret Anne Rowe, Maria Stoianova, Mariko Uno, Mary Henderson, Maya Barzilai, Md. Jahurul Islam, Michael Kranzlein, Michaela Harrington, Minnie Annan, Mitchell Abrams, Mohammad Ali Yektaie, Naomee-Minh Nguyen, Nicholas Mararac, Nicholas Workman, Nicole Steinberg, Rachel Thorson, Rebecca Childress, Rebecca Farkas, Riley Breslin Amalfitano, Rima Elabdali, Robert Maloney, Ruizhong Li, Ryan Mannion, Ryan Murphy, Sakol Suethanapornkul, Sarah Bellavance, Sasha Slone, Sean Macavaney, Sean Simpson, Seyma Toker, Shane Quinn, Shannon Mooney, Shelby Lake, Shira Wein, Sichang Tu, Siddharth Singh, Siyu Liang, Stephanie Kramer, Sylvia Sierra, Talal Alharbi, Tatsuya Aoyama, Timothy Ingrassia, Trevor Adriaanse, Ulie Xu, Wenxi Yang, Xiaopei Wu, Yang Liu, Yi-Ju Lin, Yilun Zhu, Yingzhu Chen, Yiran Xu, Young-A Son, Yuhang Hu, Yushi Zhao, Yu-Tzu Chang, Zhuosi Luo, Zhuxin Wang, Amir Zeldes

... and other annotators who wish to remain anonymous!

## References

As a scholarly citation for the corpus in articles, please use this paper:

* Zeldes, Amir (2017) "The GUM Corpus: Creating Multilayer Resources in the Classroom". Language Resources and Evaluation 51(3), 581–612.

```
@Article{Zeldes2017,
  author    = {Amir Zeldes},
  title     = {The {GUM} Corpus: Creating Multilayer Resources in the Classroom},
  journal   = {Language Resources and Evaluation},
  year      = {2017},
  volume    = {51},
  number    = {3},
  pages     = {581--612},
  doi       = {http://dx.doi.org/10.1007/s10579-016-9343-x}
}
```

# Changelog

* 2021-05-01
  * Added MWTs
  * Added metadata
  * Comprehensive corrections

* 2021-03-10
  * Added enhanced dependencies

* 2021-01-20
  * Added documents from four new genres: conversation, speeches, textbooks and vlogs
  * Added Wikification annotations
  * Added bridging and split antecedent anaphora to MISC
  * Improved FEATS, now including Abbr and NumForm
  * Added sentence addressee annotations
  * Rebalanced splits to account for new genres

* 2020-10-31
  * Major improvements to entity and coreference consistency
  * Removed 'quantity' entity type
  * Added discourse dependency information in MISC column
  * Moved Typo annotation from MISC to FEATS

* 2020-03-06 
  * Added rest of GUM6 documents
  * Added entity and coreference annotations to the MISC column
  * Changed prepositional TO xpos to IN
  * Cardinal number lemmas are now numbers, not @card@
  * Identified more cases of orphan
  * Numerous corrections

* 2019-10-31v2.5
  * Added three new documents from GUM6 preview
  * Introduced use of the list relation according to the guidelines
  * Overhaul of flat relations for non-personal names
  * Numerous sporadic error corrections, and systematic overhaul of some lemmas throughout

* 2019-03-21
  * Added new documents from GUM version 5
  * Numerous error corrections, now conforming to UD2.4 validation

* 2018-11-08 v2.3
  * Added 'multiple' s_type annotation value (formerly subsumed in 'other')
  * Numerous error corrections

* 2018-07-01 v2.2
  * First official release

<pre>
=== Machine-readable metadata (DO NOT REMOVE!) ================================
Data available since: UD v2.2
License: CC BY-NC-SA 4.0
Includes text: yes
Genre: academic blog fiction government news nonfiction social spoken web wiki
Lemmas: manual native
UPOS: converted from manual
XPOS: manual native
Features: converted from manual
Relations: manual native
Contributors: Peng, Siyao;Zeldes, Amir
Contributing: elsewhere
Contact: amir.zeldes@georgetown.edu
===============================================================================
</pre>
