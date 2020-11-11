# Summary

Universal Dependencies syntax annotations from the GUM corpus (https://corpling.uis.georgetown.edu/gum/)

# Introduction

GUM, the Georgetown University Multilayer corpus, is an open source collection of richly annotated web texts from multiple text types. The corpus is collected and expanded by students as part of the curriculum in the course LING-367 "Computational Corpus Linguistics" at Georgetown University. The selection of text types is meant to represent different communicative purposes, while coming from sources that are readily and openly available (usually Creative Commons licenses), so that new texts can be annotated and published with ease.

The dependencies in the corpus up to GUM version 5 were originally annotated using Stanford Typed Depenencies (de Marneffe & Manning 2013) and converted automatically to UD using DepEdit (https://corpling.uis.georgetown.edu/depedit/). The rule-based conversion took into account gold entity annotations found in other annotation layers of the GUM corpus (e.g. entity annotations), and has since been corrected manually in native UD. The original conversion script used can found in the GUM build bot code from version 5, available from the (non-UD) GUM repository. Documents from version 6 of GUM onwards were annotated directly in UD, and subsequent manual error correction to all GUM data has also been done directly using the UD guidelines. For more details see the [corpus website](https://corpling.uis.georgetown.edu/gum/).

# Additional annotations in MISC

The MISC column contains **entity, coreference and discourse** annotations from the full GUM corpus, encoded using the annotations `Entity` and `Discourse`. The `Entity` annotation uses the CoNLL 2012 shared task bracketing format, which identifies entities using round opening and closing brackets as well as a unique ID per entity, repeated across mentions. In the following example, Czech composer Dvořák appears in a single token mention, labeled `(person-1)` indicating the entity type (`person`) combined with the unique ID of all mentions of Dvořák in the text (`person-1`). Multi-token mentions receive opening brackets on the line in which they open, such as `(person-49` (in this case Johannes Brahms), and a closing annotation `person-50)` at the token on which they end. Multiple annotations are possible for one token, corresponding to nested entities, e.g. `(event-48(person-49` below. Note that currently only plain coreference annotations are included in this format (including appositions and cataphora), but not split antecedent and bridging anaphora, which can be found in the GUM [source repo](https://github.com/amir-zeldes/gum/).

Discourse annotations are given in RST dependencies following the conversion from RST constituent trees as suggested by Li et al. (2014) - for the original RST constituent parses of GUM see the [source repo](https://github.com/amir-zeldes/gum/). At the beginning of each Elementary Discourse Unit (EDU), and annotation `Discourse` gives the discourse function of the unit beginning with that token, followed by a colon, the ID of the current unit, and an arrow pointing to the ID of the parent unit in the discourse parse. For instance, `Discourse=concession:28->29` in the example below means that this token begins discourse unit 28, which functions as a `concession` to unit 29, which begins at token 9 in this sentence. The unique `ROOT` node of the discourse tree has no arrow notation, e.g. `Discourse=ROOT:4` means that this token begins unit 4, which is the Central Discourse Unit (or discourse root) of the current document.

```
1	Although	although	SCONJ	IN	_	5	mark	_	Discourse=concession:28->29
2	Dvořák	Dvořák	PROPN	NNP	Number=Sing	5	nsubj	_	Entity=(person-1)
3	was	be	AUX	VBD	Mood=Ind|Number=Sing|Person=3|Tense=Past|VerbForm=Fin	5	cop	_	_
4	not	not	PART	RB	Polarity=Neg	5	advmod	_	_
5	aware	aware	ADJ	JJ	Degree=Pos	14	advcl	_	_
6	of	of	ADP	IN	_	7	case	_	_
7	it	it	PRON	PRP	Case=Nom|Gender=Neut|Number=Sing|Person=3|PronType=Prs	5	obl	_	Entity=(event-48)|SpaceAfter=No
8	,	,	PUNCT	,	_	5	punct	_	_
9	Johannes	Johannes	PROPN	NNP	Number=Sing	14	nsubj	_	Discourse=background:29->30|Entity=(event-48(person-49
10	Brahms	Brahms	PROPN	NNP	Number=Sing	9	flat	_	Entity=person-49)
11	was	be	AUX	VBD	Mood=Ind|Number=Sing|Person=3|Tense=Past|VerbForm=Fin	14	cop	_	_
```

# Documents and splits

The training, development and test sets contain complete, contiguous documents, balanced for genre. Test and dev contain similar amounts of data, usually around 2,500 tokens in each genre in each, and the rest is assigned to training. For the exact file lists in each split see:

https://github.com/UniversalDependencies/UD_English-GUM/tree/master/not-to-release/file-lists

# Acknowledgments

GUM annotation team (so far - thanks for participating!)

Adrienne Isaac, Akitaka Yamada, Amani Aloufi, Amelia Becker, Andrea Price, Andrew O\'Brien, Anna Runova, Anne Butler, Arianna Janoff, Ayan Mandal, Aysenur Sagdic, Bertille Baron, Bradford Salen, Brandon Tullock, Brent Laing, Candice Penelton, Chenyue Guo, Colleen Diamond, Connor O\'Dwyer, Cristina Lopez, Dan Simonson, Didem Ikizoglu, Edwin Ko, Emily Pace, Emma Manning, Ethan Beaman, Felipe De Jesus, Han Bu, Hana Altalhi, Hang Jiang, Hannah Wingett, Hanwool Choe, Hassan Munshi, Ho Fai Cheng, Hortensia Gutierrez, Jakob Prange, James Maguire, Janine Karo, Jehan al-Mahmoud, Jemm Excelle Dela Cruz, Jessica Kotfila, Joaquin Gris Roca, John Chi, Jongbong Lee, Juliet May, Katarina Starcevic, Katelyn MacDougald, Katherine Vadella, Lara Bryfonski, Leah Northington, Lindley Winchester, Linxi Zhang, Logan Peng, Lucia Donatelli, Luke Gessler, Mackenzie Gong, Margaret Anne Rowe, Margaret Borowczyk, Maria Stoianova, Mariko Uno, Mary Henderson, Maya Barzilai, Md. Jahurul Islam, Michael Kranzlein, Michaela Harrington, Minnie Annan, Mitchell Abrams, Mohammad Ali Yektaie, Naomee-Minh Nguyen, Nicholas Mararac, Nicholas Workman, Nicole Steinberg, Rachel Thorson, Rebecca Childress, Rebecca Farkas, Riley Breslin Amalfitano, Rima Elabdali, Robert Maloney, Ruizhong Li, Ryan Mannion, Ryan Murphy, Sakol Suethanapornkul, Sasha Slone, Sean Macavaney, Sean Simpson, Seyma Toker, Shane Quinn, Shannon Mooney, Shelby Lake, Shira Wein, Sichang Tu, Siddharth Singh, Siyu Liang, Stephanie Kramer, Sylvia Sierra, Talal Alharbi, Timothy Ingrassia, Trevor Adriaanse, Wenxi Yang, Xiaopei Wu, Yang Liu, Yilun Zhu, Yingzhu Chen, Yiran Xu, Young-A Son, Yu-Tzu Chang, Yuhang Hu, Yushi Zhao, Zhuosi Luo, Zhuxin Wang, Amir Zeldes

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
Genre: academic fiction nonfiction news spoken web wiki
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
