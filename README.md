# Summary

Universal Dependencies syntax annotations from the GUM corpus (https://corpling.uis.georgetown.edu/gum/)

# Introduction

GUM, the Georgetown University Multilayer corpus, is an open source collection of richly annotated web texts from multiple text types. The corpus is collected and expanded by students as part of the curriculum in the course LING-367 "Computational Corpus Linguistics" at Georgetown University. The selection of text types is meant to represent different communicative purposes, while coming from sources that are readily and openly available (usually Creative Commons licenses), so that new texts can be annotated and published with ease.

The dependencies in the corpus up to GUM version 5 were originally annotated using Stanford Typed Depenencies (de Marneffe & Manning 2013) and converted automatically to UD using DepEdit (https://corpling.uis.georgetown.edu/depedit/). The rule-based conversion took into account gold entity annotations found in other annotation layers of the GUM corpus (e.g. entity annotations), and has since been corrected manually in native UD. The original conversion script used can found in the GUM build bot code from version 5, available from the (non-UD) GUM repository. Documents from version 6 of GUM onwards were annotated directly in UD, and subsequent manual error correction to all GUM data has also been done directly using the UD guidelines. For more details see the [corpus website](https://corpling.uis.georgetown.edu/gum/).

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
