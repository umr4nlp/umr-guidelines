# Uniform Meaning Representation (UMR) 0.1 Specification
=======================================================

**November 4, 2019**

-AUTHORS-

**Table of Contents**

* Part 1. [Introduction](#part-1-introduction) (Bert)
* Part 2. [From AMR to UMR](#part-2-from-amr-to-umr) (Bert)
* Part 3. [Sentence-Level Representation](#part-3-sentence-level-representation)
    * Part 3-1. [UMR Concepts](#part-3-1-umr-concepts)
      * Part 3-1-1. [Named entities](#part-3-1-1-named-entities)  (Bert, Andy)
      * Part 3-1-2. [Concept word mismatches](#part-3-1-2-concept-word-mismatches)  [reflexives,causatives, inchoatives, noun incorporation, identify what counts as light verbs] (Bill et al, Andy)]
      * Part 3-1-3. [Word senses](#part-3-1-3-word-senses)
      * Part 3-1-4. [Identification of eventive concepts](#part-3-1-4-event-identification)
      * Part 3-1-5. [Scope for Quantification and negation](#part-3-1-5-scope-for-quantification-and-negation) (James)
    * Part 3-2. [UMR relations](#part-3-2-umr-relations) 
      * Part 3-2-1. [Participant roles](#part-3-2-1-participant-roles) (Bill and Martha)
      * Part 3-2-2. [Non-participant role UMR relations](#part-3-2-2-Non-participant-UMR-relations)
    * Part 3-3. [UMR attributes](#part-3-3-UMR-attributes) 
      * Part 3-3-1. [Aspect](#Part-3-3-1-Aspect) 
      * Part 3-3-2. Mode
      * Part 3-3-3. Polarity
      * Part 3-3-4. Quant
      * Part 3-3-5. Unit
* Part 4. [Document-Level Representation](#part-4-document-level-representation)
    * Part 4-1. [Coreference](#part-4-1-coreference) (Jayeol, Bert) 
    * Part 4-2. [Temporal Dependency](#part-4-2-temporal-dependency) (Bert, Jiarui)
    * Part 4-3. [Modality Dependency](#part-4-3-modal-dependency) (Meagan, Bill)
* Part 5. Integrated examples


##  Part 1: Introduction

The **Uniform Meaning Representation** (UMR) project aims to design a meaning representation that facilitates
the computational interpretation of a text. UMR combines a **sentence-level** representation that is adapted 
from **Abstract Meaning Representation** (AMR), which focuses on **predicte-argument structures**, **word senses**, **named entities**, **multi-word expressions**, **aspect**, and **quantification**, and a document-level representation
that focuses on **coreference**, **temporal** and **modal** relations. We illustrate this representation with a short English document, and then describe in more detail each component of UMR in the next few sections. UMR is intended to be a cross-lingual annotation framework with a shared set of **abstract** concepts and relations. 

Operationally, for both sentence-level and document-level annotation, we assume an annotation procedure in which a document is processed sentence by sentence. The sentence-level representation is annotated first, so that the document-level annotation can make reference to the concepts in the sentence-level representation.

```
Snt1: Edmund Pope tasted freedom today for the first time in more than eight months.

(t2 / taste-01
  :aspect Performance
  :ARG0 (p / person :wiki "Edmond_Pope"
         :name (n2 / name :op1 "Edmund" :op2 "Pope"))
  :ARG1 (f / free-04
         :ARG1 p)
  :time (t3 / today)
  :ord (o3 / ordinal-entity :value 1
        :range (m / more-than
                :op1 (t / temporal-quantity :quant 8
                    :unit (m2 / month)))))
                    
(s1 / sentence
    :temporal(
          (s1t3 depends-on DCT) )
    :modal( (s1t2 :AFF AUTH) ) )
        
```
The document-level representation includes a list of **temporal and modal dependencies**, as well as a list of **coreference relations**. In this first sentence, the first temporal relation is between *DCT*, a constant that refers to the time when the document is created, and *today*, a concept that can only be correctly interpreted if we know the DCT of the document. In this sense, we say that *today* depends on DCT, hence the relation between them is *depends-on*. We will define a set of temporal relations we use in UMR in Section 3-2.  The second temporal relation is between *today* and *taste-01*, and we say here *taste-01* happened sometime *today* and therefore is included in *today*.

The document-level representation also includes a list of modal dependencies. There is only one modal relation in this sentence, and it is between *taste-01* and *AUTH*. Like DCT, AUTH is also a constant that indicates that the *taste-01* event definitely happened, and is thus positive (as indicated by the *POS* label) from the author's perspective.


```
Snt2: Pope is the American businessman who was convicted last week on spying charges and sentenced to 20 years in a Russian prison.

(b2 / businessman
      :mod (c5 / country :wiki "United_States"
            :name (n6 / name :op1 "America"))
      :domain (p / person :wiki "Edmond_Pope"
            :name (n5 / name :op1 "Pope"))
      :ARG1-of (c4 / convict-01
      	    :aspect Performance
            :ARG2 (c / charge-05
                  :ARG1 b2
                  :ARG2 (s2 / spy-01 :ARG0 p))
            :time (w / week
                  :mod (l / last)))
      :ARG1-of (s / sentence-01
            :aspect Performance
            :ARG2 (p2 / prison
                  :mod (c3 / country :wiki "Russia"
                        :name (n4 / name :op1 "Russia"))
                  :duration (t3 / temporal-quantity :quant 20
                        :unit (y2 / year)))
            :ARG3 s2))
 
(s2 / sentence
    :temporal(
        (s2s :After s2c4)
	(s2w :depends-on DCT) )
    :modal(
      (s2c4 :AFF AUTH)
      (s2s :AFF AUT)
      (s2s2 :AFF AUTH) ) )
```
<!-- should annotate coreference for nominals? if so we need to annotate "the american businessman"-->

For this sentence, the temporal relations represent the fact that the *conviction* event and the *sentence* event both
happened *last week*. The modal dependencies indicate that from the author's perspective, the *conviction* event and the
*sentence* event definitely happened. 


```
Snt3: He denied any wrongdoing.
(d / deny-01 
      :aspect Performance
      :ARG0 (h / he)
      :ARG1 (t / thing
            :ARG1-of (d2 / do-02
                  :ARG0 h
                  :ARG1-of (w / wrong-02))))
  
(s3 / sentence
    :coref( (s3h :same-entity s1p))
    :temporal((s3d :before DCT))
    :modal ( (s3d :AFF AUTH))
	     (s3d2 :NEG (s2h :AFF AUTH)  )
```

For this sentence, the coreference annotation indicates that *he* is the same person as *Alexander Pope* mentioned in
Sentence 1. 

The temporal annotation indicates that the document creation time is after his denial. When annotating temporal relations, we always need to pick a *reference time* with respect to which the temporal relation between the reference time and the event can be determined. In this case, it is not clear the denying event happened before or after the conviction and sentencing events, so the reference time is determined to be the document creation time.

The modal relation indicates that the denying event definitely happened according to the author, and wrongdoing did not happen according to Alexander Pope, based on the author's account.



```
Snt4: Russian President Vladimir Putin pardoned him for health reasons.
(p3 / pardon-01
      :aspect Performance
      :ARG0 (p / person :wiki "Vladimir_Putin"
            :name (n / name :op1 "Vladimir" :op2 "Putin")
            :ARG0-of (h / have-org-role-91
                  :ARG1 (c / country :wiki "Russia"
                        :name (n2 / name :op1 "Russia"))
                  :ARG2 (p2 / president)))
      :ARG1 (h2 / he)
      :ARG1-of (c2 / cause-01
            :ARG0 (r2 / reason
                  :mod (h3 / health))))

(s4 / sentence
    :coref( (s4h :same-entity s1p))
    :temporal( (s4p3 :after s2s))
    :modal ( (s4p3 :AFF AUTH)) )
```

In the document-level representation for this sentence, the person that is pardoned by Putin is Alexander Pope, and this is done by annotating *he* as the same person as the person whose name is Alexander Pope. In the temporal annotation, the *convict-01* event is designated as the reference time of *pardon-01* and happens before the *pardon-01* event. In the modal annotation, *pardon-01* is annotated as positve from the point of view of the author.


```
Snt5: Pope was flown to the U.S. military base at Ramstein, Germany.
 
(f / fly-01
      :aspect Performance
      :ARG1 (p / person :wiki "Edmond_Pope"
            :name (n3 / name :op1 "Pope"))
      :destination (b2 / base
            :mod (m / military
                  :mod (c / country :wiki "United_States"
                        :name (n / name :op1 "U.S.")))
            :location (c3 / city :wiki "Ramstein_Air_Base"
                  :name (n4 / name :op1 "Ramstein")
                  :location (c2 / country :wiki "Germany"
                        :name (n2 / name :op1 "Germany")))))

(s5 / sentence
    :temporal((s5f :after s4p3))
    :modal ((s5f :AFF AUTH) )
```
In the document-level annotation of this sentence, *pardon-01* from the previous sentence is chosen as the
reference time of the *fly-01* event, and it happened before the *fly-01* event. The author is positive that the *fly-01* 
event happened.

```
Snt6: He will spend the next several days at the medical center there before he returns home with his wife Sherry

(s2 / spend-02
      :ARG0 (h2 / he)
      :ARG1 (s / several
            :op1 (t / temporal-quantity :quant 1
                  :unit (d / day
                        :mod (n2 / next))))
      :time (b / before
            :op1 (r / return-01
                  :ARG1 h2
                  :ARG4 (h3 / home)
                  :accompanier (p / person :wiki -
                        :name (n / name :op1 "Sherry")
                        :ARG0-of (h / have-rel-role-91
                              :ARG1 h2
                              :ARG2 (w / wife)))))
      :location (c / center
            :mod (m / medical)
            :location (t2 / there)))

(s6 / sentence
  :temporal(
     (s6s2 :after s5f)
     (s6r :after s6s2 ))
  :modal (s6s2 :AFF AUTH)
         (s6r :AFF AUTH))
  :coref (s6h2 :same-entity s1p)))
```
In the temporal annotation of this sentence, the DCT is chosen as the reference time for *spend-02*, which is in turn the reference time for *return-01*. In the modality annotation, both *spend-02* and and *return-01* actually happened according to the author. In the coreference annotation, *he* is considered to be the same as the *person* whose name is Alexander Pope in sentence 1. 


 ```
Snt7: Pope was in remission from a rare form of bone cancer when he was arrested in Russia.

(h / have-mod-91
       :aspect Stative
       :ARG1 (p / person :wiki "Edmond_Pope"
             :name (n3 / name :op1 "Pope"))
       :ARG2 (r / remission-02
             :ARG1 (d / disease :wiki -
                   :name (n / name :op1 "bone" :op2 "cancer")
                   :ARG1-of (r2 / rare-02))
             :time (a / arrest-01
	           :aspect Performance
                   :ARG1 p
                   :location (c / country :wiki "Russia"
                         :name (n2 / name :op1 "Russia")))))

(s7 / sentence
  :temporal( (s7a :overlap s7r))
  :modal ((s7a :AFF AUTH)
         (s7r :AFF AUTH)))
```
For Sentence 7, the *remission-02* event happens simultaneously with the *arrest-01* event, and the *arrest-01* event happended before DCT. According to the author, both *arrest-01* and *remission-2* happened.


```
Snt8: Doctors will examine him for signs that the cancer may have come back while he awaiting trial in a Russian jail.

 (e / examine-01
       :ARG0 (d3 / doctor)
       :ARG1 (h / he)
       :ARG2 (s / signal-07
             :ARG1 (p / possible-01
                   :ARG1 (c3 / come-01
                         :ARG1 (d2 / disease :wiki "Cancer"
                               :name (n / name :op1 "cancer"))
                         :direction (b2 / back)
                         :time (a / await-01
                               :ARG1 h
                               :ARG2 (t / try-02
                                     :ARG1 h)
                               :location (j / jail
                                     :mod (c2 / country :wiki "Russia"
                                           :name (n3 / name :op1 "Russia"))))))
             :ARG2 d3))
(s8 / sentence
  :temporal( (s8e :after s6s2))
  :modal ((s8e :AFF AUTH)
          (s8c3 :NEU AUTH)
          (s8a :AFF AUTH))
  :coref((s8h :same-entity s7p))) 
```

The *examine-01* event will happen after the DCT. According to the author, the *examine-01* event definitely happened.
The author is neutral about whether the cancer has come back. *he* is annotated as being the same person as Alexander Pope.
```
Snt9:  A spokeswoman said that Pope was suffering from malnutrition and high blood pressure.
(s / say-01
      :aspect Performance
      :ARG0 (p3 / person
            :ARG0-of (h2 / have-org-role-91
                  :ARG2 (s2 / spokeswoman)))
      :ARG1 (s3 / suffer-01
            :aspect Stative
            :ARG0 (p / person :wiki "Edmond_Pope" :name (n / name :op1 "Pope"))
            :ARG1 (a / and
                  :op1 (m / malnourished-01
                        :ARG1 p)
                  :op2 (p2 / pressure-01
                        :ARG1 (b2 / blood)
                        :ARG1-of (h / high-02))))
(s9/sentence
 :Temporal ((s9s :before DCT)
            (s9s3 :overlap s9s))
 :Modal ((s9s :AFF AUTH)
         (s9s3 :AFF (s9p3 :AFF AUTH)))
 ```
The document-level representation indicates the *say-01* event happened before the *say-01* event, and the *suffer-01* event overlaps temporally with the *say-01* event. The modality annotation indicates that from the author's perspective, the *say-01* event definitely happened, and the author indicates that the *suffer-01* event happened according to the spokesperson.  


##  Part 2: From AMR to UMR

UMR inherits the sentence-level representation, with modifications. Like AMR, the sentence-level representation of UMR is a single-rooted, directed, node-labeled and edge-labeled graph. The nodes of this graph are UMR concepts, while edges represent UMR relations. 

```
Snt1: Edmund Pope tasted freedom today for the first time in more than eight months.

(t2 / taste-01
  :aspect Performance
  :ARG0 (p / person :wiki "Edmond_Pope"
         :name (n2 / name :op1 "Edmund" :op2 "Pope"))
  :ARG1 (f / free-04
         :ARG1 p)
  :time (t3 / today)
  :ord (o3 / ordinal-entity :value 1
        :range (m / more-than
                :op1 (t / temporal-quantity :quant 8
                    :unit (m2 / month)))))
```

**UMR concepts:** There are a number of ways that UMR concepts are created based on the input sentence:

* Lemmas: Some UMR concepts are simply lemmas. For example, `today` in the example above is a lemma, which happens to have the same form as the word token itself.
* word senses: When a dictionary of word senses is available for a language, a sense-disambiguated word can also be a concept. For instance, `taste-01` in the example above refers to the first sense of the word `taste`
* Concepts formed out of multi-word expressions: `more-than` is a concept that is formed by concatnating multiple words in a sentence. Exactly when multi-word concepts should be formed will be determined on a langugage-by-language basis.
* Named entity type. Named entities in a sentence are annotated with a named entity type concept (e.g., `person`) and a `name` concept. The actual names are annotated as a constant (`Edmund` and `Pope`).
* Abstract concepts. In some cases a concept can be inferred from the context. In this case, the concept does not corrrespond with any particular word in the sentence, hence it is an `abstract` concept.

**UMR relations:** There are also a number of ways relations between concepts are created:

* Participant roles: The partcipant roles characterize the role that a participant plays with respect to the predicate. They can be predicate-specific if a set of *frame files* are defined for a language, where a set of core participant roles are defined for that (a sense of the ) predicate. For example, `:ARG0` and `:ARG1` are participant roles defined for `taste-01`. For languages that do not have *frame files*, the participant role are generic (e.g., `Actor`, `Experiencer`), and they are described in [Part 3](#part-3-2-umr-relations)
* Semantic relations: Other UMR relations include `:time`, `:org`, `:range` etc. that are not normally characterized as participant roles. A complete list of such relations can be found in [Part 3](#part-3-2-umr-relations)

**UMR attrbitues:** UMR currently has three attribute types:

* Aspect: Aspect are annotated for eventive concepts only. Non-eventive concepts are not annotated with Aspect and are assigned the default value `Process`. Possible Aspect values include `Activity`, `Habitual`, `State`, `Endeavor`, `Performance`. A complete of Aspect values with explanations and examples can be found in [Part 3-3-1 Aspect](#part-3-3-1-aspect)
* Polarity: Polarity is only annotated for negative polarity as indicated by negation marker or an affix indicating negation.
* Mode: The mode attribute is typically for the main predicate of a sentence. Its values include `imperative` aand `interrogative`
* Quantity: The value of a `:quant` attribute is a numerical number
* Value: The value of a `:value` attribute is a numerical number. 

**Differences between AMR and UMR**

* modality


## Part 3. Sentence-Level Representation

### Part 3-1. UMR Concepts
 #### Part 3-1-1. Named entities
 
Following AMR, each named entity in a text is annotated with a type. However, the vocabuary of the named entity types are adpated from AMR so that they reflect the characterization of additional languages and thus made uniform across languages. The following is an example that has a *country* entity and a *person* entity. 

```                    
Edmond Pope is an American businessman.
(b2 / businessman
      :mod (c5 / country :wiki "United_States"
            :name (n6 / name :op1 "America"))
      :domain (p / person :wiki "Edmond_Pope"
            :name (n5 / name :op1 "Pope")))                   
```        
The total set of entity types are hierarchically organized 



<!--organization, company, government-organization, military, criminal-organization, political-party, market-sector, school, university, research-institute, team, league-->
<!--location, city, city-district, county, state, province, territory, country, local-region, country-region, world-region, continent; ocean, sea, lake, river, gulf, bay, strait, canal; peninsula, mountain, volcano, valley, canyon, island, desert, forest moon, planet, star, constellation, (landforms and water forms?)-->


|Type   |  Subtype (AMR NE Type) |
|-------|------------------------|
|       |person, family, animal, language, nationality, ethnic-group, regional-group, religious-group, political-movement|
|*Organization* | commerical_org (company), political_org (political-party), government_org (government_organization), military_org (military), criminal_org (criminal-organization), academic_org (school, university, research-institute), sports_org (team, league), market-sector|
| *Geographic-entity*   | ocean, sea, lake, river, gulf, bay, strait, canal, peninsula, mountain, volcano, valley, canyon, island, desert, forest|
|  *Celestial-body*     |moon, planet, star, constellation|
| *region*              | local-region, country-region, world-region|
|  *GPE*     |city, city-district, county, state, province, territory, country| 
|  *facility*| airport, station, port, tunnel, bridge, road, railway-line, canal, building, theater, museum, palace, hotel, worship-place, market, sports-facility, park, zoo, amusement-park|
|  *event*   |  incident, natural-disaster, earthquake, war, conference, game, festival|
|  *product* |vehicle, ship, aircraft, aircraft-type, spaceship, car-make, work-of-art, picture, music, show, broadcast-program|
|       |publication (book, newspaper, magazine, journal)|
|  *Natural-object*| |
|  *Artifact*      |award, law, court-decision, treaty, music-key, musical-note, food-dish, writing-script, variable, program|
|   *Biomedical-entity*| molecular-physical-entity, small-molecule, protein, protein-family, protein-segment, amino-acid, macro-molecular-complex, enzyme, nucleic-acid, pathway, gene, dna-sequence, cell, cell-line, species, taxon, disease, medical-condition|

 #### Part 3-1-2. Concept-word mismatches
 
 Arapahoe example:
```
nih-teb-e'ei-s-o'
nih-   teb                     -e'ei -s               -o' 
Past-  break/remove.stick.like -head -by.blade.Caus   -1s/3s 
`I cut his head off with a knife' 

(n / teb-e'ei-s
  :actor (p / person :ref 1s)
  :undergoer (p2 / person :ref 3s)
  :theme (t /thing :ref obviative)
  :Aspect Performance)
```
 
 #### Part 3-1-3. Word senses
 
 UMR allows concepts to be word senses. In order to annotate word sense, it is necessary to first have a sense inventory for all words that need to be sense disambiguated. For languages that do not have a sense inventory, the concept can simply be lemmas. It is also possible that a language only has a sense inventory for a subset of the words. This is the case with English and Chinese, where word senses are defined for predicates together with their arguments in *frame files*.
 
 [English exmaple]
 [Chinese example]
 
 #### Part 3-1-4. Event identification
 The criteria used to identify events in UMR are largely based on the
criteria used in TimeML (Pustejovsky et al. 2005). Event identification is not based on part of
speech or morphosyntactic expression, but instead on a combination of
semantic type and information packaging. Event identification should be
done at the word (or phrase) level in a particular language. That is,
annotators should consider the meaning of a whole word/phrase in
deciding if it should be identified as an event; annotators need not
analyze the morphological structure of words.

In order to figure out which words in a text qualify as an event for the
purposes of the UMR annotation, it is helpful to consider the difference
between semantic type and information packaging (Croft 2001). Semantic type refers
to the difference between entities, states (or, properties), and
processes; this can be thought of as a categorization of things in the
real world. Information packaging, on the other hand, characterizes how
a particular linguistic expression “packages” the semantic content.
The table below shows the typical types
of constructions that tend to express the different combinations of
semantic types and information packaging, modified from Croft (2001) .

|               |                   Reference                   |                    Modification                    |                  **Predication**                  |
| :-----------: | :-------------------------------------------: | :------------------------------------------------: | :-----------------------------------------------: |                                                                                                                                                                   
|   Entities    | <span class="smallcaps">unmarked nouns</span> |                 relative clauses,                  |              **predicate nominals,**              |
|               |                                               |                    PPs on nouns                    |                  **complements**                  |
|    States     |              deadjectival nouns               | <span class="smallcaps">unmarked adjectives</span> |             **predicate adjectives,**             |
|               |                                               |                                                    |                  **complements**                  |
| **Processes** |       **event nominals, complements,**        |         **participles, relative clauses**          | <span class="smallcaps">**unmarked verbs**</span> |
|               |           **infinitives, gerunds**            |                                                    |                                                   |

The small caps indicates prototypical combinations (entity reference,
state modification, and process predication); these are associated with
unmarked parts of speech cross-linguistically (namely, nouns,
adjectives, and verbs).

The most prototypical expression for an event is a process in
predication, therefore we identify a word/phrase as an event if it has
either the semantic type of the prototype (process) or the prototypical
information packaging (predication). The categories which should be
identified as events are shown in bold in the table.

##### Part 3-1-4-1. Processes in predication

Predicated processes are the most prototypical subcategory of events,
corresponding cross-linguistically to unmarked verbs. They will
therefore always be identified as events. This is shown in
[\[1\]](#predprocess) below. (Throughout this section, words
that are identified as events will be shown in bold.)

<span id="predprocess" label="predprocess">\[1\]</span>

<span id="repair" label="repair">\[a\]</span> *She
<u>**repaired**</u> her bike*.  
<span id="wentrepair" label="wentrepair">\[b\]</span> *Before
she <u>**went**</u> to school, she **repaired** my bike.*  

Regardless of whether they are in an independent clause, like *repaired*
in [\[1a\]](#1a), or a dependent clause, like *went* in
[\[1b\]](#wentrepair), predicated processes are always
identified as events.

##### Part 3-1-4-2. Processes in modification and reference

Processes packaged as modifiers or referents should also be identified
as events. Cross-linguistically, these may take a variety of
morphosyntactic forms, such as events nominals (as in
[\[2a\]](#eventnom)), non-finite complements (as in
[\[2b\]](#complement)), participles (as in
[\[2c\]](#participle)), or relative clauses (as in
[\[2d\]](#relclause)).

<span id="refprocess" label="refprocess">\[2\]</span>

<span id="eventnom" label="eventnom">\[a\]</span> *The
**<u>storm</u> damaged** the roads.*

<span id="complement" label="complement">\[b\]</span> *She
**wanted <u>to go</u>** to school.*

<span id="participle" label="participle">\[c\]</span> *The
student **<u>playing</u>** the violin **likes** Bach.*

<span id="relclause" label="relclause">\[d\]</span> *The
student, who is **<u>playing</u>** the violin, **likes** Bach.*

It’s important to remember that it’s the combination of semantic type
and information packaging that determines whether or not a particular
word in a particular context is identified as an event. The
morphological structure of a word (i.e., whether or not it derives from
a verb) doesn’t factor into whether or not it is identified as an event.
For example, not all event nominals are derived from verbs, as in
[\[3a\]](#eventnom2); and, not all words derived from verbs
actually refer to processes, as in
[\[3b\]](#nominalization).

<span id="refprocess2" label="refprocess2">\[3\]</span>

<span id="eventnom2" label="eventnom2">\[a\]</span> *He is
**planning** a **<u>ceremony</u>** for Saturday.*

<span id="nominalization" label="nominalization">\[b\]</span>
*The bus <u>driver</u> **turned** the corner too sharply.*

Even the same lexical item may or may not refer to a process, depending
on context as in ([\[4\]](#nominal)) below.

<span id="nominal" label="nominal">\[4\]</span>
<span id="event" label="event">\[a\]</span>
*The <u>**final exam**</u> began at 8:00.*

<span id="nonevent" label="nonevent">\[b\]</span>
*One student **threw** their <u>final exam</u> in the trash.*

In ([\[4a\]](#event)), *final exam* refers to a process and therefore
is identified as an event. In ([\[4b\]](#nonevent)), however,
*final exam* refers to a physical object and therefore should not be
identified as an event.

Participles (or other non-finite verb forms) are identified as events,
unless they are part of a compound. For example, *floating* in *floating
hospitals* is identified as an event, but *firing* in *firing squad* is
not, since it is part of a compound. One way to check for this
distinction is to see if the event described by the participle must be
ongoing at the reference time. For example, one can say *I saw the
firing squad* without having seen an actual firing event, whereas *I saw
the floating hospitals* implies that the seer witnessed the floating
event as well.

##### Part 3-1-4-3. States and entities

As mentioned above, anything that is predicated is identified as an
event, even if it is not a process. These correspond to predicate
nominals, as in [\[5a\]](#prednom), and predicate adjectives, as in
[\[5b\]](#predadj).

<span id="prednomadj" label="prednomadj">\[5\]</span>

<span id="prednom" label="prednom">\[a\]</span> *She <u>**is an
engineer**</u>.*

<span id="predadj" label="predadj">\[b\]</span> *She <u>**is
clever**</u>.*

States and entities expressed in complement clauses are also identified
as events, as in [\[6\]](#compnomadj).

<span id="compnomadj" label="compnomadj">\[6\]</span>

<span id="entitycomp" label="entitycomp">\[a\]</span> *She
wants <u>**to be a doctor**</u>.*

<span id="statecomp" label="statecomp">\[b\]</span> *She expects
<u>**to be on time**</u>.*

States in modification, as in [\[7a\]](#statemod1) and
[\[7b\]](#statemod2), and states in reference, as in
[\[7c\]](#stateref), are not identified as events.

<span id="states" label="states">\[7\]</span>

<span id="statemod1" label="statemod1">\[a\]</span> *The
<u>tall</u> man...*

<span id="statemod2" label="statemod2">\[b\]</span> *The man,
<u>who is tall</u>...*

<span id="stateref" label="stateref">\[c\]</span> *His
<u>happiness</u>...*

Similarly, entities in modification, as in [\[8a\]](#entitymod),
and entities in reference, as in [\[8b\]](#entityref), are not
identified as events.

<span id="entities" label="entities">\[8\]</span>

<span id="entitymod" label="entitymod">\[a\]</span> *The man,
<u>who is a doctor</u>...*

<span id="entityref" label="entityref">\[b\]</span> *The
<u>doctor</u>*

Causal relationships follow the same rules as states and entities. They
are identified as events when they’re predicated, as in
[\[9\]](#causepred), but they are not identified as events
otherwise, like in [\[10\]](#causeother).

<span id="causepred" label="causepred">\[9\]</span> *The
**explosion <u>caused</u>** the house **to collapse**.*

<span id="causeother" label="causeother">\[10\]</span> *The
house **collapsed** <u>because</u> of the **explosion**.*

##### Part 3-1-4-4. Special cases

There are some common constructions where languages may use multiple
words to express a single event. In all of these cases, only one event
is identified.  
**Complex predicates.** Following TimeML (Pustejovsky et al. 2005), complex predicates
correspond to a single event. Complex predicates can be identified
following some of FrameNet’s semantic guidelines for support predicates
(Ruppenhofer et al. 2016, 34-36). Complex predicates in English generally consist of a *verb + noun*
combination, as shown in [\[11\]](#compred).

<span id="compred" label="compred">\[11\]</span> *She <u>took a
**walk**</u> around the block.*

With complex predicates in English, the noun supplies the bulk of the
semantic information; in [\[11\]](#compred), the event describes an
act of walking, not an act of taking. Furthermore, the meaning of the
verb in a complex predicate has a different meaning when used by itself
(i.e., there is no actual taking involved in *take a walk*). The final
criterion for the identification of complex predicates is that the
support verb (in FrameNet’s terms) is fixed (i.e., a particular noun
always occurs with the same support verb). For example, you can’t say
*\*make a walk* or *\*give a walk*. Similarly, *give a talk* and *make a
choice* also have fixed support verbs (*\*take a talk*, *\*take a
choice*). The event noun (e.g., *walk, talk, choice*) in these cases is
identified as the event.  
**Light verbs.** There are a number of verbs in English that only
indicate the occurrence of an event expressed elsewhere, such as
*happen, occur, take place*, etc.

<span id="lightv" label="lightv">\[12\]</span> *The **trip**
<u>happened</u> over Spring Break.*

In [\[12\]](#lightv), *happened* only indicates that the *trip*
event occurred. These light verbs are not identified as events;
therefore, in [\[12\]](#lightv), only *trip* is identified as an
event.  
**Cognate objects.** There are constructions in which a verb and its
object refer to the same event; often, the verb and the noun are
morphologically related. English allows a few constructions of this
type, as in [\[13\]](#cogobj); other languages may make more
extensive use of this construction.

<span id="cogobj" label="cogobj">\[13\]</span> *She **laughed** <u>a
hearty laugh</u>.*

Like the other special cases discussed here, only a single event is
identified, since semantically there is only one event. For cognate
objects, only the verb is identified as an event.  
**Aspectual verbs.** Languages have various ways to express aspectual
distinctions. English uses aspectual verbs (separate from the main verb)
in order to express inceptive ([\[14\]](#incep)), continuative
([\[15\]](#cont)), terminative ([\[16\]](#term)), and completive
([\[17\]](#comp)) phases of an event.

<span id="incep" label="incep">\[14\]</span> *He <u>started</u>
**painting** the wall.*

<span id="cont" label="cont">\[15\]</span> *He <u>kept on</u>
**painting** the wall.*

<span id="term" label="term">\[16\]</span> *He <u>stopped</u>
**painting** the wall.*

<span id="comp" label="comp">\[17\]</span> *He <u>finished</u>
**painting** the wall.*

Only the verb that expresses the event (here, *paint*) is identified as
an event. The aspectual verbs inform the aspectual annotation of the
verb, but they are not identified as
separate events.

Aspectual verbs may also be used with event nominals, as in
[\[18\]](#aspectnom), or with states in
[\[19\]](#aspectstate).

<span id="aspectnom" label="aspectnom">\[18\]</span> *She
<u>finished</u> **the race**.*

<span id="aspectstate" label="aspectstate">\[19\]</span> *The
**protests** <u>turned</u> **violent**.*

These should be treated in the same way as constructions with verbs.
That is, the aspectual verbs are not themselves identified as events.
The event nominal, like *race* in [\[18\]](#aspectnom), or the
word expressing the state, like *violent* in
[\[19\]](#aspectstate), are identified as events.

##### Part 3-1-4-5. Implicit events

Since UMR annotates meaning, and not form, there are situations where
events are identified in the absence of explicit linguistic material.
These correspond to events which are implicit, given the context, but
not overtly expressed. We encourage annotators to be conservative on
this front; when in doubt, don’t add an implicit event.

We’ve identified two types of situations in which we need to identify an
implicit event: those where the implicit event corresponds to an event
mentioned earlier in the text (as in [\[20\]](#specific)), and
those where it does not (as in [\[21\]](#nonspecific)).

<span id="specific" label="specific">\[20\]</span>

<span id="smoke" label="smoke">\[a\]</span> *John was **smoking** on
the corner of the street, but when he **saw** me, he stopped* <u>
**\[smoking\]**</u>.

<span id="leave" label="leave">\[b\]</span> *They **told** me “a
card was **left** on Tuesday” (no it wasn’t* <u>**\[left\]**</u> *of
course)...*

In [\[20a\]](#smoke), there is an implicit second *smoking* event and
in [\[20b\]](#leave), there is an implicit second *leave* event. These
implicit events should be annotated as co-referential with the event
mentioned earlier in the text.

In [\[21\]](#nonspecific), however, the implicit events don’t
have a relationship with an event previously mentioned in the text;
instead, they refer to generic events which can be filled in from
context.

<span id="nonspecific" label="nonspecific">\[21\]</span>

<span id="say" label="say">\[a\]</span> ***Phoned** Amtrak on
Wednesday,* <u>**\[they said\]**</u> *“We **need** a consignment
number”.*

<span id="go" label="go">\[b\]</span> *“I have **ordered** the Coast
Guard and our entire naval force in the (Central Philippines) region*
<u>**\[to go\]**</u> *to the area,” she **said**.*

In [\[21a\]](#say), the quotation marks make it clear that there is an
implicit *say* event. In [\[21b\]](#go), we can identify a very general
*go* event, since *ordered...to the area* implies a motion event. For
these types of implicit events, the most abstract, least specific event
should be identified. For example in [\[21b\]](#go), we could make an
assumption based on context clues (e.g., *Coast Guard, naval force*),
that the type of motion event is *sail*. But, that assumption may not be
accurate (and may not be shared amongst annotators); therefore, the most
general event possible should be identified.

##### Part 3-1-4-6. Modal events

Different types of modal words may or may not be identified as events.
First, grammaticalized modals, as in [\[22\]](#modalgramm), are
not identified as events.

<span id="modalgramm" label="modalgramm">\[22\]</span>

<span id="may" label="may">\[a\]</span> *She <u>might</u> **be
eating** pizza.*

<span id="can" label="can">\[b\]</span> *She <u>can</u> **speak**
Spanish.*

<span id="should" label="should">\[c\]</span> *He <u>should</u>
**bake** a cake for tomorrow.*

The modalized event, e.g. *be eating* in [\[22a\]](#may), is identified
as an event but the modal is not. This also applies for modals that take
the form of predicate adjectives, as in
[\[23\]](#predadjmodal).

<span id="predadjmodal" label="predadjmodal">\[23\]</span>

*It <u>is possible</u> that she **is eating** pizza.*

*She <u>is able</u> **to speak** Spanish.*

Although these types of modals look like states in predication (and
therefore worthy of identification as an event), they should be regarded
the same as more grammaticalized modals and not identified as events.

Verbs which express mental attitudes, desires, intentions, and indicate
the modalized value of their complement are identified as their own
events, as in [\[24\]](#modalverb).

<span id="modalverb" label="modalverb">\[24\]</span>

<span id="expect" label="expect">\[a\]</span> *I <u>**expect**</u>
that he will **arrive** by 4pm.*

<span id="want" label="want">\[b\]</span> *She <u>**wants**</u> **to
travel** to London.*

<span id="allow" label="allow">\[c\]</span> *They’re not
<u>**allowed**</u> **to leave** yet.*

<span id="need" label="need">\[d\]</span> *We <u>**need**</u> **to
meet** earlier tomorrow.*

There is one exception to this: events that attribute beliefs to a
conceiver, e.g. *think, believe*, are not identified as events, as shown
in [\[25\]](#beliefs).

<span id="beliefs" label="beliefs">\[25\]</span>

<span id="believe" label="believe">\[a\]</span> *Mary
<u>believes</u> that he already **ate** dinner.*

<span id="think" label="think">\[b\]</span> *She <u>thinks</u> that
he’ll **be late**.*

Belief verbs will not be identified as events, since they correspond to
the links between events in the modal strength dependency structure.
 
 
 #### Part 3-1-5. Scope for Quantification and negation

To facilitate the translation of UMR into first-order expressions to support logical inference,
we add a **scope** concept to represent the relative order of the predicate, quantified concept and negated concept.
In most cases, the order of these elements are interpreted in textual order, and do not need an over scope annotation.
The scope annotation is only needed when these elements are interpreted "out-of-order".

```
Someone didn't answer all the questions
(a answer-01
   :ARG0 (p / person)
   :ARG1 (q / question
              :quant A
              :polarity -)
   :pred-of (s / scope
                :ARG0 p
                :ARG1 q))
```
 
### Part 3-2. UMR relations 

   #### Part 3-2-1. Participant roles 
   
  For languages that have *frame files* that define predicate-specific roles, predicate-specific roles are used. If not, UMR provides 
  a list of generic participant roles that do not require frame files:
  
  |Type   |  Roles |
  |-------|------------------------|
  | Central roles | Actor, Undergoer, Theme, Recipient, Force, Causer, Experiencer, Stimulus|
  | Peripheral roles | Instrument, Companion, Material/Source, Place, Start, Goal, Affectee |
  | Roles for entities and events| Cause, Manner, Reason, Purpose, Temporal, Extent |
  
  #### Part 3-2-2. Non-participant UMR relations
   
   
### Part 3-3. UMR attributes
  
  #### Part 3-3-1. Aspect
   
The aspect annotation captures the internal temporal and qualitative
structure of each event. This aspect annotation does not correspond to
specific verbs or grammatical constructions in a language, but
characterizes the nature of the event in context. As will be seen, this
will involve taking aspectual constructions, temporal expressions, and
noun phrases into account in order to determine the aspect annotation of
the event. Each event will be annotated with one of six aspectual
values:


  - <span>Not Applicable (NA)</span>

  - <span>HABITUAL</span>

  - <span>STATE</span>

  - <span>ACTIVITY</span>

  - <span>ENDEAVOR</span>

  - <span>PERFORMANCE</span>
 
 
 
Certain types of events are not annotated for aspect; these will receive
the <span>Not Applicable</span> annotation. Events that occur habitually
are annotated as <span>HABITUAL</span>. All states are simply annotated
as <span>STATE</span>, while for processes, annotators choose between
<span>ACTIVITY</span>, <span>ENDEAVOR</span>, and
<span>PERFORMANCE</span>. Annotators proceed through a series of
decisions, in order to select the appropriate
aspect annotation for each event.

Steps \#1, \#2, and \#3 in the decision tree concern the <span>Not
Applicable</span> annotation. Step \#4 selects events for the
<span>HABITUAL</span> annotation. Step \#5 distinguishes
<span>STATE</span>s from processes. Step \#6 identifies events for the
<span>ACTIVITY</span> annotation. Steps \#7, \#8, and \#9 concern the
distinction between the <span>ENDEAVOR</span> and
<span>PERFORMANCE</span> annotations.

##### Part 3-3-1-1. Event Nominal?

The first point in the decision tree concerns the morphosyntactic
expression of the event. Events expressed as nominals often lack any
grammatical clues as to their aspectual structure. This makes
determining an aspectual annotation value difficult. Therefore, events
expressed as event nominals, as in [\[26\]](#eventnoms), are
annotated as <span>NA</span>.

<span id="eventnoms" label="eventnoms">\[26\]</span>

<span id="meeting" label="meeting">\[a\]</span> *He presented his
research at **the meeting** yesterday.*  
<span>meeting: NA</span>

<span id="game" label="game">\[b\]</span> *After **the game**, she
went home.*  
<span>game: NA</span>

<span id="operation" label="operation">\[c\]</span> *The surgeon
finished **the operation** at 3pm.*  
<span>operation: NA</span>

Any event packaged in a referring expression is considered an event
nominal and annotated with <span>NA</span>. This includes underived
nominals, nominalizations, and gerunds, as in [\[27\]](#gerund).

<span id="gerund" label="gerund">\[27\]</span>

<span id="training" label="training">\[a\]</span> ***The second
training** was cancelled yesterday.*  
<span>training: NA</span>

<span id="barking" label="barking">\[b\]</span> *The dog
interrupted the meeting with **his barking**.*  
<span>barking: NA</span>

Note that *-ing* forms in English can occur in a variety of
constructions; they should only be treated as event nominals when they
are used in referring expressions (as in [\[27a\]](#training) and
[\[27b\]](#barking) above). When they occur in other types of
constructions, as in [\[28\]](#stopbarking), they should not
receive an aspect annotation at this point and should continue on to the
next step.

<span id="stopbarking" label="stopbarking">\[28\]</span> *The
dog stopped **barking** for a few seconds.*

Event nominals that occur in predicate nominal constructions, as in
[\[29\]](#earthquake), are also not annotated at this point;
these are treated like other predicate nominal constructions (see step
\#5 below).

<span id="earthquake" label="earthquake">\[29\]</span>

*It was **an earthquake**.*

##### Part 3-3-1-2. Non-real event?

The next step in the decision tree involves the polarity and epistemic
strength of the event (i.e., the values annotated in the modal strength
dependency in the second pass). Events which have negative polarity
and/or non-full epistemic strength are annotated as <span>NA</span>.
This is because it is difficult to assess (and therefore annotate) the
internal temporal structure of events which have not actually occurred,
or are not actually occurring.

Negative polarity events are often signalled by negative morphemes, as
in [\[30\]](#negpol). The negative polarity of an event may also be
signalled by complement-taking predicates which indicate that their
complement did not occur, as in [\[30e\]](#told), or counterfactual
constructions, as in [\[30f\]](#counterfact). All negative
polarity events are annotated as <span>NA</span>.

<span id="negpol" label="negpol">\[30\]</span>

<span id="eat" label="eat">\[a\]</span> *She <u>didn’t</u> **eat**
pizza for dinner last night.*  
<span>eat: NA</span>

<span id="attend" label="attend">\[b\]</span> *He <u>never</u>
**arrived** at the party.*  
<span>arrive: NA</span>

<span id="doctor" label="doctor">\[c\]</span> *He **is** <u>not</u>
**a doctor**.*  
<span>be-doctor: NA</span>

<span id="bw" label="bw">\[d\]</span> *That cat **<u>wasn’t</u> black
and white.***  
<span>be-black-and-white: NA</span>

<span id="told" label="told">\[e\]</span> *I <u>wish</u> she had
**told** me about it.*  
<span>tell: NA</span>

<span id="counterfact" label="counterfact">\[f\]</span> *If it
had **rained**, I would have **stayed** home.*  
<span>rain: NA</span>  
<span>stay: NA</span>

Another way in which an event may be considered ‘non-real’ is if it has
non-full epistemic strength. Events which are annotated with non-full
epistemic strength in the modal strength annotation also receive the
<span>NA</span> aspect value. The modal strength annotation, however,
does not apply a single epistemic strength value to each event; instead,
the modal strength annotation takes the form of a dependency structure,
with epistemic strength values characterizing the links between events
and conceivers/sources.

When the event is a direct child of the <span>AUTHOR</span> node in the
modal strength dependency, only the epistemic strength value of the
single link between the event and <span>AUTHOR</span> needs to be taken
into account. If this link has a value other than <span>Aff</span>, then
the event should receive the <span>NA</span> aspect annotation; see
[\[31\]](#nonfull).

<span id="nonfull" label="nonfull">\[31\]</span>

<span id="hike" label="hike">\[a\]</span> *He <u>might</u> have
**hiked** this trail yesterday.*  
<span>hike: NA</span>

<span id="leave" label="leave">\[b\]</span> *It’s <u>likely</u> that
she already **left**.*  
<span>leave: NA</span>

<span id="prepare" label="prepare">\[c\]</span> *She left early,
<u>in order to</u> **prepare** dinner.*  
<span>prepare: NA</span>

When events are embedded underneath non-<span>AUTHOR</span> conceivers,
there must be <span>Aff</span> values on every link from the event back
up to the <span>AUTHOR</span>, in order for an event to be considered
‘real’. If any link between the event and the document’s
<span>AUTHOR</span> node has a value other than <span>Aff</span>, the
event should be annotated as <span>NA</span>. Example
[\[32\]](#multlinks) shows events that are annotated as
<span>NA</span> because one the links between the event node and the
<span>AUTHOR</span> node has non-full epistemic strength.

<span id="multlinks" label="multlinks">\[32\]</span>

<span id="fly" label="fly">\[a\]</span> *He <u>wants</u> **to fly** to
New York.*  
<span>fly: NA</span>

<span id="buy" label="buy">\[b\]</span> *She <u>hopes</u> **to buy** a
house.*  
<span>buy: NA</span>

<span id="cond" label="cond">\[c\]</span> *If she **left** early, she
would **be home** by now.*  
<span>leave: NA</span>  
<span>be-home: NA</span>

Note that it is only the event expressed in the complement that receives
the <span>NA</span> annotation. The modal verbs themselves (*want*,
*hope*) are underneath <span>Aff</span> links in the modal strength
dependency; therefore, they are not yet given an aspect annotation
value.

When a conceiver’s thoughts or speech are presented with certainty by
the author, as in [\[33\]](#allpos), there are <span>Aff</span>
values on all of the links between the event and the
<span>AUTHOR</span>.

<span id="allpos" label="allpos">\[33\]</span>

<span id="saypos" label="saypos">\[a\]</span> *Mary <u>said</u>
that she **went** to Santa Fe.*

<span id="reportpos" label="reportpos">\[b\]</span> *The New
York Times <u>reported</u> that Congress **voted** on the bill this
afternoon.*

<span id="believe" label="believe">\[c\]</span> *She <u>thinks</u>
that the cat **stole** the dog’s food.*

Therefore, these types of events are not annotated for aspect at this
point, and move on to the next step.

##### Part 3-3-1-3. Future event?

Events that are predicted to occur in the future are also difficult to
annotate for aspect, since the event has not yet occurred. Therefore,
future events are also annotated with the <span>NA</span> value, as in
[\[34\]](#fut).

<span id="fut" label="fut">\[34\]</span>

<span id="come" label="come">\[a\]</span> *He’<u>ll</u> **come**
around tomorrow.*  
<span>come: NA</span>

<span id="write" label="write">\[b\]</span> *She <u>is going to</u>
**write** the paper tomorrow.*  
<span>write: NA</span>

Events in the future may also have negative polarity or non-full
epistemic stance; these events have already been annotated as
<span>NA</span> in Step \#2.

##### Part 3-3-1-4. Stative?

The next step in the decision tree assesses whether the event is a
<span>STATE</span> or a process (either <span>ACTIVITY</span>,
<span>ENDEAVOR</span>, or <span>PERFORMANCE</span>). The distinction
between states and processes is necessary for event identification (as
states are only identified as events when predicated). According to ,
states are those events which are stative—that is, no change takes place
over the course of the event. There are various ways to express states
in predication, shown in [\[35\]](#statepred); note that entities
and locations in predication (as in [\[35d\]](#nompred) and
[\[35c\]](#locpred), are also annotated as <span>STATE</span>).

<span id="statepred" label="statepred">\[35\]</span>

<span id="verb" label="verb">\[a\]</span> *My cat **loves** tuna.*  
<span>love: STATE</span>

<span id="adjpred" label="adjpred">\[b\]</span> *The doctor **is
tall**.*  
<span>be-tall: STATE</span>

<span id="locpred" label="locpred">\[c\]</span> *The book **is on
the table**.*  
<span>be-on-the-table: STATE</span>

<span id="nompred" label="nompred">\[d\]</span> *She **is an
architect**.*  
<span>be-architect: STATE</span>

<span id="locpred" label="locpred">\[e\]</span> *Your glass **is
in the kitchen**.*  
<span>be-in-the-kitchen: STATE</span>

States can be expressed as verbs (e.g. *love*), adjectival predicates
(*be tall*), locative constructions (*be on the table*), and nominal
predicates (*be an architect*).

There are different types of states, shown in
[\[36\]](#statetypes), however the UMR annotation does not
distinguish these: they are all annotated as <span>STATE</span>.

<span id="statetypes" label="statetypes">\[36\]</span>

<span id="temp" label="temp">\[a\]</span> *My cat **is hungry**.*  
<span>be-hungry: STATE</span>

<span id="inherent" label="inherent">\[b\]</span> *My cat **is
black and white**.*  
<span>be-black-and-white: STATE</span>

<span id="end" label="end">\[c\]</span> *He **was sick** this weekend,
but recovered by Monday.*  
<span>be-sick: STATE</span>

<span id="ongoingstate" label="ongoingstate">\[d\]</span>
*She **is nervous** today.*  
<span>be-nervous: STATE</span>

<span id="ambig" label="ambig">\[e\]</span> *She **was sick**
yesterday.*  
<span>be-sick: STATE</span>

Both temporary states ([\[36a\]](#temp)) and stable (inherent or
permanent) states ([\[36b\]](#inherent)) are annotated as
<span>STATE</span>. Likewise, states that have come to an end
([\[36c\]](#end)), states that are ongoing
([\[36d\]](#ongoingstate)), and states where it is unclear
whether or not they are ongoing ([\[36e\]](#ambig)), are all annotated
<span>STATE</span>.

Modal verbs, as in [\[37\]](#mod), are also annotated as
<span>STATE</span>.

<span id="mod" label="mod">\[37\]</span>

<span id="want" label="want">\[a\]</span> *He **wants** to travel to
Albuquerque.*  
<span>want: STATE</span>

<span id="need" label="need">\[b\]</span> *The cat **needs** to be
fed.*  
<span>need: STATE</span>

<span id="dread" label="dread">\[c\]</span> *He**’s dreading** their
decision.*  
<span>dread: STATE</span>

Ability modals, as in [\[38\]](#ability), are also annotated with
<span>STATE</span>.

<span id="ability" label="ability">\[38\]</span>

<span id="able" label="able">\[a\]</span> *She <u>is able to</u>
**sing** that aria.*  
<span>sing: STATE</span>

<span id="can" label="can">\[b\]</span> *This car <u>can</u> **go** up
to 150 mph.*  
<span>go: STATE</span>

In this analysis, ability modals refer to a static state of affairs,
i.e. an entity possesses the relevant ability. For examples like
[\[38a\]](#able), ability modals may look more like event
quantification. That is, there are probably multiple singing events that
this example is generalizing over. Examples like [\[38b\]](#can),
however, show how ability modals are more like states. It is possible
that the car has never actually gone as fast as 150 mph; the car just
has the parts and (theoretical) ability to do so. Therefore, all types
of ability modals, both [\[38a\]](#able) and [\[38b\]](#can), are
analyzed as states and annotated as such.

There is a type of event, called “inactive actions” by , which is
semantically intermediate between states and processes. In many
languages, they can be construed either way. For example, English *lie*
can occur in the Progressive (*Bill **is lying** on the bed*) or the
Simple Present (*The Sandias **lie** to the east of Albuquerque*). And
across languages there is variation as to the default construal of
inactive actions. The most frequent inactive actions are posture verbs
(*sit, stand, lie, hang*), perception verbs (*see/look at, watch,
hear/listen to, feel*), some sensation verbs (*ache*), mental activity
verbs (*think, understand*), and verbs of operation/function (*work* in
*This washing machine **works/is working***). For the UMR annotation,
inactive actions in all constructions are annotated as
<span>STATE</span>.

At this point, all events that have not yet received an aspect
annotation are processes. Processes are annotated as either
<span>ACTIVITY, ENDEAVOR</span>, or <span>PERFORMANCE</span>. These
values differ in the boundedness of the event both in terms of temporal
progression and qualitative state. Steps \#6-\#9 distinguish between
different types of processes.

##### Part 3-3-1-5. Habitual?

The next step in the decision tree concerns the application of the
<span>HABITUAL</span> aspect value. This value should be applied to all
events that are presented as occurring usually or habitually, as in
[\[39\]](#hab).

<span id="hab" label="hab">\[39\]</span>

<span id="bake" label="bake">\[a\]</span> *He **bakes** pies.*  
<span>bake: HABITUAL</span>

<span id="ride" label="ride">\[b\]</span> *She **rides** her bike to
work.*  
<span>ride: HABITUAL</span>

<span id="vacation" label="vacation">\[c\]</span> *They
**vacation** in Taos every winter.*  
<span>vacation: HABITUAL</span>

<span id="vacationpst" label="vacationpst">\[d\]</span> *They
**used to vacation** in Taos every winter.*  
<span>vacation: HABITUAL</span>

In English, habitual events are signalled by the Simple Present
construction. Note that the <span>HABITUAL</span> annotation is not used
for ability modals (e.g., *he can bake apple pie*); these events should
continue on to the next step.

##### Part 3-3-1-6. Evidence that event ended?

The <span>ACTIVITY</span> label applies when there is no evidence that
the event has come to an end, as in [\[40\]](#activity).

<span id="activity" label="activity">\[40\]</span>

<span id="ongoing" label="ongoing">\[a\]</span> *He is still
**writing** his paper.*  
<span>write: ACTIVITY</span>

<span id="ambiguous" label="ambiguous">\[b\]</span> *He was
**writing** his paper yesterday.*  
<span>write: ACTIVITY</span>

This covers cases where it is clear that the process is still ongoing at
document creation time, as in [\[40a\]](#ongoing), but also cases
where it is ambiguous whether or not the process continues, as in
[\[40b\]](#ambiguous).

This step is largely dependent on context and real world knowledge,
however there are some grammatical cues that can help at this point in
the decision tree. Events in the present tense, as in
[\[41\]](#playact), will always be annotated as
<span>ACTIVITY</span>.

<span id="playact" label="playact">\[41\]</span> *He **is playing**
the violin.*  
<span>play: ACTIVITY</span>

Inceptive and continuative aspectual auxiliaries, as in
[\[42\]](#incon), also do not imply that an event has (necessarily)
ended.

<span id="incon" label="incon">\[42\]</span>

<span id="playstart" label="playstart">\[a\]</span> *He
<u>started</u> **playing** the violin.*  
<span>play: ACTIVITY</span>

<span id="playkeep" label="playkeep">\[b\]</span> *He <u>kept
on</u> **playing** the violin.*  
<span>play: ACTIVITY</span>

If there is clear evidence that the event has come to an end prior to
Document Creation Time (DCT), it moves on to the next step.

##### Part 3-3-1-7. Aspectual marking?

Steps \#7, \#8, and \#9 distinguish between the <span>ENDEAVOR</span>
and <span>PERFORMANCE</span> aspect annotations. Both the
<span>ENDEAVOR</span> and <span>PERFORMANCE</span> aspectual types
entail that the process has come to an end; they are distinguished by
the boundedness of the event in terms of qualitative state. The
<span>PERFORMANCE</span> value is used when the event reaches a result
state distinct from the base (start) state, that is, a specific
“natural” endpoint. The <span>PERFORMANCE</span> value lumps
together Vendler’s achievements (punctual) and accomplishments
(durative). The <span>ENDEAVOR</span> value is used when the events
ends, but does not reach a distinct result state.

The strongest piece of evidence for this decision are aspectual
constructions that distinguish between completive and terminative
events. In English, these are expressed by aspectual auxiliary verbs,
shown in [\[43\]](#aspectaux).

<span id="aspectaux" label="aspectaux">\[43\]</span>

<span id="completiveaux" label="completiveaux">\[a\]</span>
*Mary <u>finished</u> **mowing** the lawn.*  
<span>mow: PERFORMANCE</span>

<span id="terminativeaux" label="terminativeaux">\[b\]</span>
*Mary <u>stopped</u> **mowing** the lawn.*  
<span>mow: ENDEAVOR</span>

Completive aspectual auxiliaries, like *finish* or *complete*, indicate
that the event expressed by the main verb has reached a distinct result
state and therefore should be annotated as <span>PERFORMANCE</span>.
Terminative aspectual auxiliaries, like *stop* or *cease*, indicate that
the event has ended without reaching a distinct result state, and
therefore the event is annotated as <span>ENDEAVOR</span>. In languages
that have grammaticalized aspect systems, the <span>PERFORMANCE</span>
value corresponds to perfective categories and the <span>ENDEAVOR</span>
value corresponds to the imperfective and/or progressive categories.

If there isn’t an aspectual auxiliary in the clause, then the event
moves on to the next step.

##### Part 3-3-1-8. Temporal adverbial?

The second strongest piece of evidence for the
<span>ENDEAVOR/PERFORMANCE</span> distinction is the presence of a
temporal adverbial. Clauses with container adverbials, as in
[\[44a\]](#container), are annotated with the
<span>PERFORMANCE</span> value; clauses with durative adverbials, as in
[\[44b\]](#durative), are annotated with the <span>ENDEAVOR</span>
value.

<span id="adverbial" label="adverbial">\[44\]</span>

<span id="container" label="container">\[a\]</span>

*Mary **mowed** the lawn <u>in thirty minutes</u>.*  
<span>mow: PERFORMANCE</span>

<span id="durative" label="durative">\[b\]</span>

*Mary **mowed** the lawn <u>for thirty minutes</u>.*  
<span>mow: ENDEAVOR</span>

Example [\[44a\]](#container) implies that Mary finished mowing
the lawn; therefore the event is annotated with the
<span>PERFORMANCE</span> value. Example [\[44b\]](#durative)
doesn’t imply that Mary has finished mowing the lawn; therefore the
event is annotated with the <span>ENDEAVOR</span> value.

If there isn’t a durative or container adverbial in the clause, then the
event moves on to the final step.

##### Part 3-3-1-9. Non-result Path?

Certain types of path expressions indicate that an event did not reach a
specific result state; these are called non-result paths. Examples of
non-result paths are show below in [\[45\]](#nonresult).

<span id="nonresult" label="nonresult">\[45\]</span>

<span id="wander" label="wander">\[a\]</span> *They **wandered**
<u>around the city</u>.*  
<span>wander: ENDEAVOR</span>

<span id="walk" label="walk">\[b\]</span> *He **walked** <u>along the
river</u>.*  
<span>walk: ENDEAVOR</span>

<span id="drive" label="drive">\[c\]</span> *They **drove** <u>past
the junction</u>.*  
<span>drive: ENDEAVOR</span>

Events with non-result paths are annotated as <span>ENDEAVOR</span>.

At this point, every event that is left without an aspect annotation is
annotated as <span>PERFORMANCE</span>. These will include processes that
have ended and reached a result state, as shown below in
[\[46\]](#result).

<span id="result" label="result">\[46\]</span>

<span id="atecookies" label="atecookies">\[a\]</span> *The dog
**ate** all the cookies.*  
<span>eat: PERFORMANCE</span>

<span id="walkto" label="walkto">\[b\]</span> *She **walked** to
the grocery store.*  
<span>walk: PERFORMANCE</span>

<span id="jump" label="jump">\[c\]</span> *The horse **jumped**.*  
<span>jump: PERFORMANCE</span>

<span id="play" label="play">\[d\]</span> *We **played** video games
yesterday.*  
<span>play: PERFORMANCE</span>
  




## Part 4. Document-Level Representation
### Part 4-1. Coreference


Anaphorical expressions such as pronouns cannot be properly interpreted without identifying their referents. This is generally done by linking an anaphorical expression to a named entity, a process generally known as *coreference* in the field of NLP. Coreference is an established NLP task, and the goal here is to identify the most relevant types of coreference in the UMR framework.  

For the UMR corereference annotation, we first need to answer two questions. The first is what counts as an anaphorical expression. For UMR annotation, we focus on pronouns. The second question is what types of coreference relations we are considering. The most common type of coreference relations are *identity* relations, and we label such relations as *same*. Identity relations means two expressions have the same referent. In the example below, *he* refers to the same person as the person whose name is "Edmond Pope":

```
Snt1: Edmund Pope tasted freedom today for the first time in more than eight months.

(t2 / taste-01
  :Aspect Performance
  :ARG0 (p / person :wiki "Edmond_Pope"
         :name (n2 / name :op1 "Edmund" :op2 "Pope"))
  :ARG1 (f / free-04
         :ARG1 p)
  :time (t3 / today)
  :ord (o3 / ordinal-entity :value 1
        :range (m / more-than
                :op1 (t / temporal-quantity :quant 8
                    :unit (m2 / month)))))


Snt3: He denied any wrongdoing.
(d / deny-01
      :Aspect Performance
      :ARG0 (h / he)
      :ARG1 (t / thing
            :ARG1-of (d2 / do-02
                  :ARG0 h
                  :ARG1-of (w / wrong-02))))
  
(s3 / sentence
    :coref((s3h :same-entity s1p)) )
```

Subset relation:

```
# ::snt He is very possesive and controlling but he has no right to be as we are not together.
(c / contrast-01
      :ARG1 (a / and
            :op1 (p / possessive-03
	          :Aspect Stative
                  :ARG0 (h2 / he)
                  :degree (v2 / very))
            :op2 (c3 / control-01
                  :ARG0 h2
                  :degree (v / very)))
      :ARG2 (r / right-05 :polarity -
            :ARG1 h2
            :ARG2 a
            :ARG1-of (c2 / cause-01
                  :ARG0 (t / together
		        :Aspect Stative
                        :domain (w / we)))))
(s / sentence
  :coref ((s4h2 :subset-of s4w)))
```

#### Event coreference
 
	
 - Event identity

 We use *same-event* to represent cases where two event mentions refer to  the same event.
 
::id PROXY_APW_ENG_20080415_1054.19 ::date 2013-07-19T04:50:53 ::snt-type body ::annotator SDL-AMR-09 ::preferred
::snt El-Shater and Malek's property was confiscated and is believed to be worth millions of dollars.
 ::save-date Wed Jan 20, 2016 ::file PROXY_APW_ENG_20080415_1054_19.txt
```
(a / and
      :op1 (c / confiscate-01
            :Aspect Performance
            :ARG1 (a2 / and
                  :op1 (p3 / property
                        :poss (p / person :wiki "Khairat_el-Shater" :name (n / name :op1 "El-Shater")))
                  :op2 (p4 / property
                        :poss (p2 / person :wiki - :name (n2 / name :op1 "Malek")))))
      :op2 (b / believe-01
            :ARG1 (w / worth-01
                  :ARG1 a2
                  :ARG2 (m / multiple
                        :op1 (m2 / monetary-quantity :quant 1000000
                              :unit (d / dollar))))))
```

 ::id PROXY_APW_ENG_20080415_1054.20 ::date 2013-07-19T04:57:55 ::snt-type body ::annotator SDL-AMR-09 ::preferred
 ::snt Abdel-Maksoud stated the confiscation will affect the Brotherhood's financial bases.
 ::save-date Thu May 28, 2015 ::file PROXY_APW_ENG_20080415_1054_20.txt
```
(s / state-01
      :Aspect Performance
      :ARG0 (p / person :wiki "Hamdeen_Sabahi" :name (n / name :op1 "Abdel-Maksoud"))
      :ARG1 (a / affect-01
            :ARG0 (c / confiscate-01)
            :ARG1 (b2 / base
                  :poss (o / organization :wiki "Muslim_Brotherhood" :name (n2 / name :op1 "Brotherhood"))
                  :mod (f / finance))))

(s2 / sentence
  :coref ((s2c :same-event s1c)))
```

Event identity also includes cases where the same underlying event is referred to with two very different linguistic expressions. This is the case for **introduced** and **provide**.
 
	

 ::id nw.chtb_0021.2 ::date 2012-11-01T15:15:42 ::annotator SDL-AMR-09 ::preferred
 ::snt The Three Gorges project on the Yangtze River has recently **introduced*** the first foreign capital .
 ::save-date Fri Oct 24, 2014 ::file nw_chtb_0021_2.txt
```
(i / introduce-01
      :ARG0 (p / project :wiki "Three_Gorges_Dam" :name (n / name :op1 "The" :op2 "Three" :op3 "Gorges")
            :location (r / river :wiki "Yangtze" :name (n2 / name :op1 "Yangtze" :op2 "River")))
      :ARG1 (c2 / capital
            :mod (f2 / foreign)
            :ord (o / ordinal-entity :value 1))
      :time (r2 / recent))
```
 ::id nw.chtb_0021.3 ::date 2012-11-01T15:29:23 ::annotator SDL-AMR-09 ::preferred
 ::snt The loan , a sum of 12.5 million US dollars , is an export credit **provided** to the Three Gorges project by the Canadian government , which will be used mainly for the management system of the Three Gorges project .
 ::save-date Thu Dec 19, 2013 ::file nw_chtb_0021_3.txt

```
(c2 / credit
      :mod (e / export-01)
      :ARG1-of (p / provide-01
            :ARG0 (g / government-organization
                  :ARG0-of (g2 / govern-01
                        :mod (c / country :wiki "Canada"
                              :name (n / name :op1 "Canada"))))
            :ARG2 (p2 / project :wiki "Three_Gorges_Dam"
                  :name (n2 / name :op1 "Three" :op2 "Gorges")))
      :ARG1-of (u / use-01
            :ARG2 (s / system
                  :poss p2
                  :mod (m2 / manage-01))
            :mod (m3 / main))
      :domain (m / monetary-quantity :quant 12500000
            :unit (d / dollar
                  :mod (c3 / country :wiki "United_States"
                        :name (n3 / name :op1 "US")))
            :ARG1-of (l / loan-01)))
	    
(s / sentence
   :coref ((s2p :same-event s1i)))
```	 

- subset

*subset* is also used to annotate the subset relations between two event mentions, with one referring to a subset of another.


::id PROXY_AFP_ENG_20080719_0249.9 ::date 2013-07-06T05:53:36 ::snt-type body ::annotator SDL-AMR-09 ::preferred
 ::snt 1 arrest took place in the Netherlands and another in Germany.
 ::save-date Sat Jul 6, 2013 ::file PROXY_AFP_ENG_20080719_0249_9.txt

```
(a / and
      :op1 (a2 / arrest-01 :quant 1
            :Aspect Performance
            :location (c / country :wiki "Netherlands"
                  :name (n / name :op1 "Netherlands")))
      :op2 (a3 / arrest-01
            :Aspect Performance
            :location (c2 / country :wiki "Germany"
                  :name (n2 / name :op1 "Germany"))
            :mod (a4 / another)))
```	    
 ::id PROXY_AFP_ENG_20080719_0249.14 ::date 2013-07-06T06:12:27 ::snt-type body ::annotator SDL-AMR-09 ::preferred
 ::snt The arrests were ordered by anti-terrorism judge fragnoli.
 ::save-date Tue Sep 17, 2013 ::file PROXY_AFP_ENG_20080719_0249_14.txt
```
(o / order-01
      :Aspect Performance
      :ARG0 (p / person :wiki -
            :name (n / name :op1 "Fragnoli")
            :ARG0-of (o2 / oppose-01
                  :ARG1 (t / terrorism))
            :ARG0-of (h / have-org-role-91
                  :ARG3 (j / judge-01)))
      :ARG2 (a / arrest-01))
 
 (s / sentence
  :coref ((s1a3, s2a :subset-of s1a3))
```

- Script / subevent?

For now UMR does not annotate cases where one event is a subevent of another event, or when an event is part of a `script'. These will be annotated under temporal relations.

 Reports suggest that the group of nine were having a **picnic** on Friday when they were abducted in the Saada province of Yemen. A spokesman for the Yemeni Embassy said "The foreigners **ventured** outside the city of Saada without the required police escorts due to the heightened security situation in the area.
  
  
  


### Part 4-2. Temporal Dependency

The temporal annotation in UMR is done at both the sentence level and the document level. For instance, a time expression that serves as the modifier of a predicate is annotated at the sentence level. In the sentence below, the time expression 
*April 1998* is annotated as a temporal modifier of the predicate *sign*. Likewise, the temporal relation between an event and its document creation time (DCT) is also annotated at the sentence level. In the example below, the temporal relation between *sign* and the DCT is annotated as `:time (b2 /before :op (n/now))`. The temporal relation between an event and a time expression is annotated when a time expression is present in the sentence. The temporal relation between an event and the DCT is annotated when this temporal relation is defined in that context. For example, while the relation between *signed* and the DCT is clearly defined, the temporal relation between *fight* and the DCT is not.




```
::id PROXY_AFP_ENG_20020105_0162.15 ::date 2013-05-08T13:37:04 ::snt-type body ::annotator LDC-AMR-14 ::preferred
::snt In April 1998 Arab countries signed an anti-terrorism agreement that binds the signatories to coordinate to fight terrorism.
::save-date Wed Dec 11, 2013 ::file PROXY_AFP_ENG_20020105_0162_15.txt
(s / sign-02
      :ARG0 (c / country
            :mod (e / ethnic-group :wiki "Arabs"
                  :name (n / name :op1 "Arab")))
      :ARG1 (a2 / agree-01
            :topic (c3 / counter-01
                  :ARG1 (t2 / terrorism)
                  :ARG0-of (b / bind-01
                        :ARG1 c
                        :ARG2 (c2 / coordinate-01
                              :ARG1 c
                              :purpose (f / fight-01
                                    :ARG0 c
                                    :ARG1 (t / terrorism))))))
      :time (d / date-entity :year 1998 :month 4)
      :time (b2 /before :op (n/now))
      :aspect Performance))
 ```

In addition to temporal relations at the sentence level, we also annotate temporal relations at the document level.
The document-level temporal relations focus on event-event and time-time relations. Time-time relations are annotated when 
a relative time depends on another time expression for its interpretation


Event-event relations are annotated only when the temporal relations are clearly supported by morpho-syntactic clues or when there is a clear temporal sequence can be inferred. 


<!--
The temporal dependency is divided into two passes: the first pass involves setting up the temporal
superstructure – the top levels of the dependency structure and the fourth
pass involves adding events to the temporal dependency structure. The temporal superstructure contains the temporal expressions (timexs) in the text and pre-defined meta nodes and their temporal relations to each other; the rest of the temporal dependency contains the events and their temporal relations to timexs and other events.

#### Temporal superstructure

The highest level of the temporal
dependency is always a single <span>ROOT</span> node. The temporal
superstructure consists of two types of nodes: time expressions and
pre-defined metanodes. For now at least, <span>Temp</span> is the
relation that is used to link all nodes in the superstructure.

##### Pre-defined metanodes

The first type of node in the temporal superstructure are the
pre-defined metanodes: <span>Past\_Ref, Present\_Ref,
Future\_Ref</span>, and <span>DCT</span> (document creation time).
Unlike time expressions, the pre-defined metanodes don’t correspond to
linguistic material in the text. All four of the pre-defined metanodes
should be added at the top of every temporal dependency structure.
Whether or not they are actually used in the annotation will be
determined when events are annotated in the next pass. As mentioned
above, there is a generic <span>Temp</span> relation between all nodes
in the temporal superstructure; this is shown in Figure
[\[tempsuper\]](#tempsuper).

##### Time expressions

The other type of node in the temporal superstructure are time
expressions. Time expressions are broken down into a taxonomy that
determines their representation in the temporal superstructure (see
Table 1 in Zhang & Xue (2018), reproduced here in Table
[\[timex-taxonomy\]](#timex-taxonomy)).

<table>
<thead>
<tr class="header">
<th style="text-align: center;"></th>
<th style="text-align: center;"><span><strong>Examples</strong></span></th>
<th style="text-align: center;"><span><strong>Possible Reference Times</strong></span></th>
<th style="text-align: center;"></th>
<th style="text-align: center;"></th>
<th style="text-align: center;"></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: center;"></td>
<td style="text-align: center;">Locatable</td>
<td style="text-align: center;"></td>
<td style="text-align: center;">Absolute</td>
<td style="text-align: center;">May 2015</td>
<td style="text-align: center;">ROOT</td>
</tr>
<tr class="even">
<td style="text-align: center;"><p>Time</p></td>
<td style="text-align: center;">Time</td>
<td style="text-align: center;"></td>
<td style="text-align: center;">Relative</td>
<td style="text-align: center;">today, two days later</td>
<td style="text-align: center;">DCT, another Concrete</td>
</tr>
<tr class="odd">
<td style="text-align: center;"><p>Expressions</p></td>
<td style="text-align: center;">Expressions</td>
<td style="text-align: center;"></td>
<td style="text-align: center;">nowadays</td>
<td style="text-align: center;">Present/Past/Future_Ref</td>
<td style="text-align: center;"></td>
</tr>
<tr class="even">
<td style="text-align: center;"></td>
<td style="text-align: center;"></td>
<td style="text-align: center;">every month</td>
<td style="text-align: center;">-</td>
<td style="text-align: center;"></td>
<td style="text-align: center;"></td>
</tr>
</tbody>
</table>

First, time expressions are distinguished based on whether they are
locatable on a timeline or not. Unlocatable time expressions are time
expressions which refer to the duration (*for three hours*) or
quantification (*every day*) of an event. Unlocatable time expressions
are not represented in the temporal dependency structure at any level.
-->

<!-- (they do influence the aspect annotation; see §[3](#aspectannotation)) -->

<!--
All locatable time expressions are represented in the temporal
superstructure. Locatable time expressions are divided between concrete
and vague time expressions. Vague time expressions (e.g. *nowadays, in
the old days*) are represented as the children of <span>Present\_Ref,
Past\_Ref,</span> or <span>Future\_Ref</span>. Concrete time expressions
are divided into relative and absolute time expressions. Relative
concrete time expressions (*yesterday, the week before*) are represented
as the children of either <span>DCT</span> (as in *yesterday*) or
another concrete time expression on which they depend for their
interpretation (as in *the week before*). Finally, absolute concrete
time expressions (*in 2019*) are represented as children of
<span>ROOT</span>.

##### Key events

For news stories only, the temporal superstructure includes the “key
event” in the text. The key event is the main event around which the
news story is centered. It is often mentioned in the title or first
sentence of the news story and referred to many times in the text. The
key event should be added to the superstructure, with a relation to the
timex which most specifically locates it in time.
-->

#### Temporal relations

The second pass in the temporal annotation involves placing events on to the
temporal dependency structure based on their temporal relations with
other events and time expressions. Unlike the modal dependency structure
which includes all of the events identified in the first pass, the
temporal dependency structure only includes events whose aspect
annotation is NOT <span>State</span>. That is, events annotated with the
aspect value <span>State</span> are not annotated for temporal location.
This is because states, by definition, don’t involve change; therefore,
they generally cannot be located on a timeline in the same way as
non-stative events.

Each (non-stative) event will be annotated as the child of either a time
expression in the superstructure or another event (or both). The set of
temporal relations are shown below. Note that the labels characterize
the relation from child to parent.

> <span>Contained</span>: child is entirely contained within the parent;
> parent begins before child and parent ends after child (Note: this is
> called ‘Includes’ in Zhang & Xue 2018)  
> <span>After</span>: child is after parent  
> <span>Before</span>: child is before parent  
> <span>Overlap</span>: child and parent overlap (either partially or
> fully)  

The goal of this temporal annotation scheme is to give each event the
most precise temporal location possible. We also want to avoid adding
annotations which do not give any additional information (i.e., the
relation falls out logically from the other annotations). Annotators
should proceed through the steps below for each event until it has at
least one temporal annotation.

1.  The most specific location for any event will be a
    <span>Contained</span> relation to a timex (although see the
    exception below). If possible, link the event to a time expression
    (timex). This can be any timex in the superstructure, but most of
    the time it will be in the same clause as the event. If the event
    cannot be related to a timex, proceed to 2. If the event is related
    to a timex, proceed to 3.
    
      - **Exception:** The only scenario in which an event, which has a clear temporal
        relation with a timex, doesn’t need to have this relation
        annotated is when the relation logically falls out from other
        annotations. This is the case when an event is a subevent of an
        event that is <span>Contained</span> in a timex. That is, if
        event A is <span>Contained</span> within event B (i.e., a
        subevent) and event B is <span>Contained</span> within a timex,
        then logically, event A must also be <span>Contained</span>
        within the timex and therefore this relation doesn’t need to be
        annotated.

2.  If the event can’t be linked to a timex, then try to link it to
    another event in text. Starting with the immediately preceding event
    in the text and working back through the events in the same sentence
    and the preceding sentence, find an event that is a good parent. If
    there is not a good parent in the same sentence or immediately
    preceding sentence, then proceed to 4. An event is considered a good
    parent if:
    
      - It has a clear temporal relation to the child event AND
    
      - It has a <span>Pos</span> relation to the same conceiver as the
        child event OR
    
      - It has the same modal relation to the same conceiver/event as
        the child event OR
    
      - It is either the parent or the child of the event in the modal
        dependency.
    
      - **Exception:** With reporting constructions, the reporting event
        and reported events can be linked in the temporal dependency
        (even though they are not linked in the modal dependency).

3.  Even if the event can be related to a timex, its temporal location
    may be made more precise by specifying a second relation to an
    event. Only add an event-event relation if it makes the temporal
    location of the child event more specific. In practice, this means
    that events which are <span>Contained</span> within a timex will
    only be related to events <span>Contained</span> within the same
    timex or events which are not contained within any timex. (That is,
    two events <span>Contained</span> within different timexs should not
    be related to each other.) Aside from that, follow the same rules as
    in 2 for selecting a good parent event.

4.  If an event cannot be related to either a timex or another event,
    then relate it to the key event in the text, if there is one.

5.  If an event cannot be related to a timex, another event, or the key
    event, then link it to a tense metanode.

In order to demonstrate how these rules work, let’s look at the
annotation of ([\[leriassaid\]](#leriassaid)) below.

<span id="leriassaid" label="leriassaid">\[leriassaid\]</span> *Lerias
**said** that many Guinsaugon residents had been **evacuated** after
**landslides** had **killed** more than 20 people on Leyte, but that
many had **returned** because the **rains** had **stopped** and the sun
had **come out**.*  
Key event: landslide\_KEY


 ::id NW_AFP_ENG_0024_2006_0217.16 ::date 2017-11-03T23:39:57 ::annotator SDL-AMR-09 ::preferred
 ::snt Lerias said that many Guinsaugon residents had been evacuated after landslides earlier in the week had killed more than 20 people on Leyte, but that many had returned Friday because the rains had stopped and the sun had come out.
 ::save-date Thu Dec 14, 2017 ::file NW_AFP_ENG_0024_2006_0217_16.txt
```
(s / say-01
      :ARG0 (p / person :wiki -
            :name (n / name :op1 "Lerias"))
      :ARG1 (e / evacuate-01
            :ARG2 (p2 / person
                  :ARG0-of (r / reside-01
                        :ARG1 (c / city :wiki "Saint_Bernard,_Southern_Leyte"
                              :name (n2 / name :op1 "Guinsaugon")))
                  :quant (m / many))
            :time (a / after
                  :op1 (k / kill-01
                        :ARG0 (l / landslide)
                        :ARG1 (p3 / person
                              :quant (m2 / more-than :op1 20))
                        :location (i2 / island :wiki "Leyte"
                              :name (n3 / name :op1 "Leyte"))
                        :time (w / week)
                        :time (b / before
                              :op1 s)))
            :concession (r2 / return-01
                  :ARG1 p2
                  :time (d / date-entity
                        :weekday (f / friday))
                  :ARG1-of (c2 / cause-01
                        :ARG0 (a2 / and
                              :op1 (s2 / stop-01
                                    :ARG1 (r3 / rain-01))
                              :op2 (c3 / come-out-09
                                    :ARG1 (s3 / sun)))))))
```


| Events    | Modal annotation      | Temporal annotation |
| :-------- | :-------------------- | :------------------ |
| say       | Pos(say,AUTH)         |                     |
| evacuate  | Pos(evacuate,LERIAS)  |                     |
| landslide | Pos(landslide,LERIAS) |                     |
| kill      | Pos(kill,LERIAS)      |                     |
| return    | Pos(return,LERIAS)    |                     |
| rain      | Pos(rain,LERIAS)      |                     |
| stop      | Pos(stop,LERIAS)      |                     |
| come-out  | Pos(come-out,LERIAS)  |                     |

For *say*, it does not have a **Contained** relation
with either of the time expressions in the example, so we move to step
2. It’s also the first event in the sentence, so (assuming it can’t be
linked to any of the events in the previous sentence), we move to step
4. We do know that *say* occurred after the key event in the
text, therefore we can add *After(say,landslide\_KEY)* and
move on to the next event.

*Evacuate* is not necessarily **Contained** within
either of the timexs, so we move to step 2. Since *evacuate*
is a reported event, the reporting event, *say*, is an
appropriate parent in the temporal dependency; we can add
*Before(evacuate,say).*

Next, we have *landslide*. Following step 1,
*landslide* is **Contained** within the timex
*earlier in the week*, so we add
*Contained(landslide,earlier\_week)*. Then, we move to step 3
and see if the temporal location of *landslide* can be made
more specific by adding an event relation. The immediately preceding
event in the text, *evacuate*, has a clear temporal relation
and the same modal annotation as *landslide* and is therefore
a good parent. We can add *Before(landslide,evacuate)*.

Then, we move on to *kill*. Like *landslide*,
*kill* is **Contained** within the timex *earlier in
the week*, so we can add *Contained(kill,earlier\_week)*.
Then we move to step 3 and can add a relation to *landslide*:
*Overlap(kill,landslide)*.

*Return* can be linked to the timex *Friday*:
*Contained(return,Friday)*. Moving to step 3, we look earlier
in the sentence for a parent event. Both *kill* and
*landslide* are Contained within a different timex, so they
don’t make good parents. That is, by virtue of the fact that
*return* is **Contained** on *Friday* and
*kill* and *landslide* are **Contained**
in *earlier in the week*, it logically falls out that
*return* happened after both *kill* and
*landslide*; therefore, we don’t need to annotate this
relation. *Evacuate*, however, is not **Contained**
within a timex and has the same modal annotation as *return*;
so, we can add *After(return,evacuate)*.

*Rain* does not have a **Contained** relation with a
timex, so we move to step 2. *Return* makes a good parent for
*rain* since it has the same modal annotation, so we can
add  
*Before(rain,return)*.

*Stop* also does not have a **Contained** relation
with a timex. The preceding event, *rain*, makes a good
parent, since it has the same modal annotation; we can add
*Overlap(stop,rain)*.

Finally, *come-out* also does not have a
<span>Contained</span> relation with a timex. *Stop* makes a
good parent, since it has the same modal annotation, so we can add
*Overlap(come-out,stop)*. This gives us the full annotation
below.

| Events    | Modal annotation   | Temporal annotation                |
| :-------- | :----------------- | :--------------------------------- |
| say       | Pos(say,LERIAS)    | After(say,landslide\_KEY)          |
| evacuate  | Pos(evacuate,say)  | Before(evacuate, say)              |
| landslide | Pos(landslide,say) | Contained(landslide,earlier\_week) |
|           |                    | Before(landslide,evacuate)         |
| kill      | Pos(kill,say)      | Contained(kill,earlier\_week)      |
|           |                    | Overlap(kill,landslide)            |
| return    | Pos(return,say)    | Contained(return,Friday)           |
|           |                    | After(return,evacuate)             |
| rain      | Pos(rain,say)      | Before(rain,return)                |
| stop      | Pos(stop,say)      | Overlap(stop,rain)                 |
| come-out  | Pos(come-out,say)  | Overlap(come-out,stop)             |

##### Contained or Overlap

Following the definition of the <span>Contained</span> and the
<span>Overlap</span> relations, <span>Overlap</span> must be used rather
than <span>Contained</span> for events that are perfectly simultaneous
(beginning and ending at the exact same time point). The
<span>Contained</span> relation will instead be used for all relations
where both the beginning and ending of one event are included within the
temporal duration of a second event - this includes subevent structure
and also events which have a purely temporal (and not causal or
conceptual) relation between them.

##### Causally related events

Causal relations between events are always annotated as
<span>After</span> relations. This means that in examples such as *the
crops grew well because it rained enough*, <span>After(grow,rain)</span>
is annotated even though the causing event (raining) and the caused
event (growing) partly overlap. If the causal relationship is explicitly
predicated, it is identified as a separate event. It is then annotated
as <span>After</span> the causing event, and the caused event is
annotated as following it. Therefore, *the opening of the food can
prompted my cat to meow* is annotated as <span>After(prompt,open)</span>
and <span>After(meow,prompt)</span>.

##### Deontic modal events

For deontics and purpose clauses, the deontic or purpose complement
(e.g., *go* in *Mary wants to go*) is annotated with with an
<span>After</span> relation to the deontic predicate (here, *want*).
This is important because it makes sure that events can be interpreted
as deontically modalized - the modal annotation scheme itself does not
provide for this.





<!-- 1.  The term “event” is used throughout these guidelines as a
    superordinate category subsuming processes and states, as is
    customary in the cognitive linguistic tradition. The more specific
    category of telic processes (which is also often called “event” in
    the formal semantics literature), we will refer to as “performance”
    (see §[3](#aspectannotation)). 2.  We are considering using the <span>NA</span> value for non-real
    events as well, but for now, these types of events should receive
    one of the other aspect values. -->

### Part 4-3. Modal Dependency

The modal strength annotation takes the form of a dependency structure:
each event receives an annotation which indicates which linguistic
material it depends on for its modal interpretation, and what type of
dependency relation holds between the parent and the child. That is, the
nodes in the dependency structure are linguistic expressions (either
events or modal conceivers) and the edges represent modal (epistemic)
strength.

In the modal strength dependency structure, there are three types of
nodes: events identified in the first pass, modal conceivers (akin to
sources), and the <span>have-condition</span> node for conditional
events. The second pass involves identifying the conceivers in the text,
adding the <span>have-condition</span> node if applicable, and creating
the dependency structure using those nodes and the events identified in
the first pass. This is done in a single pass through the document.

#### Part 3-3-1. Identifying conceivers

##### Part 3-3-1-1. Author(s)

Every text will have at least one <span>AUTH</span> node, used for the
author(s) of the document. When there are multiple authors (for example,
in a discussion forum, or in a transcript of an interview) each author
will get their own node. It is necessary to add a node for each author
because all of the content in a document is filtered through an author’s
(or speaker’s) perspective.

##### Part 3-3-1-2. Conceivers other than author(s)

Aside from authors, there are nodes in the modal strength dependency for
conceivers mentioned in the document; these correspond to sources in
FactBank. All non-author conceivers are dependent on the author
node(s) because everything in the text is ultimately from the author’s
perspective.

Conceiver nodes are added when another entity’s mental attitude or point
of view towards an event is expressed in the text. Certain types of
predicates inherently involve conceivers/sources: report, knowledge,
belief, opinion, doubt, perception, and inference. The examples below
in [\[47\]](#conceivers) show some of the types of predicates
that require the introduction of a conceiver node into the modal
strength dependency structure.

<span id="conceivers" label="conceivers">\[47\]</span>

<span id="Marythinks" label="Marythinks">\[a\]</span> *Mary
<u>thinks</u> that John **mowed** the lawn.*  
<span>AUTH</span>  
<span>MARY</span>

<span id="NYTreportedinquiry" label="NYTreportedinquiry">\[b\]</span>
*The New York Times <u>**reported**</u> that the impeachment **inquiry**
has begun.*  
<span>AUTH</span>  
<span>NEW\_YORK\_TIMES</span>

<span id="perception" label="perception">\[c\]</span> *John
<u>**saw**</u> the cat **eat** breakfast.*  
<span>AUTH</span>  
<span>JOHN</span>

<span id="deonticevent" label="deonticevent">\[d\]</span>
*Mary <u>**hopes**</u> to **leave** early.*  
<span>AUTH</span>  
<span>MARY</span>

<span id="deonticnominal" label="deonticnominal">\[e\]</span>
*John really <u>**wanted**</u> a boat.*  
<span>AUTH</span>  
<span>JOHN</span>

<span id="deonticoblig" label="deonticoblig">\[f\]</span>
*The university <u>**requires**</u> Mary to **register** by Monday.*  
<span>AUTH</span>  
<span>UNIVERSITY</span>

<span id="purpclausecon" label="purpclausecon">\[g\]</span>
*Mary is **going** to California <u>in order to</u> **see** the
beach.*  
<span>AUTH</span>  
<span>MARY</span>

As mentioned above, every example (or document) requires the
introduction of an <span>AUTH</span> node. Predicates of belief, as in
[\[47a\]](#Marythinks), also require the addition of a conceiver
node for the believer, here <span>MARY</span>. This is necessary in
order to capture the fact that the modal strength of the
<span>mow</span> event is provided by Mary and the author may or may not
agree with Mary’s perspective. Similarly, predicates of reporting, as in
[\[47b\]](#NYTreportedinquiry), and perception, as in
[\[47c\]](#perception), require the introduction of conceiver
nodes for the reporter (<span>NEW\_YORK\_TIMES</span>) and the perceiver
(<span>JOHN</span>).

Certain deontic events, such as those in
[\[47d\]](#deonticevent) and
[\[47e\]](#deonticnominal) also require the addition of a
conceiver node to the dependency structure. Hopes, wishes, desires, and
fears all model the mental content of a conceiver in the text – these
are based on a conceiver’s beliefs or perspective about the world.
Conceiver nodes should be added, even when the complement of the deontic
predicate isn’t an event, as in [\[47e\]](#deonticnominal).
Obligation deontics, as in [\[47f\]](#deonticoblig), require
the introduction of a conceiver node for the source of the obligation
(here, <span>JOHN</span>), but not the endpoint of the obligation
(<span>MARY</span>). This is because, in
[\[47f\]](#deonticoblig), nothing is asserted about Mary’s
beliefs, desires, attitude or perspective.

Purpose clauses, as in [\[47g\]](#purpclausecon), require the
introduction of a conceiver node for the subject of the sentence; this
is because the author is expressing the intentions of the subject of the
sentence.

As shown by [\[47b\]](#NYTreportedinquiry), conceivers
can be inanimate entities when they metonymically refer to a volitional
entity (or volitional entities); that is, the
<span>NEW\_YORK\_TIMES</span> node stands for the people who contribute
to the newspaper.

It’s important to point out that conceivers don’t actually represent
individuals in the text, but their sets of beliefs. That is, the
<span>MARY</span> conceiver node doesn’t correspond to the entity named
*Mary* in the document; it stands for a set of Mary’s beliefs as
presented by the author of the text. This means that there may be
multiple conceiver nodes for a single individual’s beliefs. This occurs
under two different circumstances: when the conceiver nodes are nested
underneath different other conceiver nodes in the dependency structure
as in [\[48a\]](#diffcon), and when they’re nested underneath the
same conceiver node, but with a different modal strength value as in
[\[48b\]](#diffstrength).

<span id="multconnodes" label="multconnodes">\[48\]</span>

<span id="diffcon" label="diffcon">\[a\]</span> *John
<u>**said**</u> Mary <u>**wants**</u> to **visit** Italy, but I
<u>think</u> she <u>**wants**</u> to **visit** France.*  
<span>AUTH</span>  
<span>JOHN</span>  
<span>MARY\_1</span>  
<span>MARY\_2</span>

<span id="diffstrength" label="diffstrength">\[b\]</span>
*Mary <u>**wants**</u> to **visit** Italy and she <u>might **want**</u>
to **visit** France as well.*  
<span>AUTH</span>  
<span>MARY\_1</span>  
<span>MARY\_2</span>

In [\[48a\]](#diffcon), we need two separate <span>MARY</span>
nodes: one which is dependent on the <span>JOHN</span> node to represent
John’s beliefs about Mary’s beliefs (really, the author’s beliefs about
John’s beliefs about Mary’s beliefs) and one which is nested directly
underneath the <span>AUTH</span> node to represent the author’s beliefs
about Mary’s beliefs. In [\[48b\]](#diffstrength), there are
two separate <span>MARY</span> nodes that correspond to the author’s
different levels of certainty about Mary’s sets of beliefs. One of the
<span>MARY</span> nodes represents Mary’s set of beliefs that the author
is certain of (her desire to visit Italy) and the other
<span>MARY</span> node represents Mary’s beliefs that the author is
unsure of (her desire to visit France).

##### Part 3-3-1-3. Shared beliefs

Authors may also attribute beliefs to groups of individuals. In these
cases, separate conceiver nodes should be created for each unique group
of individuals; these groups may (or may not) include the author. This
can be seen below in ([\[49\]](#sharedconceivers)).

<span id="sharedconceivers" label="sharedconceivers">\[49\]</span>

*Mary and I <u>think</u> that John **left** early. Mary was
<u>**surprised**</u> that John **left** because they had
<u>**planned**</u> to **get** pizza later.*  
<span>AUTH</span>  
<span>MARY\_AUTH</span>  
<span>MARY</span>  
<span>MARY\_JOHN</span>

Here, there is a node for the author because all examples require an
<span>AUTH</span> node. The <span>MARY\_AUTH</span> node represents the
shared beliefs of Mary and the author (namely, that John left the event
early); the <span>MARY</span> node is required because *surprise* models
Mary’s mental content. And the <span>MARY\_JOHN</span> node represents
Mary and John’s shared belief about their pizza plans.

##### Part 4-3-1-4. Generic and unspecified conceivers

Sometimes, conceivers need to be identified even when they aren’t
explicitly mentioned in the text, as in [\[50\]](#genericcon).

<span id="genericcon" label="genericcon">\[50\]</span>

<span id="prohibit" label="prohibit">\[a\]</span> *My **request**
was <u>**heard**</u>.*  
<span>AUTH</span>  
<span>NULL\_HEARER</span>

<span id="report" label="report">\[b\]</span> *It has been
<u>**reported**</u> that multiple roads are **closed**.*  
<span>AUTH</span>  
<span>NULL\_REPORTER</span>

This is often the case when predicates that introduce conceivers are
used in passive constructions. Even though there is no span of text that
represents the conceivers, they should still be identified as nodes in
the dependency structure.

Unlike perception events and reporting events, obligation deontics, as
in [\[51\]](#deonticnocon), don’t require the introduction of
a null conceiver node.

<span id="deonticnocon" label="deonticnocon">\[51\]</span>
*Mary <u>has</u> to **register** by Monday.*  
<span>AUTH</span>

When the source of obligation is expressed (as shown above in
[\[47f\]](#deonticoblig)), a conceiver node is introduced for
the source of the obligation. It is not always clear, however, that an
external source is present when it is not overtly expressed. Therefore,
null conceivers are not identified for obligation deontics.

#### Part 4-3-2. The <span>have-condition</span> node

The <span>have-condition</span> node is a special node that is required
in the modal strength dependency structure for linguistic material that
expresses hypothetical situations contingent on certain conditions. The
canonical English conditional construction is shown below in
[\[52\]](#canoncond).

<span id="canoncond" label="canoncond">\[52\]</span>

*If it **rains**, Mary will **stay** home.*  
<span>have-condition</span>

Here, the hypothetical situation, Mary staying home, is conditional on
the raining event. The UMR annotation does not capture the causal
relation between the <span>rain</span> event and the <span>stay</span>
event; this may be annotated elsewhere in the UMR annotation scheme. The
UMR modal strength annotation captures the fact that both of these
events occur in the same hypothetical scenario – these are not two
independent hypothetical events. The <span>have-condition</span> node
acts a parent to both the <span>rain</span> event and the
<span>stay</span> event in the modal strength dependency. This captures that the events in
the conditional construction occupy the same hypothetical “world” or
space and not separate hypothetical worlds/spaces.

Conditional constructions may take a variety of morphosyntactic forms,
both across languages and within a language. Although the canonical
English conditional construction takes the *if.., then...* form, there
are are other ways to express conditional semantics, such as those in
[\[53\]](#otherconds) below.

<span id="otherconds" label="otherconds">\[53\]</span>

<span id="longas" label="longas">\[a\]</span> *As long as it
**rains**, Mary will **stay** home.*  
<span>have-condition</span>

<span id="casethat" label="casethat">\[b\]</span> *Mary will
**stay** home, in (the) case (that) it **rains**.*  
<span>have-condition</span>

Regardless of the form, the conditional semantics requires the
introduction of the <span>have-condition</span> node.

The <span>have-condition</span> node is also used for different types of
conditionals and constructions related to conditionals. The
<span>have-condition</span> node is also required for counterfactuals,
as in [\[54a\]](#counterfactualrain), and concessive
conditionals, as in [\[54b\]](#concess).

<span id="otherconds" label="otherconds">\[54\]</span>

<span id="counterfactualrain" label="counterfactualrain">\[a\]</span>
*If it had **rained**, Mary would have **stayed** home.*  
<span>have-condition</span>

<span id="concess" label="concess">\[b\]</span>
*Even if it had **rained**, Mary would have **stayed** home.*  
<span>have-condition</span>

These types of constructions will be annotated differently in terms of
their modal strength values,
but they all require the introduction of a <span>have-condition</span>
node.

#### Part 4-3-3. Constructing the modal strength dependency structure

The different types of nodes in the modal strength dependency structure
have been covered in the previous sections: authors, conceivers,
<span>have-condtion</span>, and the events identified in the first pass.
There is one other node in the dependency structure: a <span>ROOT</span>
node, under which all other nodes are nested. This section covers the modal strength values that characterize the
edges and guidelines on how to construct the dependency structure.

Every document will have a single <span>ROOT</span> node at the top of
the dependency structure. All <span>AUTH</span> nodes are direct
children of the <span>ROOT</span> node and only <span>AUTH</span> nodes
can be direct children of the <span>ROOT</span> node. That is,
non-author conceivers and events will never be direct children of the
<span>ROOT</span> node. This is because any and all information in a
document is presented from (one of) the author’s perspective(s).

<span>AUTH</span> nodes may have either events, conceivers, or
<span>have-condition</span> nodes as their direct children. This reflect
the fact that authors may give their own perspective on an event or
model another conceiver’s perspective on an event. Non-author conceivers
should always be direct children of an <span>AUTH</span> node or another
non-author conceiver node; that is, a conceiver node will never have an
event node as its parent.

##### Part 4-3-3-1. Overview of modal strength edges

As has been stated above, the edges in the modal strength dependency
correspond to modal strength values. The same edge labels are used at
all levels of the dependency structure, with the exception of the link
between the <span>ROOT</span> and <span>AUTH</span> node(s). This edge
label is always <span>Modal</span>.

Modal strength values correspond to epistemic strength, i.e. the author
or conceiver’s certainty about the occurrence of the event in the real
world, or certainty about another conceiver’s mental content. Based on ,
a typological study of modal systems across languages, and following
FactBank (), the UMR annotation distinguishes three levels of modal
strength: Full, Partial, and Neutral, illustrated in
[\[55\]](#modalvalues).

<span id="modalvalues" label="modalvalues">\[55\]</span>

<span id="full" label="full">\[a\]</span> Full:  
*The cat already **ate** breakfast.*

<span id="partial" label="partial">\[b\]</span>
Partial:  
*The cat <u>probably</u> already **ate** breakfast.*

<span id="neutral" label="neutral">\[c\]</span>
Neutral:  
*The cat <u>might</u> have already **eaten** breakfast.*

The Full modal strength value, as in [\[55a\]](#full), corresponds to
complete certainty; that is, the conceiver is 100% certain that the
event occurs in the real world. The Neutral modal strength value, shown
in [\[55c\]](#neutral), indicates the possibility of the event;
essentially, this corresponds to 50/50 certainty that the event occurs
in the real world. The Partial modal strength value, as in
[\[55b\]](#partial), falls between the Full and Neutral values; the
conceiver believes that more likely than not, the event occurs in the
real world.

Also following FactBank, the UMR annotation combines the three-way
epistemic strength distinction (Full, Partial, Neutral) with a binary
polarity distinction (Affirmative, Negative). This results in six modal
strength values shown below.

<div id="introvalues">

| Label                                  | Value                                  |
| :------------------------------------- | :------------------------------------- |
| <span class="smallcaps">aff</span>     | full strength, affirmative polarity    |
| <span class="smallcaps">prt</span>     | partial strength, affirmative polarity |
| <span class="smallcaps">neut</span>    | neutral strength, affirmative polarity |
| <span class="smallcaps">neutneg</span> | neutral strength, negative polarity    |
| <span class="smallcaps">prtneg</span>  | partial strength, negative polarity    |
| <span class="smallcaps">neg</span>     | full strength, negative polarity       |

</div>

The following sections will show how these edge values are applied to
different types of nodes in the modal strength dependency structure.
Throughout these sections, the format <span>Edge(Child node,Parent
node)</span> will be used to represent the dependency structure.

##### Part 4-3-3-2. Edges between conceiver nodes

As mentioned above, the edge between the <span>ROOT</span> and the
<span>AUTH</span> is always <span>Modal</span> and does not take one of
the modal strength values shown above. Every
other edge in the modal strength dependency, however, is characterized
by the modal strength values.

For edges between two conceiver nodes, these values represent the degree
of confidence a conceiver has in modelling the contents of another
conceiver’s set of beliefs. That is, the author (or another conceiver)
may have different levels of confidence about whether or not a
particular individual holds the set of beliefs represented by a
conceiver node. Examples for each of the six possible edges values is
shown below.

<div id="conceiveredge">

| Annotation                      | Example                                                 |
| :------------------------------ | :------------------------------------------------------ |
| <span>Aff(MARY,AUTH)</span>     | *Mary believes the cat **ate**.*                        |
| <span>Prt(MARY,AUTH)</span>     | *Mary <u>probably</u> believes the cat **ate**.*        |
| <span>Neut(MARY,AUTH)</span>    | *Mary <u>might</u> believe the cat **ate**.*            |
| <span>NeutNeg(MARY,AUTH)</span> | *Mary <u>might not</u> believe the cat **ate**.*        |
| <span>PrtNeg(MARY,AUTH)</span>  | *Mary <u>probably doesn’t</u> believe the cat **ate**.* |
| <span>Neg(MARY,AUTH)</span>     | *Mary <u>doesn’t</u> believe the cat **ate**.*          |

</div>

For example, in *Mary might believe the cat ate*, the author is unsure
whether or not Mary holds the belief about the eating event. Therefore,
there is a <span>Neut</span> relation between the <span>AUTH</span> node
and the <span>MARY</span> conceiver node.

Note that this edge captures the author (or parent conceiver) node’s
certainty about the set of beliefs of the child conceiver node. That is,
it is not capturing the child conceiver’s certainty about the event in
question. Generally, when a predicate that introduces a conceiver is
modalized, the strength indicated by the modal is annotated between the
conceiver nodes, as in [\[56\]](#deonticcon).

<span id="deonticcon" label="deonticcon">\[56\]</span>

<span id="think" label="think">\[a\]</span> *Mary thinks the cat
might have **eaten** breakfast.*  
<span>Aff(MARY,AUTH)</span>

<span id="doubt" label="doubt">\[b\]</span> *Mary probably doubts
that the cat **ate** breakfast.*  
<span>Prt(MARY,AUTH)</span>

In [\[56a\]](#think), Mary is uncertain about the eating event, but
there is a <span>Aff</span> edge between the <span>AUTH</span> and
<span>MARY</span> nodes because the author is sure of Mary’s beliefs.
In [\[56b\]](#doubt), the author only has probable certainty about
Mary’s beliefs, annotated with the <span>Prt</span> edge between the
<span>AUTH</span> and <span>MARY</span> nodes.

##### Part 4-3-3-3. Edges involving event nodes

The same set of six epistemic strength values are used for edges that
involve events; there are also two additional unspecified values. This
section covers the edges between conceivers and events and between two
events (the parental options for events in the modal strength dependency
structure are fairly limited by the semantics of the text, but see
section [\[parentnodes\]](#parentnodes) on selecting appropriate parent
nodes). The eight values and their interpretation for events nodes are
shown below. The corresponding FactBank values are shown in parentheses.

<span>Aff</span>: full affirmative support; complete certainty that
the event occurs (CT+)  
<span>Prt</span>: partial affirmative support; there is strong, but
not definitive certainty that the event occurs (CR+)  
<span>Neut</span>: affirmative neutral support; there is neutral
certainty that the event occurs/doesn’t occur; event is expressed
positively (PS+)  
<span>NeutNeg</span>: negative neutral support; there is neutral
certainty that the event occurs/doesn’t occur; negation of event is
expressed (PS-)  
<span>PrtNeg</span>: partial negative support; there is strong but not
definitive certainty that the event does not occur (PR-)  
<span>Neg</span>: full negative support; complete certainty that the
event does not occur (CT-)  
<span>Unsp</span>: The conceiver knows that the event either did or
did not occur, but is uncertain about the polarity (CTu)  
<span>NegUnsp</span>: The conceiver does not know what the factual
status of the event is, or does not commit to it (Uu)

Degree of certainty corresponds most straightforwardly to the degree of
confidence of a conceiver in the occurrence of an episodic event, i.e.
the epistemic/evidential continuum from certainty to possibility and
from direct evidence to second-hand (reported or inferred) evidence. We
use the same values for epistemic/evidential support and deontic
modality. The interpretation of the value - as epistemic/evidential or
deontic - is not reflected in the modal strength annotation.

###### Part 4-3-3-3-1. Non-future events

For non-future (non-deontic) events, the strength values correspond to
the conceiver’s level of certainty towards the occurrence of the event
in the real world. Events presented as fact by a conceiver will be
annotated with <span>Aff</span>, while events for which the conceiver
categorically denies their occurrence are marked <span>Neg</span>. When
the conceiver doesn’t present the event as fact, but has a higher level
of certainty towards the event either being true or not true, this is
annotated as partial strength (<span>Prt</span> or, when the polarity is
negative, <span>PrtNeg</span>). When the conceiver doesn’t lean either
direction towards the event being true in the real world or not, the
event is annotated as neutral (<span>Neut</span> or
<span>NeutNeg</span>, depending on the polarity of the linguistic
expression). This system of annotation is why predicates such as *think*
or *believe* are not annotated as event nodes: they correspond exactly
to the edges between conceivers and events. These strength values are
exemplified in ([\[57\]](#episodic)).

<span id="episodic" label="episodic">\[57\]</span>

<span id="anaphora" label="anaphora">\[a\]</span> *The dog
**barked** last night*.  
<span>Aff(bark,AUTH)</span>

<span id="anaphora" label="anaphora">\[b\]</span> *The dog
<u>probably</u> **barked** last night.*  
<span>Prt(bark,AUTH)</span>

<span id="anaphora" label="anaphora">\[c\]</span> *The dog
<u>may</u> have **barked** last night.*  
<span>Neut(bark,AUTH)</span>

<span id="anaphora" label="anaphora">\[d\]</span> *The dog <u>may
not</u> have **barked** last night.*  
<span>NeutNeg(bark,AUTH)</span>

<span id="anaphora" label="anaphora">\[e\]</span> *The dog
<u>probably didn’t</u> **bark** last night.*  
<span>PrtNeg(bark,AUTH)</span>

<span id="anaphora" label="anaphora">\[f\]</span> *The dog
<u>didn’t</u> **bark** last night.*  
<span>Neg(bark,AUTH)</span>

###### Part 4-3-3-3-2. Future events and deontic modality

For events embedded in deontic modals, or presented as (potentially)
happening in the future, modal strength refers to the predictability of
the occurrence of the event in the future, as presented by the
conceiver. Predictive future has full strength (<span>Aff</span> or
<span>Neg</span>); intentions, commands, and purpose clauses correspond
to partial strength (<span>Prt</span> or <span>NegPrt</span>); and
desire and permission correspond to neutral (<span>Neut</span> or
<span>NeutNeg</span>) strength. This is illustrated in
([\[58\]](#futurestrength)).

<span id="futurestrength" label="futurestrength">\[58\]</span>

<span id="futpos" label="futpos">\[a\]</span> *I <u>will</u> **go**
to Santa Fe*.  
<span>Aff(go,AUTH)</span>

<span id="futprt" label="futprt">\[b\]</span> *I <u>**intend**</u>
to **go** to Santa Fe. / You <u>must</u> **go** to Santa Fe.* / *I’m
getting my car **fixed** <u>in order to</u> **go** to Santa Fe.*  
<span>Prt(go,AUTH)</span>

<span id="futneut" label="futneut">\[c\]</span> *I <u>**want**</u>
to **go** to Santa Fe. / You are <u>**allowed**</u> to **go** to Santa
Fe.*  
<span>Neut(go,AUTH)</span>

The predictive future, as in [\[58a\]](#futpos), is annotated with
full modal strength because it presents the future event as a certainty
(i.e., it is as certain as is possible for future events). Intentions,
commands, and purpose clauses, as in [\[58b\]](#futprt), are
annotated with partial modal strength because they present the future
event as less likely than the predictive future, but more likely to
happen than the neutral strength deontics. Finally, desire and
permission, as in [\[58c\]](#futneut), are annotated as neutral
strength.

Examples like [\[59\]](#futuretests) demonstrate how the
predictive future, intention, and desire present events with different
future likelihoods, based on whether or not they’re compatible with
different strength negatives of the same event.

<span id="futuretests" label="futuretests">\[59\]</span>

<span id="futtestpos" label="futtestpos">\[a\]</span> *\*I will
go to Santa Fe, but I won’t go.*  
*\*I will go to Santa Fe, but I probably won’t go.*  
*\*I will go to Santa Fe, but I might not go.*

<span id="futtestprt" label="futtestprt">\[b\]</span> *\*I
intend to go to Santa Fe, but I won’t go.*  
*\*I intend to go to Santa Fe, but I probably won’t go.*  
*I intend to go to Santa Fe, but I might not go.*

<span id="futtestneut" label="futtestneut">\[c\]</span> *I
want to go to Santa Fe, but I won’t go.*  
*I want to go to Santa Fe, but I probably won’t go.*  
*I want to go to Santa Fe, but I might not go.*

The predictive future, as in [\[59a\]](#futtestpos), can’t
combine with any strength of negative. This is because full affirmative
strength doesn’t allow for any uncertainty, or any possibility that the
event does not occur. The partial strength future/deontic events, like
intention as in [\[59b\]](#futtestprt), are only compatible with
a neutral strength negative of the same event. Partial strength allows
for the possibility that the event won’t occur in the future, but can’t
occur with the partial (or full) strength negative of the event. Neutral
strength future/deontics, like desires as in
[\[59c\]](#futtestneut), can occur with any strength negative of
the same event, since the event is only presented as a possibility.

Modalized deontic predicates capture
the modal value with the link between the <span>AUTH</span> and the
conceiver node. This means that the link between a conceiver and the
node for the deontic predicate is very often a default <span>Aff</span>
value; see example ([\[60\]](#defaultpos)).

<span id="defaultpos" label="defaultpos">\[60\]</span> *Mary
<u>might</u> **want** to **visit** France.*  
<span>Neut(MARY,AUTH)</span>  
<span>Aff(want,MARY)</span>  
<span>Neut(visit,want)</span>

This is because the link between a conceiver and the deontic predicate
represents the modal strength of the event with respect to the
conceiver, and not the author. That is, the author is unsure of Mary’s
desires; the author is not asserting that Mary is unsure of her own
desires.

When the conceiver is unsure of their own beliefs, desires, etc., this
is represented with the link between the conceiver and the deontic
predicate, as in ([\[61\]](#mightwant)).

<span id="mightwant" label="mightwant">\[61\]</span>

*Mary <u>thinks</u> that she <u>might</u> **want** to **visit**
France.*  
<span>Aff(MARY,AUTH)</span>  
<span>Neut(want,MARY)</span>  
<span>Neut(visit,want)</span>

Here, the author is sure of Mary’s beliefs, so there is a
<span>Aff</span> link between the author and Mary’s set of beliefs. But,
Mary herself is unsure of her desire to visit France; therefore, there
is a <span>Neut</span> link between the <span>MARY</span> node and the
<span>want</span> node.

###### Part 4-3-3-3-3. Interaction of modal strength and negation

Since the modal strength edges combine both epistemic strength and
polarity, the interaction of negation (polarity) and epistemic strength
within a construction requires further annotation guidelines. As is the
case with the UMR annotation scheme in general, it is important to
annotate the meaning of the text, regardless of its morphosyntactic
form. For example, certain constructions in English exhibit what is
often called neg-raising, as in [\[62a\]](#negraise1).

<span id="negraisethink" label="negraisethink">\[62\]</span>

<span id="negraise1" label="negraise1">\[a\]</span> *Mary
<u>doesn’t think</u> John **is in** his office.*  
<span>Aff(MARY,AUTH)</span>  
<span>Neg(be-in,MARY)</span>

<span id="negraise2" label="negraise2">\[b\]</span> *Mary
<u>thinks</u> John **isn’t in** his office.*  
<span>Aff(MARY,AUTH)</span>  
<span>Neg(be-in,MARY)</span>

Although the negation in [\[62a\]](#negraise1) is syntactically on
*think*, the meaning of [\[62a\]](#negraise1) and
[\[62b\]](#negraise2) is the same. That is, that Mary has a belief
that John is in not in his office. Therefore, both of these have the
same annotation, with the negation represented between the
<span>MARY</span> node and the <span>be-in</span> node. Further examples
of this can be seen below in [\[63\]](#negraise).

<span id="negraise" label="negraise">\[63\]</span>

<span id="POS" label="POS">\[a\]</span> *Mary <u>doesn’t</u> **want**
to **go**. / Mary **wants** <u>not</u> to **go**.*  
<span>Aff(MARY,AUTH)</span>  
<span>Aff(want,MARY)</span>  
<span>NeutNeg(go,want)</span>

<span id="NEUT" label="NEUT">\[b\]</span> *Mary <u>isn’t</u>
**planning** on **going**. / Mary is **planning** to <u>not</u>
**go**.*  
<span>Aff(MARY,AUTH)</span>  
<span>Aff(plan,MARY)</span>  
<span>PrtNeg(go,plan)</span>

Note that only certain predicates allow neg-raising in English (e.g.,
*believe, think, want, plan*); other predicates (e.g., *know*) have
different meanings depending on the syntactic location of the negation.

When negation interacts with highly grammaticalized modals, this is
invariably represented with the negation inside the scope of the modal
(again, regardless of where the negation is syntactically). Since
grammaticalized modals aren’t identified as their own event (i.e.,
node), the strength of the grammaticalized modal and the negation must
be annotated with a single edge. This amounts to combining the strength
of the modal (i.e., partial or neutral) with the negative polarity
(<span>PrtNeg</span> or <span>NeutNeg</span>). This can be seen in
example ([\[64\]](#combo)) below.

<span id="combo" label="combo">\[64\]</span>

<span id="POS" label="POS">\[a\]</span> *Mary <u>doesn’t have</u> to
**go**. / Mary <u>could</u> (choose to) <u>not</u> **go**.*  
<span>NeutNeg(go,AUTH)</span>

<span id="NEUT" label="NEUT">\[b\]</span> *Mary is <u>unlikely</u> to
**go**. / Mary is <u>likely not</u> to **go**.*  
<span>NegPrt(go,AUTH)</span>

<span id="NEUT" label="NEUT">\[c\]</span> *Mary <u>mustn’t/shouldn’t</u> **open** the box. / <u>It is required</u>
that Mary <u>not</u> **open** the box.*  
<span>NegPrt(open,AUTH)</span>

<span id="NEUT" label="NEUT">\[d\]</span> *He <u>might not</u> **be in** his office. / <u>It is possible</u> that
he **is** <u>not</u> **in** his office.*  
<span>NeutNeg(be-in,AUTH)</span>

There are also cases where the modal strength value of the edge is not a
straightforward combination of the modal strength and negation. Examples
of these can be seen below in ([\[65\]](#notcombo)).

<span id="notcombo" label="notcombo">\[65\]</span>

<span id="POS" label="POS">\[a\]</span> *<u>It is not possible</u> for
Mary **to be** in France already.*  
<span>Neg(be-in,AUTH)</span>

<span id="NEUT" label="NEUT">\[b\]</span> *You <u>may not</u>
**enter**. / <u>It is not allowed</u> for you **to enter**.*  
<span>NegPrt(enter,AUTH)</span>

In these cases, the combination of a weak modal (*can, may*) with
negation leads to a stronger negative strength relation (either full or
partial).

###### Part 4-3-3-3-4. Selecting parent nodes

For each event annotated for modal strength, both a modal strength edge
value and a parent node must be selected. In the majority of cases, it
is rather straightforward which node should be selected as the parent of
an event in question.

<span id="clearparent" label="clearparent">\[66\]</span>

<span id="travel" label="travel">\[a\]</span> *Mary **travelled**
to France.*  
<span>Aff(travel,AUTH)</span>

<span id="grammodal" label="grammodal">\[b\]</span> *Mary might
**travel** this summer.*  
<span>Neut(travel,AUTH)</span>

<span id="purpclause" label="purpclause">\[c\]</span> *Mary
will **travel** to France in order to **see** the Louvre.*  
<span>Aff(travel,AUTH)</span>  
<span>Aff(MARY,AUTH)</span>  
<span>Prt(see,MARY)</span>

<span id="belief" label="belief">\[d\]</span> *Mary thinks she will
**travel** to France.*  
<span>Aff(MARY, AUTH)</span>  
<span>Aff(travel,MARY)</span>

For the events in examples like [\[66a\]](#travel) and
[\[66b\]](#grammodal), <span>AUTH</span> is the parent node of the
event. Grammaticalized modals aren’t annotated as their own nodes,
therefore events under the scope of their modality are annotated
directly underneath the relevant conceiver node, such as the author in
[\[66b\]](#grammodal). The events in purpose clauses, as in
[\[66c\]](#purpclause), are also represented as direct children
of the conceiver node (here, <span>MARY</span>). Since belief predicates
also aren’t represented as nodes in the annotation, the complements of
belief predicates will be linked directly to the relevant conceiver, as
in ([\[66d\]](#belief)).

There are also cases where there may be a choice between selecting a
conceiver or another event as the parent node. This is specifically the
case when modal predicates are represented as their own events (nodes)
in the annotation, as in ([\[67\]](#modalevent)).

<span id="modalevent" label="modalevent">\[67\]</span>

<span id="wants" label="wants">\[a\]</span> *Mary **wants** to
**travel** this summer.*  
<span>Aff(MARY,AUTH)</span>  
<span>Aff(want,MARY)</span>  
<span>Neut(travel,want)</span>

<span id="decided" label="decided">\[b\]</span> *Mary **decided**
to **travel** this summer.*  
<span>Aff(MARY,AUTH)</span>  
<span>Aff(decide,MARY)</span>  
<span>Prt(travel,decide)</span>

<span id="expects" label="expects">\[c\]</span> *Mary **expects**
to **travel** this summer.*  
<span>Aff(MARY,AUTH)</span>  
<span>Aff(expect,MARY)</span>  
<span>Prt(travel,expect)</span>

<span id="allows" label="allows">\[d\]</span> *This bar **allows
smoking**.*  
<span>Aff(BAR,AUTH)</span>  
<span>Aff(allow,BAR)</span>  
<span>Neut(smoke,allow)</span>

<span id="allows" label="allows">\[e\]</span> *We are **required**
to **order** two drinks.*  
<span>Aff(require,AUTH)</span>  
<span>Neut(order,require)</span>

In these cases, it may not be clear whether the node for the modalized
event (e.g., <span>travel</span> in [\[67a\]](#wants)) should be a
direct child of the relevant conceiver (<span>MARY</span>) or the modal
predicate event node (<span>want</span>). In all clauses with modal
predicates, the modalized event (e.g., <span>travel</span>) should be
represented as the child of the modal predicate (e.g.,
<span>want</span>) and not directly underneath the conceiver. This is
the only case (aside from reporting events) where events will be
the children of other events instead of (a direct child of) the relevant
conceiver. The event is still nested underneath the relevant conceiver,
just not as its direct child.

If multiple events are presented with the same modal strength, they
should be linked to the same parent node with the appropriate modal
strength value; they should not be linked to each other.

<span id="samespace" label="samespace">\[68\]</span>

<span id="mighttravelwork" label="mighttravelwork">\[a\]</span>
*Mary might **travel** and **work** on a paper this summer.*  
<span>Neut(travel,AUTH)</span>  
<span>Neut(work,AUTH</span>

<span id="wanttravelwork" label="wanttravelwork">\[b\]</span>
*Mary **wants** to **travel** and **work** on a paper this summer*.  
<span>Aff(MARY,AUTH)</span>  
<span>Aff(want,MARY)</span>  
<span>Neut(travel,want)</span>  
<span>Neut(work,want)</span>

In [\[68a\]](#mighttravelwork), the author has a neutral
epistemic stance towards both the *travel* and *work* events; these
events are annotated separately as children of the <span>AUTH</span>
node and not directly linked to each other. Similarly, in
[\[68b\]](#wanttravelwork), both *travel* and *work* are
Mary’s desires; they are both annotated as children of
<span>want</span> and not linked to each other.

###### Part 4-3-3-3-5. Nested modal strengths

The main way in which this annotation differs from FactBank is that it
allows for the nesting of modal strengths; that is, events can be
annotated as the children of other (possibly modalized) events in the
dependency structure. This is especially often the case when dealing
with deontic modals, as in [\[69\]](#nesting).

<span id="nesting" label="nesting">\[69\]</span>

<span id="mayneed" label="mayneed">\[a\]</span> *I <u>may</u>
**need** to **bring** a rain coat*.  
<span>Neut(need-01,AUTH)</span>  
<span>Prt(bring-01,need-01)</span>

<span id="probablywant" label="probablywant">\[b\]</span>
*I’ll <u>probably</u> **want** to **leave** early*.  
<span>Prt(want,AUTH)</span>  
<span>Neut(leave,want)</span>

In [\[69a\]](#mayneed), the partial strength deontic *need* is
embedded within the neutral epistemic modal *may*. In an annotation
scheme which does not allow nesting, it is not clear whether *bring*
should be annotated as neutral or partial strength. Here, however, we
can capture both by annotating *need* as neutral strength depending
directly on the author, and *bring* as partial strength depending on
*need*. This is the reason why the complements of modal predicates are
annotated as children of the modal predicate: by annotating
<span>leave</span> as dependent on <span>want</span>, we can capture the
nested modal strengths in an example like
[\[69b\]](#probablywant).

###### Part 4-3-3-3-6. Conditionals

Conditional constructions are some of the most complex modal expressions
and therefore require more specific annotation guidelines. As discussed
in [4.2](#havecondnode), conditionals require the addition of a
<span>have-condition</span> node. For hypothetical (i.e., prototypical)
conditionals, the <span>have-condition</span> node is linked to the
relevant conceiver with a <span>Neut</span> edge label; the protasis and
apodosis are linked to the <span>have-condition</span> node with their
appropriate modal strength. Examples are shown in
[\[70\]](#basicconds).

<span id="basicconds" label="basicconds">\[70\]</span>

<span id="posposcond" label="posposcond">\[a\]</span> *If it
**rains**, I’ll **stay** home.*  
<span>Neut(have-condition,AUTH)</span>  
<span>Aff(rain,have-condition)</span>  
<span>Aff(stay,have-condition)</span>

<span id="posneutcond" label="posneutcond">\[b\]</span> *If it
**rains**, I <u>might</u> **stay** home.*  
<span>Neut(have-condition,AUTH)</span>  
<span>Aff(rain,have-condition)</span>  
<span>Neut(stay,have-condition)</span>

<span id="neutnegcond" label="neutnegcond">\[c\]</span> *As
long as it <u>doesn’t</u> **rain**, I’ll <u>probably</u> **go** to
school.*  
<span>Neut(have-condition,AUTH)</span>  
<span>Neg(rain,have-condition)</span>  
<span>Prt(go,have-condition)</span>

<span id="multpros" label="multpros">\[d\]</span> *If it
<u>doesn’t</u> **rain** and if I **find** a ride, I’ll <u>probably</u>
**go** to school and **take** the test.*  
<span>Neut(have-condition,AUTH)</span>  
<span>Neg(rain,have-condition)</span>  
<span>Aff(find,have-condition)</span>  
<span>Prt(go,have-condition)</span>  
<span>Prt(take,have-condition)</span>

The <span>Neut</span> edge between the <span>have-condition</span> node
and the relevant conceiver reflects that the events in a conditional are
presented as only possible, not likely or certain. As mentioned in
[4.2](#havecondnode), the causal relationship between the events in the
protasis and apodosis of a conditional is not annotated, just the modal
strength of each event. The <span>Neut</span> link is annotated between
the <span>have-condition</span> node and the relevant conceiver because
it scopes over the events in the protasis and the apodosis; furthermore,
the events in the protasis and apodosis can contain modals and negation
whose value is annotated in the link between the
<span>have-condition</span> node and the event.

The modal strength edge value between an event and the
<span>have-condition</span> node reflects the event’s modal strength
value within the conditional. In [\[70a\]](#posposcond), where
there’s no negation or modals, both events have a <span>Aff</span>
relation to the <span>have-condition</span> node. In
[\[70b\]](#posneutcond), the apodosis includes the modal *might*
and therefore there is a <span>Neut</span> edge between the
<span>stay</span> event and the <span>have-condition</span> node.
Example [\[70c\]](#neutnegcond) has a negative in the protasis
and the partial strength *probably* in the apodosis. This is annotated
with a <span>Neg</span> edge between <span>rain</span> and
<span>have-condition</span> and a <span>Prt</span> edge between
<span>go</span> and <span>have-condition</span>.

As is shown in [\[70d\]](#multpros), there may be multiple events
in the protasis and/or apodosis. All events are linked to the
<span>have-condition</span> node with the appropriate modal strength
edge value.

As mentioned in [4.2](#havecondnode), the <span>have-condition</span>
node is also used for counterfactuals, as in
[\[71a\]](#counterfactual), and in concessive conditionals,
as in [\[71b\]](#concessive).

<span id="otherconds" label="otherconds">\[71\]</span>

<span id="counterfactual" label="counterfactual">\[a\]</span>
*If it had **rained**, I would have **stayed** home.*  
<span>Neg(have-condition,AUTH)</span>  
<span>Aff(rain,have-condition)</span>  
<span>Aff(go,have-condition)</span>  

<span id="concessive" label="concessive">\[b\]</span> *Even if
it is **raining**, I will **go** to school.*  
<span>Neut(have-condition,AUTH)</span>  
<span>Aff(rain,have-concession)</span>  
<span>Aff(go,have-concession)</span>

The structure of the dependency is the same for counterfactuals and
concessive conditionals as it is for hypothetical conditionals: that is,
the events in the protasis and apodosis are children of the
<span>have-condition</span> node. For counterfactuals, as in
[\[71a\]](#counterfactual), the edge value between the
conceiver and the <span>have-condition</span> node is full negative
(<span>Neg</span>). This is because counterfactuals present the events
in both the protasis and apodosis as (certaintly) not occurring.
Concessive conditionals, as in [\[71b\]](#concessive), are
annotated with a <span>Neut</span> link between the conceiver and the
<span>have-condition</span> node.

Like hypothetical conditionals, the events in the protasis and apodosis
of counterfactuals and concessive conditionals may be negated or
modalized; there also may be multiple events in the protasis or
apodosis. These are shown in [\[72\]](#othercondmods).

<span id="othercondmods" label="othercondmods">\[72\]</span>

<span id="negneutcond" label="negneutcond">\[a\]</span> *I
<u>might</u> have **gone** to school, if it <u>hadn’t</u> **rained** and
if I had **woken** up on time.*  
<span>Neg(have-condition,AUTH)</span>  
<span>Neut(go,have-condition)</span>  
<span>Neg(rain,have-condition)</span>  
<span>Aff(wake,have-condition)</span>

<span id="concessivenegneut" label="concessivenegneut">\[b\]</span>
*Even if it <u>isn’t</u> **raining**, I <u>might not</u> **go** to
school.*  
<span>Neut(have-condition,AUTH)</span>  
<span>Neg(rain,have-condition)</span>  
<span>NeutNeg(go,have-condition)</span>

###### Part 4-3-3-3-7. Reporting events

Reporting or saying events (e.g., *say, tell, shout, report*) also
require special guidelines. These types of events, as in
[\[72\]](#basicreports), express both an event in the
(author’s) ‘real-world’ and the mental content of the agent of the
reporting predicate. This means that the agents of reporting predicates
should be identified as conceivers. The conceiver node represents the
fact that what a person (or a group of people) says is on some level
based on their beliefs - either they report their beliefs accurately, or
they lie, pretend, or otherwise misrepresent their beliefs. Therefore,
the reporting predicate (like <span>say</span> in
[\[72a\]](#Marysaid) and <span>report</span> in
[\[72b\]](#NYTreported)) are annotated as a child of the
<span>AUTH</span> node; the events that are reported are annotated as
children of the reporter conceiver node (<span>MARY</span> in
[\[72a\]](#Marysaid) and <span>NEW\_YORK\_TIMES</span> in
[\[72b\]](#NYTreported).

<span id="basicreports" label="basicreports">\[72\]</span>

<span id="Marysaid" label="Marysaid">\[a\]</span> *Mary **said**
that she **went** to Santa Fe.*  
<span>Aff(MARY,AUTH)</span>  
<span>Aff(say,AUTH)</span>  
<span>Aff(go,MARY)</span>

<span id="NYTreported" label="NYTreported">\[b\]</span> *The
New York Times **reported** that Congress **voted** on the bill this
afternoon.*  
<span>Aff(NEW\_YORK\_TIMES,AUTH)</span>  
<span>Aff(report,AUTH)</span>  
<span>Aff(vote,NEW\_YORK\_TIMES)</span>

The annotation of the reporting predicate directly underneath the
<span>AUTH</span> node represents the fact that the reporting event
occurs in the real world. The reported events, however, do not
(necessarily) occur in the real world, but they reflect the mental
content of the agent of the reporting predicate.

When the author is certain that the reporting event occurs, as in
[\[72a\]](#Marysaid) and [\[72b\]](#NYTreported), this is
annotated with a <span>Aff</span> value between the author node and the
reporting event; this is also annotated in the link between the author
node and the conceiver node for the agent of the reporting predicate.
That is, the author’s certainty about the conceiver’s beliefs is based
on the author’s certainty about the occurrence of the reporting event.
With reporting events, the author’s evidence for the conceiver’s beliefs
comes from the reporting event; therefore the edge between the author
node and the reporting event node and the edge between the author node
and the reporting conceiver node will always have the same modal
strength value.

For example, in [\[72a\]](#Marysaid), the author is certain that
the reporting event occurred and therefore the author is certain about
Mary’s set of of beliefs. Note that this annotation doesn’t capture the
author’s certainty about the reported events, i.e. in
[\[72a\]](#Marysaid) the author doesn’t have a perspective on
whether or not Mary actually went to Santa Fe. This faithfully
represents the semantics of reporting constructions; the author doesn’t
express an opinion on the reality of the reported events.

When the author is uncertain about the occurrence of the reporting
event, this is also reflected in both the edge between the author and
the reporting predicate and the edge between the author and the
reporting conceiver; see [\[73a\]](#mightsay) and
[\[73b\]](#notsay).

<span id="reportsuncertain" label="reportsuncertain">\[73\]</span>

<span id="mightsay" label="mightsay">\[a\]</span>

*Mary <u>might</u> have **said** that she **went** to Santa Fe.*  
<span>Neut(MARY,AUTH)</span>  
<span>Neut(say,AUTH)</span>  
<span>Aff(go,MARY)</span>

<span id="notsay" label="notsay">\[b\]</span> *Mary <u>didn’t</u>
**say** that she **went** to Santa Fe.*  
<span>Neg(MARY,AUTH)</span>  
<span>Neg(say,AUTH)</span>  
<span>Aff(go,MARY)</span>

In [\[73a\]](#mightsay), the neutral modal strength indicated by
*might* corresponds to both the <span>Neut</span> edge between the
<span>AUTH</span> and <span>MARY</span> nodes and the <span>Neut</span>
edge between the <span>AUTH</span> and <span>say</span> nodes. As
explained above, if the author is uncertain about whether the saying
event occurs, the author must also be uncertain about Mary’s beliefs (as
expressed in the saying event). Similarly, if the author believes that
the saying event did not occur, as in [\[73b\]](#notsay), there is a
<span>Neg</span> edge between both the <span>AUTH</span> and
<span>MARY</span> nodes and between the <span>AUTH</span> and
<span>say</span> nodes.

Finally, the edge between the reporting event and the reported event(s)
reflects the modal strength of the reported events, as in
[\[74\]](#reportnest).

<span id="reportnest" label="reportnest">\[74\]</span>

<span id="sayneut" label="sayneut">\[a\]</span> *Mary **said**
that John <u>might</u> have **gone** to Santa Fe.*  
<span>Aff(MARY,AUTH)</span>  
<span>Aff(say,AUTH)</span>  
<span>Neut(go,MARY)</span>

<span id="sayprt" label="sayprt">\[b\]</span> *Mary **said** that
John <u>probably didn’t</u> **go** to Santa Fe.*  
<span>Aff(MARY,AUTH)</span>  
<span>Aff(say,AUTH)</span>  
<span>NegPrt(go,MARY)</span>

In [\[74a\]](#sayneut), Mary reports the *go* event with only
neutral certainty; this is reflected in the edge between the
<span>say</span> and <span>go</span> events. In [\[74b\]](#sayprt),
Mary reports the *go* event with negative partial certainty; this is
also reflected in the edge between the <span>say</span> and
<span>go</span> events.

#### Part 4-3-4. English constructions and lexical items

This list gives the modal strength value associated with common English
modal constructions (this is certaintly not an exhaustive list). For
modal predicates that are identified as their own event node (e.g.,
deontic predicates), the modal strength value characterizes the link
between the modal predicate node and its child event. For example,
*want* is in the <span>Neut(ral)</span> list, which indicates that there
is a <span>Neut</span> link between the <span>want</span> node and its
complement event node.  

Aff (full affirmative)

  - Simple assertions: declarative sentences

  - Certainty: *certainly, be sure, definitely, necessarily*

  - Predictive future: *will,* non-intentional *be going to*

  - Factual predicates: *manage to, finished*

Prt (partial affirmative)

  - Strong epistemic modals: *must/must have, have to, expect that,
    deduce*

  - Strong epistemic adverbs/adjectives: *probably/be probable that,
    likely/be likely that*

  - Strong deontic modals:
    
      - Intention: *intend, plan,* intentional *be going to, decide, be
        slated to*
    
      - Obligation: imperative, deontic *must, have to, should, ought
        to, be required to, need; order to, tell to, demand*
    
      - Purpose clauses/purposive event nominals: *(in order) to* VERB,
        *for* EVENT.NOM

Neut (neutral affirmative)

  - Weak epistemic modals: *may, might/might have, could have*

  - Weak epistemic adverbs/adjectives: *maybe, possibly/be possible
    that*

  - Conditionals

  - Hope/Fear: *hope, fear, worry, dread*

  - Weak deontic modals
    
      - Desire: *want, prefer, would like to*
    
      - Permission: *let, permit, allow*

NeutNeg (neutral negative)

  - Doubt: *doubt, call into question, be dubious that, be skeptical
    that*

  - Combination of (some) <span>Neut</span> lexical items with negation

PrtNeg(partial negative)

  - Strong negative deontics: *forbid, ban, disallow*

  - Negative imperatives

  - Combination of (some) <span>Prt</span> lexical items with negation

Neg (full negative)

  - Negation: *not, never, no* + noun phrase

  - Negative complement taking predicates that entail that the event
    didn’t happen: *deny, prevent, prohibit, block, cease, it is
    impossible that, avoid*

  - Counterfactuals

  - Wishes: *wish*

<!-- end list -->
  
  
 ## Part 5: Integrated examples

PRECEDING: A man has been given silver bullets, and told to shoot a Crow Chief. The man rode up behind the Crow Chief. He aimed his gun at him. He fired.

```
\ref	CrowCh(o).096
\tx	"wohei,"	hee3oohok	nuhu'	3ii'okuni3i,	"nooxohowu',
\mb	wohei		hee3oohok	nuhu'	3ii'oku -ni3i	nooxoh -owu'
\ge	okay		said.to.s.o.	this	IC.sit -4PL	dig.hole.with.tool -2PL.IMPER
\ps	part		vta.3s/4	det	vai -infl	vti -infl
			Hee3- ‘say s.t. to s.o.’ (verb, di-transitive)
			ARG 0 = [Crow Chief] [not overt in sentence]
			ARG 1 = [those sitting there]
			ARG 2 = [wohei/okay] + [dig for them, dig for them]
			Nooxoh- ‘dig for s.t. with a tool’ (verb, transitive)
			ARG 0 = [those sitting there]
			ARG 1 = [bullets] [not overt in sentence]

\tx	nooxohowu'!
\mb	nooxoh -owu'
\ge	dig.hole.with.tool -2PL.IMPER
\ps	vti -infl
\ft	"Wohei, the Crow Chief said to the ones sitting there, "dig for them, dig for them!"

(h / hee3-01
   :Arg0 (p / person :ref "3sg")
   :Arg1 (p2 / person :ref "4pl"
             :mod (n2 / nuhu')
             :Arg0-of (x / 3ii'oku))
   :Arg2 (n / nooxoh-01 :mode imperative
              :Arg0 p2
             :Arg1 (t / thing)
             :discmark (w / wohei))
    :time (b/before :op (n/now))
    :aspect Performance)

\ref	CrowCh(o).097
\tx	bii'inowuneehek,	neihoowneh'e'.
\mb	bii'in -owunee	-hek	neihoow- neh' -e'
\ge	find.s.t. -2PL	-SUBJ	1.NEG- kill -3/1
\ps	vti -infl	-infl		infl.pref- vta -infl
\ft	"If you find [the bullets], he does not kill me."
	Bii’in- ‘find s.t.’ (verb, transitive)
	ARG 0 = [you]
	ARG 1 = [bullets] [not overt in sentence]
	Neh’- ‘kill s.o.’ (verb, transitive)
	ARG 0 = [he]
	ARG 1 = [me]
(n/neh’ 
   :Arg0 (p / person :ref “3sg”)
   :Arg1 (p2/person :ref “1sg”)
   :polarity –
   :condition (b/ Bii’in
                         :Arg0 (p3 /person :ref “2pl”)
                         :Arg1 (t/thing )))
			 
\ref	CrowCh(o).098
\tx	ciibii'inowuneehek,	noh	ne'neh'einoo."
\mb	cii- bii'in -owunee	-hek	noh	ne'- neh' -einoo
\ge	NEG- find.s.t. -2PL	-SUBJ	and	then- kill -3S/1S
\ps	pref- vti -infl	-infl	part	pref- vta -infl
\ft	"If you don't find them, then he kills me."
	SAME ARG STRUCTURE AS PRECEDING
(n/neh’ 
   :Arg0 (p / person :ref “3sg”)
   :Arg1 (p2/person :ref “1sg”)
   :condition (b/ Bii’in
                         :polarity –
                         :Arg0 (p3 /person :ref “2pl”)
                         :Arg1 (t/thing ))

\ref	CrowCh(o).099
\tx	wo'oe'onoun	he'ih'iinooxoheino'.
\mb	wo'oe'onoun	he'ih'ii- nooxohei -no'
\ge	on.and.on	NARRPAST.IMPERF- dig.holes -pers.PL
\ps	part		pref- vai.o -infl
\ft	On and on they were digging (for them).
			Nooxohei- ‘dig, dig for s.t. unspecified’ (verb, intransitive)
			ARG 0 = [the ones sitting there] [not overt in sentence]
 			ARG 1 (implied only) = [the bullets] [not overt in sentence, and
 				verb is syntactically/grammatically intransitive, though
 				semantically transitive]

(n/nooxohei
   :Arg0 (p/person :ref “3pl”)
   :Arg1 (t /thing)
   :manner (w / wo'oe'onoun)
   :time (b/before :op (n/now))
   :aspect Activity)

    
\ref	CrowCh(o).100
\tx	he'ihnooko'wuuteen.
\mb	he'ih- nooko'wuutee-  ni
\ge	NARRPAST- white.streak.in/on.ground
\ps	pref- vii- OS.OBV
\ft	The ground had a white mark/streak in it.
	Nooko’wuutee- ‘there is a white mark in the ground’ or ‘the ground is marked white’ (verb, intransitive)
	ARG 0 = [the ground] (incorporated into the verb)

(w / nooko'wuutee
       :Arg0 (t /thing)
       :time (b/before :op (n/now))
       :aspect State)

\ref	CrowCh(o).101
\tx	niisootoxuuus	ne'no'uxoo';		nooxoheino'.
\mb	niisootox- uuus	ne'- no'uxoo -'		nooxohei -no'
\ge	seven- days	then- arrive -0S		dig.holes -pers.PL
\ps	pref- ni.pl	pref- vai+aff -infl	vai.o -infl
\ft	For seven days they are digging (for them).
			No’uxoo- ‘a certain time arrives, comes’ (verb, intransitive)
			ARG 0 = [(end of) seven days]
			Nooxohei- ‘dig for s.t. unspecified’ (verb, intransitive)
			SEE ARG STRUCTURE ABOVE
(a/and 
   : op1 ( n /No’uxoo
                   :Arg0 (n2 /  niisootoxuuus)
                   :time (b/before :op1 (n /now))
		   :aspect Performance)
   :op2  (n2/ nooxohei
                  :Arg0 (p/person :ref “3pl”)
                  :Arg1 (t /thing))
		  :aspect Activity)


\ref	CrowCh(o).102
\tx	hoo3ontii3i';
\mb	hoo3ontii -3i'
\ge	fail.to.do.s.t. -3PL
\ps	vai.t -infl
\ft	They failed to find them;
	Hoo3ontii- ‘fail to do s.t.’ (verb, intransitive)
	ARG 0 = [the ones sitting there] [not overt in the sentence]
	ARG 1 (implied only) = [find the bullets by digging] [not overt in the sentence, and the verb is syntactically/grammatically intransitive, though semantically transitive]
   (h/ hoo3ontii
       :Arg0 (p  /person :ref “3pl”)
       :time (b /before :op (n /now))
       :aspect Endeavor)

```
The above segment illustrates many of the issues with Arapaho: lack of overt noun phrases in a sentence; noun incorporation; and a mismatch between syntactic argument structure and semantic argument structure. Also, the actual arguments are really the pronominal affixes on the verb, Marianne Mithun would argue, and the overt nominals are just there as adjuncts for clarification where necessary.


