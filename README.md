# Summary

Universal Dependencies syntax annotations from the GUM corpus (https://gucorpling.org/gum/)

# Introduction

GUM, the Georgetown University Multilayer corpus, is an open source collection of richly annotated texts from multiple text types. The corpus is collected and expanded by students as part of the curriculum in the course LING-367 "Computational Corpus Linguistics" at Georgetown University. The selection of text types is meant to represent different communicative purposes, while coming from sources that are readily and openly available (usually Creative Commons licenses), so that new texts can be annotated and published with ease.

The dependencies in the corpus up to GUM version 5 were originally annotated using Stanford Typed Depenencies (de Marneffe & Manning 2013) and converted automatically to UD using DepEdit (https://gucorpling.org/depedit/). The rule-based conversion took into account gold entity annotations found in other annotation layers of the GUM corpus (e.g. entity annotations), and has since been corrected manually in native UD. The original conversion script used can found in the GUM build bot code from version 5, available from the (non-UD) GUM repository. Documents from version 6 of GUM onwards were annotated directly in UD, and subsequent manual error correction to all GUM data has also been done directly using the UD guidelines. Enhanced dependencies were added semi-automatically from version 7.1 of the corpus. For more details see the [corpus website](https://gucorpling.org/gum/).

# Additional annotations in MISC

The MISC column contains **entity, coreference, information status, Wikification and discourse** annotations from the full GUM corpus, encoded using the annotations `Entity`, `SplitAnte`, `Bridge` and `Discourse`. 

## Entity

The `Entity` annotation uses the CoNLL 2012 shared task bracketing format, which identifies potentially coreferring entities using round opening and closing brackets as well as a unique ID per entity, repeated across mentions. In the following example, actor Jared Padalecki appears in a single token mention, labeled `(1-person-giv:act-cf2*-1-coref-Jared_Padalecki)` indicating the entity type (`person`) combined with the unique ID of all mentions of Padalecki in the text (`1-person`). Because Padalecki is a named entity with a corresponding Wikipedia page, the Wikification identifier corresponding to his Wikipedia page is given after the last hyphen (`1-person-Jared_Padalecki`). We can also see an information status annotation (`giv:act`, indicating an aforementioned or 'given' entity, actively mentioned last no farther than the previous sentences; see Dipper et al. 2007), a Centering Theory annotation (`cf2*`, indicating he is the second most central salient entity in the sentence moving forward, and that he was mentioned in the previous sentence, indicated by the `*`), as well as minimum token ID information indicating the head tokens for fuzzy matching (in this case `1`, the first and only token  in this span) and the coreference type `coref`, indicating lexical subsequent mention. The labels for each part of the hyphen-separated annotation are given at the top of each document in a comment `# global.Entity = GRP-etype-infstat-centering-minspan-link-identity`, indicating that these annotations consist of the entity group id (i.e the coreference group), entity type, information status, centering theory annotation, minimal span of tokens for head matching, the coreference link type, and named entity identity (if available). 

Multi-token mentions receive opening brackets on the line in which they open, such as `(97-person-giv:inact-cf4-1,3-coref-Jensen_Ackles`, and a closing annotation `97)` at the token on which they end. Multiple annotations are possible for one token, corresponding to nested entities, e.g. `(175-time-giv:inact-cf5-1-coref)189)` below corresponds to the single token and last token of the time entities "2015" and "April 2015" respectively. 

```CoNLL-U
# global.Entity = GRP-etype-infstat-centering-minspan-link-identity
...
1	For	for	ADP	IN	_	4	case	4:case	Discourse=joint-sequence_m:104->98:2
2	the	the	DET	DT	Definite=Def|PronType=Art	4	det	4:det	Bridge=173<188|Entity=(188-event-acc:inf-cf6-3,6,8-sgl
3	second	second	ADJ	JJ	Degree=Pos|NumType=Ord	4	amod	4:amod	_
4	campaign	campaign	NOUN	NN	Number=Sing	16	obl	16:obl:for	_
5	in	in	ADP	IN	_	10	case	10:case	_
6	the	the	DET	DT	Definite=Def|PronType=Art	10	det	10:det	Entity=(173-abstract-giv:inact-cf3-2,4,5-coref
7	Always	Always	ADV	NNP	Number=Sing	8	advmod	8:advmod	XML=<hi rend:::"italic">
8	Keep	Keep	PROPN	NNP	Number=Sing	10	compound	10:compound	_
9	Fighting	Fighting	PROPN	NNP	Number=Sing	8	xcomp	8:xcomp	XML=</hi>
10	series	series	NOUN	NN	Number=Sing	4	nmod	4:nmod:in	Entity=173)
11	in	in	ADP	IN	_	12	case	12:case	_
12	April	April	PROPN	NNP	Number=Sing	4	nmod	4:nmod:in	Entity=(189-time-new-cf10-1-sgl|XML=<date when:::"2015-04">
13	2015	2015	NUM	CD	NumForm=Digit|NumType=Card	12	nmod:tmod	12:nmod:tmod	Entity=(175-time-giv:inact-cf5-1-coref)189)188)|SpaceAfter=No|XML=</date>
14	,	,	PUNCT	,	_	4	punct	4:punct	_
15	Padalecki	Padalecki	PROPN	NNP	Number=Sing	16	nsubj	16:nsubj	Entity=(1-person-giv:act-cf2*-1-coref-Jared_Padalecki)
16	partnered	partner	VERB	VBD	Mood=Ind|Number=Sing|Person=3|Tense=Past|VerbForm=Fin	0	root	0:root	_
17	with	with	ADP	IN	_	18	case	18:case	_
18	co-star	co-star	NOUN	NN	Number=Sing	16	obl	16:obl:with	Entity=(97-person-giv:inact-cf4-1,3-coref-Jensen_Ackles
19	Jensen	Jensen	PROPN	NNP	Number=Sing	18	appos	18:appos	XML=<ref target:::"https://en.wikipedia.org/wiki/Jensen_Ackles">
20	Ackles	Ackles	PROPN	NNP	Number=Sing	19	flat	19:flat	Entity=97)|XML=</ref>
21	to	to	PART	TO	_	22	mark	22:mark	Discourse=purpose-goal:105->104:0
22	release	release	VERB	VB	VerbForm=Inf	16	advcl	16:advcl:to	_
23	a	a	DET	DT	Definite=Ind|PronType=Art	24	det	24:det	Entity=(190-object-new-cf7-2-coref
24	shirt	shirt	NOUN	NN	Number=Sing	22	obj	22:obj	Entity=190)
25	featuring	feature	VERB	VBG	VerbForm=Ger	24	acl	24:acl	Discourse=elaboration-attribute:106->105:0
26	both	both	DET	DT	PronType=Art	25	obj	25:obj	Entity=(191-object-new-cf9-1-sgl
27	of	of	ADP	IN	_	29	case	29:case	_
28	their	their	PRON	PRP$	Case=Gen|Number=Plur|Person=3|Poss=Yes|PronType=Prs	29	nmod:poss	29:nmod:poss	Entity=(192-person-acc:aggr-cf1-1-coref)|SplitAnte=1<192,97<192
29	faces	face	NOUN	NNS	Number=Plur	26	nmod	26:nmod:of	Entity=191)|SpaceAfter=No
```

In addition, a list of the globally most salient entities in each document can be found in the metadata at the beginning of the document, for example:

```CoNLL-U
# meta::salientEntities = 1, 5, 6, 7, 8, 12, 98, 173, 180, 181, 182, 183, 184
```

Where the value `1` stands for Padalecki, as in the annotations above.

Possible values for the other annotations mentioned above are:

  * entity type: abstract, animal, event, object, organization, person, place, plant, substance, time
  * information status 
    * new - not previously mentioned
    * giv:act - mentioned no further than one sentence ago
    * giv:inact - mentioned earlier
    * acc:inf - accessible, inferable from some previous mention (e.g. the house... [the door]) 
    * acc:aggr - accessible, aggregate, i.e. split antecedent mediated by a set of previous mentions
    * acc:com - accessible, common ground, i.e. generic ([the world]) or situationally accessible ("pass [the salt]", first mention of "you" or "I")
  * centering: 
    * rank in the forward looking center (Cf), and a '*' for the top entity also mentioned in the previous sentence (Cb). The preferred forward looking center (Cp) is simply expressed as cf1. 
    * centering transition types are computed from these annotations in the sentence level `# transition` annotations
  * link: 
    * ana - pronominal anaphora (the dancers ... [they])
    * appos - apposition (Kim, [the lawyer])
    * cata - cataphora ("In [their] speech, the athletes said", or expletive cataphora: "[it] is easy [to dance]")
    * coref - lexical coreference (e.g. [Kim] ... [Kim])
    * disc - discourse deixis, non-NP, e.g. verbal antecedent as in "[Kim arrived] - [this] delighted the children
    * pred - predication, e.g. Kim is [a teacher] (but NOT definite identification: This is Kim)
    * sgl - singleton, not mentioned again in document
  * identity: any Wikipedia article title
  * minspan: a number or set of comma-separated numbers indicating indices of minimal head tokens within the span of the mention (first in span: 1, etc.)

For equivalent Wikidata identifiers for each Wikipedia article title, see [this file](https://github.com/amir-zeldes/gum/blob/master/coref/wiki_map.tab).

## Split antecedent and bridging

The annotations `SplitAnte` and `Bridge` mark non-strict identity anaphora (see the [Universal Anaphora](http://universalanaphora.org/) project for more details). For example, at token 28 in the example, the pronoun "their" refers back to two non-adjacent entities, requiring a split antecedent annotation. The value `SplitAnte=1<192,97<192` indicates that `192-person` (the pronoun "their") refers back to two previous Entity annotations, with pointers separatated by a comma: `1` (`1-person-...Jared_Padalecki`) and `97` (`97-person-...Jensen_Ackles`). 

Bridging anaphora is annotated when an entity has not been mentioned before, but is resolvable in context by way of a different entity: for example, token 2 has the annotation `Bridge=173<188`, which indicates that although `188-event` ("the second campaign...") has not been mentioned before, its identity is mediated by the previous mention of another entity, `173-abstract` (the project "Always Keep Fighting", mentioned earlier in the document, to which the campaign event belongs). In other words, readers can infer that "the second campaign" is part of the already introduced larger project, which also had a first campaign. This inference also leads to the information status label `acc:inf`, accessible-inferable.

## RST discourse trees

Discourse annotations are given in RST dependencies following the conversion from RST constituent trees as suggested by Li et al. (2014) - for the original RST constituent parses of GUM see the [source repo](https://github.com/amir-zeldes/gum/). At the beginning of each Elementary Discourse Unit (EDU), an annotation `Discourse` gives the discourse function of the unit beginning with that token, followed by a colon, the ID of the current unit, and an arrow pointing to the ID of the parent unit in the discourse parse. For instance, `Discourse=purpose-goal:105->104:0` at token 21 in the example below means that this token begins discourse unit 105, which functions as a `purpose-goal` to unit 104, which begins at token 1 in this sentence ("Padalecki partnered with co-star Jensen Ackles --purpose-goal-> to release a shirt..."). The final `:0` indicates that the attachment has a depth of 0, without an intervening span in the original RST constituent tree (this information allows deterministic reconstruction of the RST constituent discourse tree from the conllu file). The unique `ROOT` node of the discourse tree has no arrow notation, e.g. `Discourse=ROOT:2:0` means that this token begins unit 2, which is the Central Discourse Unit (or discourse root) of the current document. Although it is easiest to recover RST constituent trees from the source repo, it is also possible to generate them automatically from the dependencies with depth information, using the scripts in the [rst2dep repo](https://github.com/amir-zeldes/rst2dep/).

Discourse relations in GUM are defined based on the effect that W (a writer/speaker) has on R (a reader/hearer) by modifying a Nucleus discourse unit (N) with another discourse unit (a Satellite, S, or another N). Discourse relation units can precede their nuclei (satellite-nucleus, or SN relation), follow them (NS), or be coordinated with each other (NN or multinuclear relations). Relations are classified hierarchically into 15 major classes and include:

  * Adversative
    * adversative-antithesis (SN/NS) - R is meant to prefer N as an alternative to S
    * adversative-concession (SN/NS) - R is meant to look past an incompatibility of N with S
    * adversative-contrast (NN) - W presents multiple Ns as incompatible, but of equal prominence
  * Attribution
    * attribution-positive (SN/NS) - S states a source for the information in N
    * attribution-negative (SN/NS) - S states that a potential source is NOT a source of the information in N
  * Causal
    * causal-cause (SN/NS) - S is the cause of N (and N is more prominent)
    * causal-result (SN/NS) - S is the result of N (or: N is the cause of S, and N is more prominent)
  * Context
    * context-background (SN/NS) - S provides prerequisite information to increase R's understanding of N
    * context-circumstance (SN/NS) - S details circumstances (often spatio-temporal) under which N applies
  * Contingency
    * contingency-condition (SN/NS) - N occurs (or not) depending on S
  * Elaboration
    * elaboration-attribute (NS) - S gives additional information about a participant within N (not on the entire proposition in N)
    * elaboration-additional (NS) - S gives additional information about the proposition in N as a whole
  * Explanation
    * explanation-evidence (SN/NS) - S provides evidence which increases R's belief in N
    * explanation-justify (SN/NS) - S increases R's acceptance of W's right to say N
    * explanation-motivation (SN/NS) - S is meant to influence R's willingness to act according to N
  * Evaluation
    * evaluation-comment (SN/NS) - S provides an assessment of N by W (R does not have to share this assessment)
  * Joint
    * joint-disjunction (NN) - W presents multiple Ns which can be regarded as interchangeable alternatives
    * joint-list (NN) - W presents multiple Ns in parallel which are additive, of equal prominence, and of equivalent purpose
    * joint-sequence (NN) - Multiple Ns form a temporally ordered sequence of events presented in chronological order
    * joint-other (NN) - a collection of unlike Ns of equal prominence, but of disparate (non-equivalent) discourse purpose
  * Mode
    * mode-manner (SN/NS) - S indicates the manner in which N happens
    * mode-means (SN/NS) - S indicates the means by which N happens
  * Organization
    * organization-heading (SN) - S prepared R for N using an explicit text organizing device such as a heading
    * organization-phatic (SN/NS) - S prepares R for N by holding the floor for W, without contributing propositional content
    * organization-preparation (SN) - covers all other forms of S units primarily used to signal an upcoming N
  * Purpose
    * purpose-attribute (SN/NS) - S gives the purpose of a participant within N (not the entire propostion in N)
    * purpose-goal (SN/NS) - the proposition in N as a whole is initiated or exists in order to realize S
  * Restatement
    * restatement-partial (NS) - S partly realizes the same role and content as a previous N
    * restatement-repetition (NN) - Multiple Ns of equal prominence realize the same role and content
  * Topic
    * topic-question (SN) - S steers the discourse topic by posing a question to which N is the answer
    * topic-solutionhood (SN/NS) - S steers the discourse topic by posing a problem, to which N presents a solution
  * Same-unit (NN) - connects parts of a discontinuous discourse unit (this is not a discourse relation)

## XML

Markup from the original XML annotations using TEI tags is available in the XML MISC annotation, which indicates which XML tags, if any, were opened or closed before or after the current token, and in what order. In tokens 7-9 in the example above, the XML annotations indicate the words "Always Keep Fighting" were originally italicized using the tag pair `<hi rend="italic">...</hi>`, which opens at token 7 and closes after token 9. To avoid confusion with the `=` sign in MISC annotations, XML `=` signs are escaped and represented as `:::`.

```CoNLL-U
7	Always	Always	ADV	NNP	Number=Sing	8	advmod	8:advmod	XML=<hi rend:::"italic">
8	Keep	Keep	PROPN	NNP	Number=Sing	10	compound	10:compound	_
9	Fighting	Fighting	PROPN	NNP	Number=Sing	8	xcomp	8:xcomp	XML=</hi>
```

XML block tags spanning whole sentences (i.e. not beginning or ending mid sentence), such as paragraphs (`<p>`) or headings (`<head>`) are instead represented using the standard UD `# newpar_block` comment under the `# newpar` comment, which may however feature nested tags, for example:

```CoNLL-U
# newpar
# newpar_block = list type:::"unordered" (10 s) | item (4 s)
```

This comment indicates the opening of a `<list type="unordered">` block element, which spans 10 sentences (`(10 s)`). However, the list begins with a nested block, a list item (i.e. a bullet point), which spans 4 sentences, as indicated after the pipe separator. For documentation of XML elements in GUM, please see the [GUM wiki](https://wiki.gucorpling.org/gum/tei_markup_in_gum).

More information and additional annotation layers can also be found in the GUM [source repo](https://github.com/amir-zeldes/gum/).

# Metadata

Document metadata is given at the beginning of each new document in key-value pair comments beginning with the prefix `meta::`, as in:

```
# newdoc id = GUM_bio_padalecki
# global.Entity = GRP-etype-infstat-centering-minspan-link-identity
# meta::author = Wikipedia, The Free Encyclopedia
# meta::dateCollected = 2019-09-10
# meta::dateCreated = 2004-08-14
# meta::dateModified = 2019-09-11
# meta::genre = bio
# meta::salientEntities = 1, 5, 6, 7, 8, 12, 98, 173, 180, 181, 182, 183, 184
# meta::sourceURL = https://en.wikipedia.org/wiki/Jared_Padalecki
# meta::speakerCount = 0
# meta::summary = Jared Padalecki is an award winning American actor who gained prominence in the series Gilmore Girls, best known for playing the role of Sam Winchester in the TV series Supernatural, and for his active role in campaigns to support people struggling with depression, addiction, suicide and self-harm.
# meta::title = Jared Padalecki
```

Document summaries are included in the metadata `summary` annotation and follow strict guidelines described [here](https://wiki.gucorpling.org/gum/summarization).

# Documents and splits

The training, development and test sets contain complete, contiguous documents, balanced for genre. Test and dev contain similar amounts of data, usually around 1,800 tokens in each genre in each, and the rest is assigned to training. For the exact file lists in each split see:

https://github.com/UniversalDependencies/UD_English-GUM/tree/master/not-to-release/file-lists

# Acknowledgments

GUM annotation team (so far - thanks for participating!)

Adrienne Isaac, Akitaka Yamada, Alex Giorgioni, Alexandra Berends, Alexandra Slome, Amani Aloufi, Amber Hall, Amelia Becker, Andrea Price, Andrew O'Brien, Anna Runova, Anne Butler, Arianna Janoff, Aryaman Arora, Ayan Mandal, Aysenur Sagdic, Bertille Baron, Bradford Salen, Brandon Tullock, Brent Laing, Candice Penelton, Charlie Dees, Chenyue Guo, Colleen Diamond, Connor O'Dwyer, Cristina Lopez, Dan Simonson, Derek Reagan, Didem Ikizoglu, Edwin Ko, Emile Zahr, Emily Pace, Emma Manning, Ethan Beaman, Felipe De Jesus, Han Bu, Hana Altalhi, Hang Jiang, Hannah Wingett, Hanwool Choe, Hassan Munshi, Helen Dominic, Ho Fai Cheng, Hortensia Gutierrez, Jakob Prange, James Maguire, Janine Karo, Jehan al-Mahmoud, Jemm Excelle Dela Cruz, Jessica Cusi, Jessica Kotfila, Joaquin Gris Roca, John Chi, Jongbong Lee, Juliet May, Jungyoon Koh, Katarina Starcevic, Katelyn MacDougald, Katherine Vadella, Khalid Alharbi, Lara Bryfonski, Lauren Levine, Leah Northington, Lindley Winchester, Linxi Zhang, Siyao Peng, Lucia Donatelli, Luke Gessler, Mackenzie Gong, Margaret Anne Rowe, Margaret Borowczyk, Maria Stoianova, Mariko Uno, Mary Henderson, Maya Barzilai, Md. Jahurul Islam, Michael Kranzlein, Michaela Harrington, Minnie Annan, Mitchell Abrams, Mohammad Ali Yektaie, Naomee-Minh Nguyen, Negar Siyari, Nicholas Mararac, Nicholas Workman, Nicole Steinberg, Nitin Venkateswaran, Phoebe Fisher, Rachel Thorson, Rebecca Childress, Rebecca Farkas, Riley Breslin Amalfitano, Rima Elabdali, Robert Maloney, Ruizhong Li, Ryan Mannion, Ryan Murphy, Sakol Suethanapornkul, Sarah Bellavance, Sasha Slone, Sean Macavaney, Sean Simpson, Seyma Toker, Shane Quinn, Shannon Mooney, Shelby Lake, Shira Wein, Sichang Tu, Siddharth Singh, Siyu Liang, Stephanie Kramer, Sylvia Sierra, Talal Alharbi, Tatsuya Aoyama, Timothy Ingrassia, Trevor Adriaanse, Ulie Xu, Wai Ching Leung, Wenxi Yang, Xiaopei Wu, Yang Liu, Yi-Ju Lin, Yifu Mu, Yilun Zhu, Yingzhu Chen, Yiran Xu, Young-A Son, Yu-Tzu Chang, Yuhang Hu, Yunjung Ku, Yushi Zhao, Zhuosi Luo, Zhuxin Wang, Amir Zeldes

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

* 2023-02-02
  * Added GUM V9 documents (train only)
  * Added document summaries to metadata
  * Added salient entity metadata

* 2022-10-21
  * Added new subtypes advcl:relcl and nsubj:outer
  * Many updates to UPOS and FEATS consistency with EWT

* 2022-04-29
  * Added Centering Theory annotations

* 2022-01-31
  * Revised RST discourse relations (now 32 labels + ROOT)

* 2022-01-09
  * Added GUM V8 documents

* 2021-12-14
  * Corrections incl. bug fix for escaping wikification identifiers containing hyphens
  * Added more exhaustive PronType annotations

* 2021-10-31
  * Add annotated newpar comments representing possibly nesting blocks
  * Add XML MISC attribute for XML markup in source data which does not correspond to paragraph blocks
  * Shorten Entity mention span closers in MISC
  * Add information status and coref type annotations to spans incl. discourse deixis, predicatives, singletons etc.
  * Add MIN IDs for fuzzy coref matching scores (mostly NP heads, but more for coordinations and proper names)

* 2021-09-23
  * split hyphenated tokens to match EWT tokenization, added `HYPH` xpos tag
  * added tree depth information in discourse dependencies, allowing reconstruction of RST constituents
  * added `_m` suffix to multinuclear discourse dependencies (distinguishes multinuclear and satellite restatements)

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
