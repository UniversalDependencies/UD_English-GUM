# Summary

Universal Dependencies syntax annotations from the GUM corpus (https://gucorpling.org/gum/)

# Introduction

GUM, the Georgetown University Multilayer corpus, is an open source collection of richly annotated texts from multiple text types. The corpus is collected and expanded by students as part of the curriculum in the course LING-4427 "Computational Corpus Linguistics" at Georgetown University. The selection of text types is meant to represent different communicative purposes, while coming from sources that are readily and openly available (usually Creative Commons licenses), so that new texts can be annotated and published with ease.

The dependencies in the corpus up to GUM version 5 were originally annotated using Stanford Typed Depenencies (de Marneffe & Manning 2013) and converted automatically to UD using DepEdit (https://gucorpling.org/depedit/). The rule-based conversion took into account gold annotations found in other annotation layers of the GUM corpus (e.g. entity annotations), and has since been corrected manually in native UD. The original conversion script used can found in the GUM build bot code from version 5, available from the (non-UD) GUM repository. Documents from version 6 of GUM onwards were annotated directly in UD, and subsequent manual error correction to all GUM data has also been done directly using the UD guidelines. Enhanced dependencies were added semi-automatically from version 7.1 of the corpus. For more details see the [corpus website](https://gucorpling.org/gum/).

# Additional annotations in MISC

The MISC column contains **morphological segmentation, Construction Grammar, entity, coreference, information status, Wikification and discourse** annotations from the full corpus, encoded using the annotations `MSeg`, `Cxn`, `Entity`, `SplitAnte`, `Bridge` and `Discourse`. 

## MSeg

Morphological segmentation is annotated in the MISC field `MSeg` attribute semi-automatically using the [Unimorph](https://unimorph.github.io/) lexical resource (Kirov et al. 2018), specifically using scripts based on the lexicon data [here](https://github.com/unimorph/eng). Analyses are concatenative, using hyphens as separators, and are guaranteed to sum up to the string of each token with only hyphens added. Existing hyphens in a word form are retained and assumed to be meaningful. Analyses cover inflection, derivation and compounding. For example:

  * books -> book-s
  * explanation -> explan-ation
  * baseball -> base-ball
  * e-mail -> e-mail (hyphen is retained, presumably meaningful)
  
Note that stems are retained in their orthographic forms (explanation does not become explain+ation), and 'etymological affixation' in loanwords is not necessarily analyzed (e.g. "ex" is not split off since the corresponding affixation process is no longer interpretable in English). For more information and updates to the segmentation guidelines see the [GUM wiki](https://wiki.gucorpling.org/gum/tokenization_segmentation#morphological-segmentation-mseg).

## Cxn

We use the MISC field `Cxn` annotation to distinguish some complex constructions in a Construction Grammar (CxG) framework developed by collaborators from [Dagstuhl Seminar 23191](https://www.dagstuhl.de/en/seminars/seminar-calendar/seminar-details/23191) for the integration of CxG analyses into UD trees. Construction labels are always attached to the highest token belonging to the necessary or defining elements of the construction, and carry hierarchical designations, such as a prefix `Cxn=Conditional` for all conditional constructions, but a more specific `Cxn=UnspecifiedEpistemic-Reduced` for reduced conditionals (the type seen in "if possible"). Individual elements of a construction are annotated using the `CxnElt` MISC annotation. Currently covered constructions are listed in the [GUM wiki](https://wiki.gucorpling.org/gum/cxn). For more information and for work using these annotations, please refer to [Weissweiler et al. 2024](https://aclanthology.org/2024.lrec-main.1471).

## Entity

The `Entity` annotation uses the CoNLL 2012 shared task bracketing format, which identifies potentially coreferring entities using round opening and closing brackets as well as a unique ID per entity, repeated across mentions. In the following example, actor Jared Padalecki appears in a single token mention, labeled `(1-person-giv:act-sssss-cf2*-1-coref-Jared_Padalecki)` indicating the entity type (`person`) combined with the unique ID of all mentions of Padalecki in the text (`1-person`). Because Padalecki is a named entity with a corresponding Wikipedia page, the Wikification identifier corresponding to his Wikipedia page is given after the last hyphen (`1-person-Jared_Padalecki`). We can also see an information status annotation (`giv:act`, indicating an aforementioned or 'given' entity, actively mentioned last no farther than the previous sentence; see Dipper et al. 2007), and a summarization-based salience annotation, which indicates which of five summaries mention this entity. The value `sssss` means that all five summaries of this document mention Padalecki, placing him in the most salient rank (a salience score of 5); if a summary does not mention the entity, a corresponding `n` will appear in that position - for example Padalecki's co-start Jensen Ackles is not mentioned in any summary and has the value `nnnnn`. Centering Theory annotations are also available (`cf2*`, indicating he is the second most central entity in the sentence moving forward, and that he was mentioned in the previous sentence, indicated by the `*`), as well as minimum token ID information indicating the head tokens for fuzzy matching (in this case `1`, the first and only token  in this span) and the coreference type `coref`, indicating lexical subsequent mention. 

The labels for each part of the hyphen-separated annotation are given at the top of each document in a comment `# global.Entity = GRP-etype-infstat-salience-centering-minspan-link-identity`, indicating that these annotations consist of the entity group id (i.e the coreference group), entity type, information status, salience, centering theory annotation, minimal span of tokens for head matching, the coreference link type, and named entity identity (if available). 

Multi-token mentions receive opening brackets on the line in which they open, such as `(97-person-giv:inact-nnnnn-cf4-1,3-coref-Jensen_Ackles`, and a closing annotation `97)` at the token on which they end. Multiple annotations are possible for one token, corresponding to nested entities, e.g. `(175-time-giv:inact-nnnnn-cf5-1-coref)189)188)` below corresponds to the single token and last token of the time entities "2015" and "April 2015" respectively, as well as the last token of the larger "the second campaign in the Always Keep Fighting series in April 2015". 

```CoNLL-U
# global.Entity = GRP-etype-infstat-salience-centering-minspan-link-identity
...
1	For	for	ADP	IN	_	4	case	4:case	Discourse=joint-sequence_m:104->98:2:lex-indph-954-955
2	the	the	DET	DT	Definite=Def|PronType=Art	4	det	4:det	Bridge=173<188|Entity=(188-event-acc:inf-nnnnn-cf6-3,6,8-sgl
3	second	second	ADJ	JJ	Degree=Pos|NumForm=Word|NumType=Ord	4	amod	4:amod	_
4	campaign	campaign	NOUN	NN	Number=Sing	16	obl	16:obl:for	_
5	in	in	ADP	IN	_	10	case	10:case	_
6	the	the	DET	DT	Definite=Def|PronType=Art	10	det	10:det	Entity=(173-abstract-giv:inact-sssnn-cf3-2,4,5-coref
7	Always	Always	ADV	NNP	_	8	advmod	8:advmod	MSeg=Al-way-s|XML=<hi rend:::"italic">
8	Keep	Keep	VERB	NNP	Mood=Imp|Person=2|VerbForm=Fin	10	compound	10:compound	_
9	Fighting	Fighting	VERB	NNP	VerbForm=Ger	8	xcomp	8:xcomp	MSeg=Fight-ing|XML=</hi>
10	series	series	NOUN	NN	Number=Sing	4	nmod	4:nmod:in	Entity=173)
11	in	in	ADP	IN	_	12	case	12:case	_
12	April	April	PROPN	NNP	Number=Sing	4	nmod	4:nmod:in	Entity=(189-time-new-nnnnn-cf10-1-sgl|XML=<date when:::"2015-04">
13	2015	2015	NUM	CD	NumForm=Digit|NumType=Card	12	nmod:unmarked	12:nmod:unmarked	Entity=(175-time-giv:inact-nnnnn-cf5-1-coref)189)188)|SpaceAfter=No|XML=</date>
14	,	,	PUNCT	,	_	4	punct	4:punct	_
15	Padalecki	Padalecki	PROPN	NNP	Number=Sing	16	nsubj	16:nsubj	Entity=(1-person-giv:act-sssss-cf2*-1-coref-Jared_Padalecki)
16	partnered	partner	VERB	VBD	Mood=Ind|Number=Sing|Person=3|Tense=Past|VerbForm=Fin	0	root	0:root	MSeg=partner-ed
17	with	with	ADP	IN	_	18	case	18:case	_
18	co-star	co-star	NOUN	NN	Number=Sing	16	obl	16:obl:with	Entity=(97-person-giv:inact-nnnnn-cf4-1,3-coref-Jensen_Ackles|MSeg=co-star
19	Jensen	Jensen	PROPN	NNP	Number=Sing	18	appos	18:appos	XML=<ref target:::"https://en.wikipedia.org/wiki/Jensen_Ackles">
20	Ackles	Ackles	PROPN	NNP	Number=Sing	19	flat	19:flat	Entity=97)|XML=</ref>
21	to	to	PART	TO	_	22	mark	22:mark	Discourse=purpose-goal:105->104:0:syn-inf-963|PDTB=Implicit:Contingency.Purpose.Arg2-as-goal:in order:_:943-962:963-981
22	release	release	VERB	VB	VerbForm=Inf	16	advcl	16:advcl:to	_
23	a	a	DET	DT	Definite=Ind|PronType=Art	24	det	24:det	Entity=(190-object-new-nnnnn-cf7-2-coref
24	shirt	shirt	NOUN	NN	Number=Sing	22	obj	22:obj	Entity=190)
25	featuring	feature	VERB	VBG	VerbForm=Ger	24	acl	24:acl	Discourse=elaboration-attribute:106->105:0:syn-mdf-966+syn-nmn-967|MSeg=featur-ing
26	both	both	DET	DT	PronType=Tot	25	obj	25:obj	Entity=(191-object-new-nnnnn-cf9-1-sgl
27	of	of	ADP	IN	_	29	case	29:case	_
28	their	their	PRON	PRP$	Case=Gen|Number=Plur|Person=3|Poss=Yes|PronType=Prs	29	nmod:poss	29:nmod:poss	Entity=(192-person-acc:aggr-nnnnn-cf1-1-coref)|SplitAnte=1<192,97<192
29	faces	face	NOUN	NNS	Number=Plur	26	nmod	26:nmod:of	Entity=191)|MSeg=face-s|SpaceAfter=No
```

In addition, a list of the globally most salient entities in each document can be found in the metadata at the beginning of the document, along with a salience score from 1-5, for example:

```CoNLL-U
# meta::salientEntities = 1 (5*), 7 (5*), 12 (5*), 6 (4*), 5 (3*), 173 (3*), 8 (2*), 11 (2), 42 (2), 181 (2*), 9 (1), 10 (1), 16 (1), 41 (1), 56 (1), 98 (1*), 132 (1), 134 (1), 165 (1), 166 (1), 180 (1*), 182 (1*), 183 (1*), 184 (1*), 186 (1)
```

Where the value `1` stands for Padalecki, as in the annotations above, and his score, 5, appears in brackets. Entities which are mentioned in the canonical reference summary for the document, `summary1`, also receive a star after the score, and these correspond to binary salience annotations in older version of the corpus. For example, both entities 8 and 11 have a score of `2`, but only entity 8 is mentioned in the reference summary, giving it the label `(2*)`.

Possible values for the other annotations mentioned above are:

  * entity type: abstract, animal, event, object, organization, person, place, plant, substance, time
  * information status 
    * new - not previously mentioned
    * giv:act - mentioned no further than one sentence ago
    * giv:inact - mentioned earlier
    * acc:inf - accessible, inferable from some previous mention (e.g. the house... [the door]) 
    * acc:aggr - accessible, aggregate, i.e. split antecedent mediated by a set of previous mentions
    * acc:com - accessible, common ground, i.e. generic ([the world]) or situationally accessible ("pass [the salt]", first mention of "you" or "I")
  * salience:
    * any 5 character string consisting of occurrences of n or s
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

## Enhanced RST discourse trees and signals

Discourse annotations are given in [eRST](https://wiki.gucorpling.org/en/gum/rst) dependencies following the conversion from RST constituent trees as suggested by Li et al. (2014) - for the original RST constituent parses see the [source repo](https://github.com/amir-zeldes/gum/). At the beginning of each Elementary Discourse Unit (EDU), an annotation `Discourse` gives the discourse function of the unit beginning with that token, followed by a colon, the ID of the current unit, and an arrow pointing to the ID of the parent unit in the discourse parse. For instance, `Discourse=purpose-goal:105->104:0:syn-inf-963` at token 21 in the example below means that this token begins discourse unit 105, which functions as a `purpose-goal` to unit 104, which begins at token 1 in this sentence ("Padalecki partnered with co-star Jensen Ackles --purpose-goal-> to release a shirt..."). The third number `:0` indicates that the attachment has a depth of 0, without an intervening span in the original RST constituent tree (this information allows deterministic reconstruction of the RST constituent discourse tree from the conllu file). The final part of the `Discourse` annotation indicates categorized signals which correspond to the discourse relation in question, as defined by eRST - in this case, `syn-inf-963` indicates a syntactic signal (`syn`) of the subtype "infinitival_clause" (`inf`), since the purpose relation is signaled by the use of an infinitive, a typical strategy in English. The index `963` refers to the position of the signal, in this case token number 963 in the document (excluding empty nodes), the infinitive 'to' (token 21 in the sentence). Multiple signals are separated by `+`. See below for the inventory of signal types.

Additionally, note that multiple discourse relations can sometimes occur on the same line, since eRST allows multiple concurrent and tree-breaking relations to be identified. In such cases the multiple relation entries will be separated by `;` and ordered such that the primary relation (which indicates RST nuclearity and is guaranteed to be projective in the discourse tree) will be serialized first, and non-projective secondary relations are guaranteed to be serialized subsequently. The unique `ROOT` node of the discourse tree has no arrow notation, e.g. `Discourse=ROOT:2:0` means that this token begins unit 2, which is the Central Discourse Unit (or discourse root) of the current document. Although it is easiest to recover RST constituent trees from the source repo, it is also possible to generate them automatically from the dependencies with depth information, using the scripts in the [rst2dep repo](https://github.com/amir-zeldes/rst2dep/).

Discourse relations are defined based on the effect that W (a writer/speaker) has on R (a reader/hearer) by modifying a Nucleus discourse unit (N) with another discourse unit (a Satellite, S, or another N). Discourse relation units can precede their nuclei (satellite-nucleus, or SN relation), follow them (NS), or be coordinated with each other (NN or multinuclear relations). Relations are classified hierarchically into 15 major classes and include:

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

Relation signals fall into nine major classes, most with several subtypes each, and include:

  * dm: discourse markers of primary relations ('but', 'additionally', 'on the other hand'...)
  * orphan (orp): discourse markers of secondary relations
  * graphical (grf): colon (col), dash (dsh), items_in_sequence (seq), layout (ly), parentheses (prn), quotation_marks (qt), question_mark (qst), semicolon (semcol)
  * lexical (lex): alternate_expression (altlex), indicative_phrase (indph), indicative_word (indwd)
  * morphological (mrf): mood (md), tense (tns)
  * numerical (num): same_count (count)
  * reference (ref): comparative_reference (cmp), demonstrative_reference (dem), general_word (gnrl), personal_reference (prs), propositional_reference (prop)
  * semantic (sem): antonymy (antnm), attribution_source (atsrc), lexical_chain (lxchn), meronymy (mrnym), negation (ngt), repetition (rpt), synonymy (synym)
  * syntactic (syn): subject_auxiliary_inversion (sbinv), infinitival_clause (inf), interrupted_matrix_clause (intrp), modified_head (mdf), nominal_modifier (nmn), parallel_syntactic_construction (prl), past_participial_clause (pst), present_participial_clause (pres), relative_clause (relcl), reported_speech (rpr)

## PDTB shallow discourse relations

With the publication of the GUM Discourse Treebank (GDTB), a shallow version of discourse relation annotations is now included in the `PDTB` key in the MISC field, which provides information for all Explicit, Implicit, AltLex, AltLexC, EntRel, Hypophora and NoRel annotations following the Penn Discourse Treebank (PDTB) v3 guidelines. Annotations are placed on the first token of the connective or alternative lexicalization marking the relation for explicit/altlex relations, or on the first token of the second argument span (arg2) for other cases. Token ranges for each argument span, the connective and relation label are provided as well. For example, the line in the excerpt above:

```CoNLL-U
21	to	to	PART	TO	_	22	mark	22:mark	Discourse=purpose-goal:105->104:0:syn-inf-963|PDTB=Implicit:Contingency.Purpose.Arg2-as-goal:in order:_:943-962:963-981
```

Indicates an Implicit relation with the label `Contingency.Purpose.Arg2-as-goal`, with an implicit connective "in order". Because the connective is implicit, it has no token indices (`_`), but arg1 spans token`943-962` of the document (ignoring decimal ellipsis tokens), and arg2 spans tokens `963-981`. If multiple PDTB relations apply at the same token position, they are separated by a semicolon.

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

This comment indicates the opening of a `<list type="unordered">` block element, which spans 10 sentences (`(10 s)`). However, the list begins with a nested block, a list item (i.e. a bullet point), which spans 4 sentences, as indicated after the pipe separator. For documentation of XML elements in the GUM annotation scheme, please see the [GUM wiki](https://wiki.gucorpling.org/gum/tei_markup_in_gum).

More information and additional annotation layers can also be found in the [source repo](https://github.com/amir-zeldes/gum/).

# Metadata

Document metadata is given at the beginning of each new document in key-value pair comments beginning with the prefix `meta::`, as in:

```CoNLL-U
# newdoc id = GUM_bio_padalecki
# global.Entity = GRP-etype-infstat-salience-centering-minspan-link-identity
# meta::author = Wikipedia, The Free Encyclopedia
# meta::dateCollected = 2019-09-10
# meta::dateCreated = 2004-08-14
# meta::dateModified = 2019-09-11
# meta::genre = bio
# meta::salientEntities = 1 (5*), 7 (5*), 12 (5*), 6 (4*), 5 (3*), 173 (3*), 8 (2*), 11 (2), 42 (2), 181 (2*), 9 (1), 10 (1), 16 (1), 41 (1), 56 (1), 98 (1*), 132 (1), 134 (1), 165 (1), 166 (1), 180 (1*), 182 (1*), 183 (1*), 184 (1*), 186 (1)
# meta::sourceURL = https://en.wikipedia.org/wiki/Jared_Padalecki
# meta::speakerCount = 0
# meta::summary1 = (human1) Jared Padalecki is an award winning American actor who gained prominence in the series Gilmore Girls, best known for playing the role of Sam Winchester in the TV series Supernatural, and for his active role in campaigns to support people struggling with depression, addiction, suicide and self-harm.
# meta::summary2 = (claude-3-5-sonnet-20241022; postedited) Jared Padalecki's career highlights run the gamut from starring in Gilmore Girls and films like House of Wax to his long-running role as Sam Winchester on Supernatural, while his personal life includes marriage to co-star Genevieve Cortese and mental health advocacy through the Always Keep Fighting campaign.
# meta::summary3 = (gpt4o; postedited) Jared Padalecki, an American actor living in Austin, Texas, with his wife and three children, became known for playing Sam Winchester in “Supernatural” and rose to fame in the early 2000s through “Gilmore Girls,” as well as launching successful charity campaigns with his Always Keep Fighting initiative after his own battle with depression.
# meta::summary4 = (Llama-3.2-3B-Instruct) Jared Padalecki is an American actor best known for playing the role of Sam Winchester in the TV series Supernatural, which he has been starring in since 2005.
# meta::summary5 = (Qwen2.5-7B-Instruct) American actor Jared Padalecki, known for his roles in Gilmore Girls and Supernatural, has had a successful acting career since the early 2000s and is openly supportive of mental health initiatives.
# meta::title = Jared Padalecki
```

Document summaries are included in the metadata `summary` annotation and follow strict guidelines described [here](https://wiki.gucorpling.org/gum/summarization). For some documents, up to five human written summaries are available and notated with `(human<N>)`. For other documents, additional model generated summaries as added and the source model is noted. In cases where model summaries deviated from the guidelines, human corrections are made available, in which case the model name is suffixed with `; postedited`. For example above, a summary by a Claude model contained an error, and the postedited human corrected version is labeled as `(claude-3-5-sonnet-20241022; postedited)`.

Additionally, sentences carry some sentence-level annotations in CoNLL-U comment annotations, such as [sentence types](https://wiki.gucorpling.org/gum/tokenization_segmentation#sentence-annotation) in `s_type` (declarative, imperative, wh-question, fragment, etc.), as well as sentence transition types based on Centering Theory and sentence prominence levels based on graph proximity to the discourse parse root. For example, this fragment sentence (`frag`) establishes a new backwards looking Center (`establishment`) and is a level-2 sentence (`s_prominence = 2`, i.e. its discourse nesting level is one further than a sentence containing the level-1 Central Discourse Unit of the entire text.

```CoNLL-U
# s_prominence = 2
# s_type = frag
# transition = establishment
# text = Jared Padalecki
1	Jared	Jared	PROPN	NNP	Number=Sing	0	root	0:root	MSeg=Jared
2	Padalecki	Padalecki	PROPN	NNP	Number=Sing	1	flat	1:flat	_
```

# Documents and splits

The training, development and test sets contain complete, contiguous documents, balanced for genre. Test and dev contain similar amounts of data, usually around 1,800 tokens in each genre in each, and the rest is assigned to training. A second, out-of-domain test split (test2) is made available in the form of the GENTLE corpus. For the exact document lists in each split including all genres see:

https://github.com/amir-zeldes/gum/blob/master/splits.md

# Acknowledgments

GUM annotation team (so far - thanks for participating!)

Abhishek Purushothama, Adrienne Isaac, Akitaka Yamada, Alex Giorgioni, Alexandra Berends, Alexandra Slome, Amani Aloufi, Amber Hall, Amelia Becker, Andrea Price, Andrew O'Brien, Ángeles Ortega Luque, Aniya Harris, Anna Prince, Anna Runova, Anne Butler, Arianna Janoff, Aryaman Arora, Ayşenur Sağdiç, Ayan Mandal, Bertille Baron, Bielasan Zaina, Bradford Salen, Brandon Tullock, Brent Laing, Caitlyn Pineault, Calvin Engstrom, Candice Penelton, Carlotta Hübener, Caroline Gish, Charlie Dees, Chenyue Guo, Chloe Evered, Cindy Luo, Colleen Diamond, Connor O'Dwyer, Cristina Lopez, Cynthia Li, Dan DeGenaro, Dan Simonson, Derek Reagan, Devika Tiwari, Diana Robson, Didem Ikizoglu, Edwin Ko, Eliza Rice, Emile Zahr, Emily Pace, Emma Manning, Emma Rafkin, Ethan Beaman, Felipe De Jesus, Han Bu, Hana Altalhi, Hang Jiang, Hannah Wingett, Hanwool Choe, Hassan Munshi, Helen Dominic, Ho Fai Cheng, Hortensia Gutierrez, Hyun Min, Jakob Prange, James Maguire, Janine Karo, Jehan al-Mahmoud, Jemm Excelle Dela Cruz, Jess Godes, Jessica Cusi, Jessica Kotfila, Jingni Wu, Joaquin Gris Roca, John Chi, Jongbong Lee, Juliet May, Jungyoon Koh, Katarina Starcevic, Katelyn Carroll, Katelyn MacDougald, Katherine Vadella, Khalid Alharbi, Kristen Cook, Kushaan Vardhan, Lanni Bu, Lara Bryfonski, Lauren Levine, Leah Northington, Lillian Ehrhart, Lindley Winchester, Linxi Zhang, Lucia Donatelli, Luke Gessler, Mackenzie Gong, Margaret Anne Rowe, Margaret Borowczyk, Maria Laura Zalazar, Maria Stoianova, Mariko Uno, Mary Henderson, Maya Barzilai, Md. Jahurul Islam, Micaela Wells, Michael Kranzlein, Michaela Harrington, Mikayla Campbell, Mingyeong Choi, Minnie Annan, Mitchell Abrams, Mohammad Ali Yektaie, Naomee-Minh Nguyen, Negar Siyari, Nicholas Mararac, Nicholas Workman, Nicole Steinberg, Nitin Venkateswaran, Parker DiPaolo, Phoebe Fisher, Rachel Kerr, Rachel Thorson, Rebecca Childress, Rebecca Farkas, Riley Breslin Amalfitano, Rima Elabdali, Robert Maloney, Ruizhong Li, Ryan Mannion, Ryan Murphy, Sakol Suethanapornkul, Sarah Bellavance, Sarah Carlson, Sasha Slone, Saurav Goswami, Sean Macavaney, Sean Simpson, Seyma Toker, Shane Quinn, Shannon Mooney, Shelby Lake, Shira Wein, Sichang Tu, Siddharth Singh, Siona Ely, Siyao Peng, Siyu Liang, Stephanie Kramer, Sylvia Sierra, Talal Alharbi, Tatsuya Aoyama, Tess Feyen, Timothy Ingrassia, Trevor Adriaanse, Ulie Xu, Wai Ching Leung, Wenxi Yang, Wesley Scivetti, Xiaopei Wu, Xiulin Yang, Yang Liu, Yi-Ju Lin, Yifu Mu, Yilun Zhu, Yingzhu Chen, Yiran Xu, Young-A Son, Yu-Tzu Chang, Yuhang Hu, Yunjung Ku, Yushi Zhao, Zhijie Song, Zhuosi Luo, Zhuxin Wang, Amir Zeldes

... and other annotators who wish to remain anonymous!

## References

The best paper to cite depends on the data you are using. To cite the corpus in general, please refer to the following article (but note that the corpus has changed and grown a lot in the time since); otherwise see different citations for specific aspects below:

Zeldes, Amir (2017) "The GUM Corpus: Creating Multilayer Resources in the Classroom". Language Resources and Evaluation 51(3), 581–612. 

```bibtex
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

If you are using the **Reddit** subset of GUM in particular, please use this citation instead:

* Behzad, Shabnam and Zeldes, Amir (2020) "A Cross-Genre Ensemble Approach to Robust Reddit Part of Speech Tagging". In: Proceedings of the 12th Web as Corpus Workshop (WAC-XII).

```bibtex
@InProceedings{BehzadZeldes2020,
  author    = {Shabnam Behzad and Amir Zeldes},
  title     = {A Cross-Genre Ensemble Approach to Robust {R}eddit Part of Speech Tagging},
  booktitle = {Proceedings of the 12th Web as Corpus Workshop (WAC-XII)},
  pages     = {50--56},
  year      = {2020},
}
```

For papers focusing on the discourse relations, discourse markers or other discourse signal annotations, please cite [the eRST paper](https://aclanthology.org/2025.cl-1.3/):

```bibtex
@article{zeldes-etal-2025-erst,
    title = "e{RST}: A Signaled Graph Theory of Discourse Relations and Organization",
    author = "Zeldes, Amir  and
      Aoyama, Tatsuya  and
      Liu, Yang Janet  and
      Peng, Siyao  and
      Das, Debopam  and
      Gessler, Luke",
    journal = "Computational Linguistics",
    volume = "51",
    number = "1",
    year = "2025",
    address = "Cambridge, MA",
    publisher = "MIT Press",
    url = "https://aclanthology.org/2025.cl-1.3/",
    doi = "10.1162/coli_a_00538",
    pages = "23--72"
}
```

For papers using GDTB/PDTB style shallow discourse relations, please cite:

  * Yang Janet Liu, Tatsuya Aoyama, Wesley Scivetti, Yilun Zhu, Shabnam Behzad, Lauren Elizabeth Levine, Jessica Lin, Devika Tiwari, and Amir Zeldes (2024), "GDTB: Genre Diverse Data for English Shallow Discourse Parsing across Modalities, Text Types, and Domains". In: Proceedings of the 2024 Conference on Empirical Methods in Natural Language Processing. Association for Computational Linguistics: Miami, USA.

```bibtex
@inproceedings{liu-etal-2024-gdtb,
    title = "{GDTB}: Genre Diverse Data for {E}nglish Shallow Discourse Parsing across Modalities, Text Types, and Domains",
    author = "Liu, Yang Janet  and
      Aoyama, Tatsuya  and
      Scivetti, Wesley  and
      Zhu, Yilun  and
      Behzad, Shabnam  and
      Levine, Lauren Elizabeth  and
      Lin, Jessica  and
      Tiwari, Devika  and
      Zeldes, Amir",
    editor = "Al-Onaizan, Yaser  and
      Bansal, Mohit  and
      Chen, Yun-Nung",
    booktitle = "Proceedings of the 2024 Conference on Empirical Methods in Natural Language Processing",
    month = nov,
    year = "2024",
    address = "Miami, Florida, USA",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2024.emnlp-main.684/",
    doi = "10.18653/v1/2024.emnlp-main.684",
    pages = "12287--12303"
}
```

If you are using the OntoNotes schema version of the coreference annotations (a.k.a. OntoGUM data in `coref/ontogum/`), please cite this paper instead:

```bibtex
@InProceedings{ZhuEtAl2021,
  author    = {Yilun Zhu and Sameer Pradhan and Amir Zeldes},
  booktitle = {Proceedings of ACL-IJCNLP 2021},
  title     = {{OntoGUM}: Evaluating Contextualized {SOTA} Coreference Resolution on 12 More Genres},
  year      = {2021},
  pages     = {461--467},
  address   = {Bangkok, Thailand}
```

For papers focusing on named entities or entity linking (Wikification), please cite this paper instead:

```bibtex
@inproceedings{lin-zeldes-2021-wikigum,
    title = {{W}iki{GUM}: Exhaustive Entity Linking for Wikification in 12 Genres},
    author = {Jessica Lin and Amir Zeldes},
    booktitle = {Proceedings of The Joint 15th Linguistic Annotation Workshop (LAW) and 
                 3rd Designing Meaning Representations (DMR) Workshop (LAW-DMR 2021)},
    year = {2021},
    address = {Punta Cana, Dominican Republic},
    url = {https://aclanthology.org/2021.law-1.18},
    pages = {170--175},
}
```
For papers focusing on the salience annotations, please cite this paper instead:

```bibtex
@inproceedings{lin-zeldes-2024-gumsley,
    title = "{GUM}sley: Evaluating Entity Salience in Summarization for 12 {E}nglish Genres",
    author = "Lin, Jessica  and
      Zeldes, Amir",
    editor = "Graham, Yvette  and
      Purver, Matthew",
    booktitle = "Proceedings of the 18th Conference of the European Chapter of the Association for Computational Linguistics (Volume 1: Long Papers)",
    year = "2024",
    address = "St. Julian{'}s, Malta",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2024.eacl-long.158/",
    pages = "2575--2588"
}
```

# Changelog

* 2025-03-13
  * Added GUM V11 documents
  * Added 5 summaries per document
  * Added graded salience annotations
  * New dependency subtype nmod:desc for titles etc.

* 2024-10-29
  * Added PDTB-style shallow discourse relations from GDTB in MISC
  * Added CxnElt in MISC
  * Moved Polarity=Neg of negative morphological derviations to MISC Negation=Yes
  * Added ExtPos to fixed expressions in FEATS
  * Renamed :npmod and :tmod relation subtypes to :unmarked

* 2024-02-15
  * Added GUM V10 documents (four new genres: court, essay, letter and podcast)

* 2023-10-31
  * Added eRST annotations in MISC Discourse, incl. multiple concurrent discourse relations and discourse relation signals
  * Added morphological segmentation in MISC MSeg
  * Added Construction Grammar annotations in MISC Cxn
  * Added second human written document summaries as summary2 in metadata for the test set

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
Genre: academic blog email fiction government legal news nonfiction social spoken web wiki
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
