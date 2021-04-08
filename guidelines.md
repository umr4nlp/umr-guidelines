# Uniform Meaning Representation (UMR) 0.1 Specification
=======================================================

**November 4, 2019**

-AUTHORS-

**Table of Contents**

* Part 1. [Introduction](#part-1-introduction) (Bert) 
* Part 2. [From AMR to UMR](#part-2-from-amr-to-umr) (Bert)
* Part 3. [Sentence-Level Representation](#part-3-sentence-level-representation)
    * Part 3-1. [UMR Concepts](#part-3-1-umr-concepts)
      * Part 3-1-1. [Eventive concepts](#part-3-1-1-eventive-concepts)
      * Part 3-1-2. [Named entities](#part-3-1-2-named-entities)  (Bert, Andy)
      * Part 3-1-3. [Concept word mismatches](#part-3-1-3-concept-word-mismatches)  [reflexives,causatives, inchoatives, noun incorporation, identify what counts as light verbs] (Bill et al, Andy)]
         * Part 3-1-3-1. [Predicate and argument as one word](#part-3-1-3-1-predicate-and-argument-as-one-word)
         * Part 3-1-3-2. [Valency-changing operations](#part-3-1-3-2-Valency-changing-operations)
         * Part 3-1-3-3. [TAM categories](#Part-3-1-3-3-TAM-categories)
         * Part 3-1-3-4. [Associated Motion](#Part-3-1-3-4-Associated-Motion)
         * Part 3-1-3-5. [Non-verbal clauses](#Part-3-1-3-5-Non-verbal-clauses)
         * Part 3-1-3-6. [Multi-word concepts](#part-3-1-3-6-multi-word-concepts)
      * Part 3-1-4. [Word senses](#part-3-1-4-word-senses)
      * Part 3-1-5. [Scope for Quantification and negation](#part-3-1-5-scope-for-quantification-and-negation) (James)
      * Part 3-1-6. [Discourse relations](#part-3-1-6-discourse-relations)
    * Part 3-2. [UMR relations](#part-3-2-umr-relations) 
      * Part 3-2-1. [Participant roles](#part-3-2-1-participant-roles) (Bill and Martha)
      * Part 3-2-2. [Non-participant role UMR relations](#part-3-2-2-Non-participant-UMR-relations)
    * Part 3-3. [UMR attributes](#part-3-3-UMR-attributes) 
      * Part 3-3-1. [Aspect](#Part-3-3-1-Aspect) 
      * Part 3-3-2. [Mode](#Part-3-3-2-mode)
      * Part 3-3-3. [Polarity](#Part-3-3-3-polarity)
      * Part 3-3-4. [Quant](#Part-3-3-4-quant)
      * Part 3-3-5. [Ref](#part-3-3-5-ref)
      
      
* Part 4. [Document-Level Representation](#part-4-document-level-representation)
    * Part 4-1. [Coreference](#part-4-1-coreference) (Jayeol, Bert) 
    * Part 4-2. [Temporal Dependency](#part-4-2-temporal-dependency) (Bert, Jiarui)
    * Part 4-3. [Modality Dependency](#part-4-3-modal-dependency) (Meagan, Bill)
    
* Part 5. Integrated examples


##  Part 1: Introduction

The **Uniform Meaning Representation** (UMR) project aims to design a meaning representation that facilitates
the computational interpretation of a text. UMR combines a **sentence-level** representation that is adapted 
from **Abstract Meaning Representation** (AMR), which focuses on **predicate-argument structures**, **word senses**, **named entities**, **multi-word expressions**, **aspect**, and **quantification**, and a document-level representation
that focuses on **coreference**, **temporal** and **modal** relations. We illustrate this representation with a short English document as in [\[1 (1)\]](#1 (1)) - [\[1 (9)\]](#1 (9)), and then describe in more detail each component of UMR in the next few sections. UMR is intended to be a cross-lingual annotation framework with a shared set of **abstract** concepts and relations. 

Operationally, for both sentence-level and document-level annotation, we assume an annotation procedure in which a document is processed sentence by sentence. The sentence-level representation is annotated first, so that the document-level annotation can make reference to the concepts in the sentence-level representation.

<span id="1 (1)" label="1 (1)">\[1 (1)\]</span>
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

<span id="1 (2)" label="1 (2)">\[1 (2)\]</span>
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

<span id="1 (3)" label="1 (3)">\[1 (3)\]</span>
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
[\[1 (1)\]](#1 (1)). 

The temporal annotation indicates that the document creation time is after his denial. When annotating temporal relations, we always need to pick a *reference time* with respect to which the temporal relation between the reference time and the event can be determined. In this case, it is not clear the denying event happened before or after the conviction and sentencing events, so the reference time is determined to be the document creation time.

The modal relation indicates that the denying event definitely happened according to the author, and wrongdoing did not happen according to Alexander Pope, based on the author's account.

<span id="1 (4)" label="1 (4)">\[1 (4)\]</span>
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

In the document-level representation for this sentence, the person that is pardoned by Putin is Alexander Pope, and this is done by annotating *he* as the same person as the person whose name is Alexander Pope. In the temporal annotation, the *convict-01* event is designated as the reference time of *pardon-01* and happens before the *pardon-01* event. In the modal annotation, *pardon-01* is annotated as positive from the point of view of the author.

<span id="1 (5)" label="1 (5)">\[1 (5)\]</span>
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
In the document-level annotation of this sentence, *pardon-01* from [\[1 (4)\]](#1 (4)) is chosen as the
reference time of the *fly-01* event, and it happened before the *fly-01* event. The author is positive that the *fly-01* 
event happened.

<span id="1 (6)" label="1 (6)">\[1 (6)\]</span>
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
In the temporal annotation of this sentence, the DCT is chosen as the reference time for *spend-02*, which is in turn the reference time for *return-01*. In the modality annotation, both *spend-02* and and *return-01* actually happened according to the author. In the coreference annotation, *he* is considered to be the same as the *person* whose name is Alexander Pope in [\[1 (1)\]](#1 (1)). 

<span id="1 (7)" label="1 (7)">\[1 (7)\]</span>
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
For [\[1 (7)\]](#1 (7)), the *remission-02* event happens simultaneously with the *arrest-01* event, and the *arrest-01* event happended before DCT. According to the author, both *arrest-01* and *remission-2* happened.

<span id="1 (8)" label="1 (8)">\[1 (8)\]</span>
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

<span id="1 (9)" label="1 (9)">\[1 (9)\]</span>
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

### Part 2-1. Introduction

UMR inherits the sentence-level representation of AMR, with modifications. Like AMR, the sentence-level representation of UMR is a single-rooted, directed, node- and edge-labeled graph, as in [\[2 (1)\]](#2 (1)). The nodes of this graph are UMR concepts, while edges represent UMR relations. 

<span id="2 (1)" label="2 (1)">\[2 (1)\]</span>
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
* word senses: When definitions of word senses are available for a language in the form of a lexicon, a concept can also be a sense-disambiguated word. For instance, `taste-01` in the example above refers to the first sense of the word `taste`
* Concepts formed out of multi-word expressions: `more-than` is a concept that is formed by concatnating multiple words in a sentence. Exactly when multi-word concepts should be formed will be determined on a langugage-by-language basis.
* Named entity types. Named entities in a sentence are annotated with a named entity type concept (e.g., `person`) and a `name` concept. The actual names are annotated as a constant (`Edmund` and `Pope`).
* Abstract concepts. In some cases a concept can be inferred from the context. In this case, the concept does not corrrespond with any particular word in the sentence, hence it is an `abstract` concept.

**UMR relations:** There are also a number of ways relations between concepts are created:

* Participant roles: The partcipant roles characterize the role that a participant plays with respect to the predicate. They can be predicate-specific if a set of *frame files* are defined for a language, where a set of core participant roles are defined for each (a sense of the ) predicate. For example, `:ARG0` and `:ARG1` are participant roles defined for `taste-01`. For languages that do not have *frame files*, the participant role are generic (e.g., `Actor`, `Experiencer`), and they are described in [Part 3](#part-3-2-umr-relations)
* Semantic relations: Other UMR relations include `:time`, `:org`, `:range` etc. that are not normally characterized as participant roles. A complete list of such relations can be found in [Part 3](#part-3-2-umr-relations)

**UMR attributes:** UMR currently has three attribute types:

* Aspect: Aspect are annotated for eventive concepts only. Non-eventive concepts are not annotated with Aspect and are assigned the default value `Process`. Possible Aspect values include `Activity`, `Habitual`, `State`, `Endeavor`, `Performance`. A complete list of aspect values with explanations and examples can be found in [Part 3-3-1 Aspect](#part-3-3-1-aspect). 
* Polarity: Polarity is only annotated for negative polarity as indicated by a negation marker or an affix indicating negation.
* Mode: The mode attribute is typically for the main predicate of a sentence. Its values include `imperative` and `interrogative`
* Quantity: The value of a `:quant` attribute is a numerical number
* Value: The value of a `:value` attribute is a numerical number. 
* Reference: The value of a `:ref` attribute is a *bundle* of person and number feature used to represent reference. The bundle of features is used to represent pronouns (e.g., `1s`, `2pl`).

**Differences between AMR and UMR**

UMR differs from AMR in a number of ways:

* UMR is a document-level representation that represents *coreference*, *temporal dependencies*, and *modal dependencies*.

* As a result, some sentence-level AMR concepts  are now represented at the document level. This applies to concepts for modality (e.g., `possible-01`, `obligate-01`) - see the AMR and the UMR for `The boy can go` in [\[2 (2a)\]](#2 (2a)) and [\[2 (2b)\]](#2 (2b)), respectively.

<span id="2 (2a)" label="2 (2a)">\[2 (2a)\]</span>

```
(p / possible-01
   :ARG0 ( g / go-01  
            :ARG0 boy ))
```
<span id="2 (2b)" label="2 (2b)">\[2 (2b)\]</span>
```
( g / go-01  
    :ARG0 boy )

(s0/sentence
  :modal (s0g :PARTAFF AUTH))
  
```

* UMR adds a *scope* concept to represent the relative scope of quantifiers and negations. See [Part-3-1-5](#part-3-1-5-scope-for-quantification-and-negation) for details.
* UMR allows the use of non-predicate-specific participant roles for languages that do not *frame files*
* UMR adds  *aspect*  and *ref* attribute to the representation. See [Part 3-3-1](#part-3-3-1-aspect) for details.

### Part 2-2: Introduction for field linguists.

The annotation scheme detailed in these guidelines, Uniform Meaning
Representation (UMR), intends to allow for annotation of temporal,
aspectual, modal, and quantification semantics, as well as semantic
argument structure, in a cross-linguistically motivated and portable
way. Some semantic domains, specifically co-reference, temporal
relations, and modal relations, are annotated in a document-level
structure. Other domains, such as predicate-argument structure, aspect,
and quantification, are annotated in a sentence-level structure.

This UMR sentence-level structure builds on a sentence-level representation
that is adapted from the Abstract Meaning Representation (AMR)
annotation scheme, which was originally designed for the annotation of
English, and has since been extended to Chinese and Arabic, amongst
others. This means that, before getting to the cross-linguistically
motivated parts of UMR annotation, annotators for new languages need to
do some AMR-based annotation of their texts, specifically regarding
predicate-argument structure. This section of the guidelines discusses
which parts of AMR annotation are required before the UMR annotation
procedure detailed in the rest of these guidelines can be applied.

The core of AMR is that it represents natural language sentences as
single-rooted, directed, node-labelled and edge-labelled graphs.
Semantic concepts expressed in such natural language sentences are
represented in two ways. Some of them are represented as *concepts*,
which means that they function as nodes in the AMR graphs. This is the
case for predicates and (heads of) referring expressions, for instance.
Other meanings are represented as *relations* in AMR, which means that
they function as edges in the AMR graphs. This is the case for argument
roles and modifiers of nouns, amongst others.

The annotation of predicate-argument structure is the main domain in
which AMR annotation conventions are inherited. First and foremost,
predicated events are represented in the graph as nodes, as are
predicated states, events that are being referred to or used as
modifiers, and various other kinds of "non-verbal predicates" (see
section 3.1.5 on event identification). For annotation of English texts,
sense-disambiguated predicates from PropBank are used to label predicate
nodes. Since for most languages, no equivalent of PropBank is available,
we recommend labelling nodes with a citation form of the verb
supplemented with a -00 suffix. In this way, annotations can be used for
the development of digital lexicons in the future.

The semantic arguments of such predicate nodes are represented in the
graph as daughter nodes of the relevant predicate (see section 3.1.6 on
participant identification). The edge that connects parent and daughter
nodes in these structures carries a participant role label. For English,
these participant role labels are predicate-specific, numbered argument
roles drawn once again from PropBank. For languages without comparable
lexical databases, we use an inventory of general argument roles such as
Actor, Undergoer, and Theme. In the long run, annotations can be used to
create language-specific and predicate-specific frame files detailing
argument structure of individual predicates, and the predicate-specific
argument roles can be linked to predicate-general participant roles for
commensurability (see section 3.2.1 on argument structure annotation).
This AMR-based predicate-argument annotation is shown in its most basic
form in [\[2-2-1 (1)\]](#2-2-1 (1)) below.

<span id="2-2-1 (1)" label="2-2-1 (1)">\[2-2-1 (1)\]</span>
```
ap-hle-am-ke'				nenhlet
2M-travel-PST/HAB-V1.NFUT	person
'A man travelled.'

(e / enhleama-00 'travel'
	:Actor (n / nenhlet 'person))
(t / travel-01
	:ARG0 (m/ man))
```

The basic, AMR-inspired graph structures for simple sentences in
languages like English and Sanapaná then look very similar, as shown
above: they both have a predicate corresponding to the main event of the
sentence as the top of the graph - the English one has a reference to a
numbered PropBank frame file for the predicate *travel*, the Sanapaná
one just has the citation form of the *travel*-verb with a -00 suffix.
In both cases, the semantic argument 'person/man' is a daughter of this
predicate, linked with a participant role edge. In English, this is a
numbered participant role taken from this same PropBank frame file,
while in Sanapaná it is a predicate-general participant role.

AMR and UMR concepts are underspecified for morphosyntactic
representation: the same concept (for example, *travel-01*) can be used
to annotate a verb (as seen above), a noun (e.g. *his travels* in [\[2-2-1 (2)\]](#2-2-1 (2))), or any other relevant part of speech conveying the same semantic meaning. Section 3.1.1 discusses how AMR and UMR deal with the
information-packaging differences which are conveyed by packaging such
content in different parts of speech.

<span id="2-2-1 (2)" label="2-2-1 (2)">\[2-2-1 (2)\]</span>
```
I heard about his travels.

(h / hear-01
	:ARG0 (p / person
		:ref-person 1st
		:ref-number Singular)
	:ARG1 (t / travel-01
		:ARG0 (p2 / person
			:ref-person 3rd
				:ref-number Singular))
```

UMR inherits annotation conventions from AMR in domains other than
predicate-argument structure. With regard to concepts, UMR treats
multi-word expressions in essentially the same way as AMR. Specifically,
it allows annotators to select multiple words in a sentence and annotate
them as a single concept. This is necessary, for example, to annotate
idiomatic expressions which cannot be semantically decomposed
felicitously. In [\[2-2-1 (3)\]](#2-2-1 (3)), for instance,
*elvongkeskama tayep* is a multi-word expression which literally and
compositionally means "cause (someone) to be just across", but its
idiomatic meaning is "rescue". The two words are therefore annotated
together as a multi-word expression with a single meaning. Some further
specifications are made in UMR with regards to the annotation of
multi-word expressions such as serial verb constructions and
periphrastic TAM constructions. More information about the annotation of
multi-word expressions is given throughout section 3.1.3, and
specifically in section 3-1-3-6.

<span id="2-2-1 (3)" label="2-2-1 (3)">\[2-2-1 (3)\]</span>
```
apk-el-vongk-es-akp-e'				tayep	ayko<'o>k
2/3M-DISTR-be.just-CAUS-PAS-V1.NFUT	across	child<PL>
'The children were rescued.'

(e / elvongkeskama-tayep-00 'rescue'
	:Undergoer (a/ aykok 'child'
		:ref-number Plural))
```

AMR conventions are also largely inherited with regards to the use of
abstract concepts. Abstract concepts are concepts that are identified
and annotated even though they do not (consistently) correspond to any
overt word in the sentence. There are typically two main reasons for
which AMR and UMR use abstract concepts. Firstly, there are concepts
where AMR and UMR use abstract concepts rather than language-specific
concepts corresponding to specific words with the goal of making
annotations cross-linguistically comparable. For example, even though
the Sanapaná thetic possession construction in [\[2-2-1 (4)\]](#2-2-1 (4)) makes use of a verb
that literally means *exist*, an abstract concept predicate node
"have-03" is introduced rather than a language specific "enyetnema-00"
concept. This way, possessive constructions across the world's languages
can be annotated in consistent and comparable ways regardless of the
morphosyntactic strategies they use (see section 3-1-3-5 for more
information on such "non-verbal clauses").

<span id="2-2-1 (4)" label="2-2-1 (4)">\[2-2-1 (4)\]</span>
```
an-yetn-eye'			ko'o	vakka-hak	ah-ahangkok
2/3F-exist-V1.NFUT		1SG:PRO	cow-old		1SG-POS
'I have a book.' lit. 'My book exists.'

(h/ have-03
	:ARG0 (p / person
		:ref-person 1st
		:ref-number Singular)
	:ARG1 (v/ vakkahak 'book'))
```

Secondly, abstract concept conventions are inherited from AMR in a
variety of domains where information expressed in natural language text
needs to be standardized for computational tractability. This applies
to, for example, the annotation of different types of quantities (which
use abstract concepts such as *distance-quantity*,
*temporal-quantity* and *monetary-quantity*, as
illustrated in [\[2-2-1 (5a)\]](#2-2-1 (5a)) )-[\[2-2-1 (5b)\]](#2-2-1 (5b)), and the annotation of dates and times (which use abstract concepts such as *date-entity*, as illustrated in [\[2-2-1 (5c)\]](#2-2-1 (5c)). More information on abstract concepts can be found throughout this document in the sections dedicated to the specific semantic
phenomena for which they are needed.

<span id="2-2-1 (5)" label="2-2-1 (5)">\[2-2-1 (5)\]</span>

<span id="2-2-1 (5a)" label="2-2-1 (5a)">\[2-2-1 (5a)\]</span>
```
cinco,	seis	meses	apk-ehl-ta'mehl-kes-kam-a
five	six		months	2/3M-DSTR-be.good-CAUS-PST/HAB-NOM
'They used to preserve it for five or six months.'

(e/ enta'mehlkeskama-00 'preserve'
	:Actor (p/ person
		:ref-person 3rd
		:ref-number Plural)
	:Undergoer (t/ thing)
	:Duration (o/ or
		:op1 (t2/ temporal-quantity
			:quant 5
			:unit (m/ mes 'month'))
		:op2 (t3/ temporal-quantity
			:quant 6
			:unit (m/ mes 'month'))))
```
<span id="2-2-1 (5b)" label="2-2-1 (5b)">\[2-2-1 (5b)\]</span>
```
escuela	agrícola		seis	millón	cada	año		on-yanmong-kes-ek
school	agricultural	six		million	each	year	1PL.IRR-exchange-CAUS-FUT
'For the agricultural school, we would pay six million (guaranies) per year.'

(e/ enyanmongkeskama-00 'pay'
	:Actor (p/ person
		:ref-person 1st
		:ref-number Plural)
	:Recipient (e2/ escuela 'school'
		:mod (a/ agrícola 'agricultural'))
	:Theme (m/ monetary-quantity
		:quant 6,000,000
		:unit (g/ guaraní
			:mod (c/ country
				:wiki "Paraguay"
				:name (n/ name :op1 "Paraguay"))))
	:Frequency (r/ rate-entity
		:ARG1 1
		:ARG2 (t/ temporal-quantity
			:quant 1
			:unit (a2/ año 'year))))
```
<span id="2-2-1 (5c)" label="2-2-1 (5c)">\[2-2-1 (5c)\]</span>
```
apk-el-v-ayk-akh-a'					Venancio	el-eyv-om-akha'				mil			novecientos		sesenta	y	seis=anehla
2/3M-DSTR-arrive-PST/HAB-REP-NOM	Venancio	1PL-live-PST/HAB-NOM.LOC	thousand	nine-hundred	sixty	and	six=DUB
'Venancio and his companions arrived where we lived in ninteen sixty-six, maybe.'

(e/ elvay'a-00 'arrive'
	:Actor (p/ person
		:name (n/ name "Venancio")
		:Companion (p2/ person))
	:Goal (p3/ place
		:Place-of (e2/ eleyvoma-00 'live'
			:Actor (p4/ person
				:ref-person 1st
				:ref-number Plural)))
	:Temporal (d/ date-entity
		:year 1966))
```
Another domain in which AMR conventions are inherited by UMR is the
annotation of non-participant role relations. Such relations are used to
annotate a wide range of meanings. Many of them, such as :medium,
:topic, and :mod (the latter of which is illustrated in [\[2-2-1 (5b)\]](#2-2-1 (5b)) are used to
annotate modifiers of referring expressions. Other relations are used
with specific abstract concepts: whenever a *date-entity*
concept is present, one of the temporal relations :month, :year, :date
etc. will be used, for example. The use of these relations is treated
more in detail in section 3-2-2 of this document.

Even though many of these relations are straightforwardly inherited by
UMR, some changes are made to their use for the sake of cross-linguistic
comparability. Firstly, UMR adjusts the use of the :mod relation to
cover all *typifying* modifiers - i.e. modifiers which subcategorize the
reference of a referring expression rather than narrowing it down to a
specific entity (e.g. *women* in *women's magazine*). In AMR, this
semantic domain was shared between the :mod relation and a number of
other relations such as :medium, :topic, and :consist-of. In UMR, these
other relations still exist, but they are treated as more fine-grained
values on a lattice underneath the more general :mod relation. Whereas
AMR used the :frequency and :duration relations as the main ways of
annotating Aspect, UMR does this through a dedicated :Aspect attribute.
However, UMR maintains the :duration and :frequency relations so that
annotators can use them to indicate more fine-grained aspectual
information beyond the aspect categories offered in the corresponding
attribute, as in [\[2-2-1 (5b)\]](#2-2-1 (5b)). UMR also adds a new non-participant role relation: the :other relation, which annotators can use when encountering meanings that UMR currently does not provide a straightforward annotation procedure for.

The last area in which AMR conventions are inherited by UMR is that of
*attribute* annotations. Attributes are relations which attach one of a
closed, pre-defined list of values to a concept node: for example, the
:Aspect attribute allows annotators to hang a *state, habitual,
activity, endeavor*, or *performance* value off
of a predicate node. Attributes inherited from AMR are :polarity, :mode,
:quant, and :value (discussed in more depth in section 3-2-2). The use
of the :quant relation was changed in that a more fine-grained
annotation scheme for quantification is now available (see sections
3-1-5 and 3-3-4). The :quant relation is mainly what annotators with
less training or for languages with less available linguistic analysis
will use to flag concepts that are of interest with regards to
quantification (i.e. in stage 0 annotation). More confident annotators
and annotators for well-documented languages will apply the full
fine-grained quantification and scope scheme (stage 1 annotation). One
specific change is that, whereas in mensural constructions (e.g. *three
cups of milk*, AMR varies between having the substance or the mensural
term as the head depending on morphosyntactic expression, UMR always
annotates the substance as the head for greater cross-linguistic
comparability. This means that even less conventionalized measure terms,
like English *cup* or *bag*, are annotated as modifiers, even though
they look like morphosyntactic heads. This is illustrated in [\[2-2-1 (6)\]](#2-2-1 (6)). The use of the :polarity value is constrained to the sentence level.
Propositional negation is annotated in the modal section of the document
level annotation. The :polarity value is used to indicate any overt
morphosyntactic exponents of negation at the sentence level, flagging
such concepts as interesting for the modal or scope negation. This
includes e.g. morphologically negated adjectives, even though in the
document-level modal annotation, these will not be annotated as negated.

<span id="2-2-1 (6)" label="2-2-1 (6)">\[2-2-1 (6)\]</span>
```
Three bottles of water

(w/ water
	:quant 3
	:unit (b/ bottle)
```

UMR introduces three new attributes: :Aspect (see section 3-3-1), and
:ref-person and :ref-number (see section 3-3-5).


## Part 3. Sentence-Level Representation

### Part 3-1. UMR Concepts

#### Part 3-1-1. Eventive concepts

Identification of eventive concepts is important to participant role annotation as well as aspect and modality annotation.
The criteria used to identify events in UMR are largely based on the
criteria used in TimeML (Pustejovsky et al. 2005). Event identification is not based on parts of speech or word classes, since these vary greatly across languages. Instead, event identification is based on a combination of semantic type and information packaging (Croft 2001). Semantic type refers to the difference between entities (or, objects), states (or, properties), and processes; this can be thought of as a categorization of things in the real world.
Information packaging (also called discourse function or information
structure), on the other hand, characterizes how a particular linguistic
expression “packages” the semantic content. There are three fundamental
information packaging functions: reference, modification, and
predication. Croft (in preparation)  defines them as:

**reference**: what the speaker is talking about  
**modification**: additional information provided about the referent  
**predication**: what the speaker is asserting about the referents in a particular utterance

The three semantic types can occur with any of the three fundamental
information packaging functions, as shown in Table
1 from Croft (in preparation).



|           |              Reference               |           Modification           |         Predication         |
| :-------: | :----------------------------------: | :------------------------------: | :-------------------------: |
| Entities  |         the sharp **thorns**         |      the **bush’s** thorns       |     It **is a thorn.**      |
|  States   |            **sharpness**             |       the **sharp** thorns       | Those thorns **are sharp.** |
|     Processes      |     I said \[**that** the thorns **scratched** me\]. / <br />      the \[**scratching** of the thorns\]    |       the thorns **that** \[**scratched** me\] / <br /> the thorns \[**scratching** me\]        |      The sharp thorns **scratched** me.      |

Cross-linguistically, certain types of morphosyntactic constructions
tend to express specific combinations of semantic type and information
packaging; these are shown in Table 2,
modified from Croft (2001). Prototypical combinations of semantic type and
information packaging are indicated with caps. These correspond to
well-known part-of-speech classes across languages: entities in
reference correspond to nouns, states in modification to adjectives, and
processes in predication to verbs.

|               |                   Reference                   |                    Modification                    |                  **Predication**                  |
| :-----------: | :-------------------------------------------: | :------------------------------------------------: | :-----------------------------------------------: |
|   Entities    | UNMARKED NOUNS |                 relative clauses, PPs on nouns                  |              **predicate nominals,** **complements**             |
|    States     |              deadjectival nouns               | UNMARKED ADJECTIVES |             **predicate adjectives,** **complements**           |
| **Processes** |       **event nominals, complements,** **infinitives, gerunds**        |         **participles, relative clauses**          | **UNMARKED VERBS** |

The most prototypical expression for an event is a process in
predication, therefore we identify a word/phrase as an event if it has
either the semantic type of the prototype (process) or the prototypical
information packaging (predication). The categories which are identified
as events in UMR are shown in bold in Table 2.

##### 3-1-1-1. Processes in predication

Predicated processes are the most prototypical subcategory of events,
corresponding cross-linguistically to unmarked verbs. They will
therefore always be identified as events. This is shown in
[\[3-1-1-1 (1)\]](#3-1-1-1 (1)) below. (Throughout this section, words
that are identified as events will be shown in bold; the relevant
phenomenon under discussion will be underlined.)

<span id="3-1-1-1 (1)" label="3-1-1-1 (1)">\[3-1-1-1 (1)\]</span>

<span id="3-1-1-1 (1a)" label="3-1-1-1 (1a)">\[3-1-1-1 (1a)\]</span> She
<u>**repaired**</u> her bike.  
<span id="3-1-1-1 (1b)" label="3-1-1-1 (1b)">\[3-1-1-1 (1b)\]</span> Before
she <u>**went**</u> to school, she **repaired** my bike.  

Regardless of whether they are in an independent clause, like *repaired*
in [\[3-1-1-1 (1a)\]](#3-1-1-1 (1a)), or a dependent clause, like *went* in
[\[3-1-1-1 (1b)\]](#3-1-1-1 (1b)), predicated processes are always
identified as events.

##### 3-1-1-2. Processes in modification and reference

Processes packaged as modifiers or referents should also be identified
as events. Cross-linguistically, these may take a variety of
morphosyntactic forms, such as event nominals (as in
[\[3-1-1-2 (1a)\]](#3-1-1-2 (1a))), non-finite complements (as in
[\[3-1-1-2 (1b)\]](#3-1-1-2 (1b))), participles (as in
[\[3-1-1-2 (1c)\]](#3-1-1-2 (1c))), or relative clauses (as in
[\[3-1-1-2 (1d)\]](#3-1-1-2 (1d))).

<span id="3-1-1-2 (1)" label="3-1-1-2 (1)">\[3-1-1-2 (1)\]</span>

<span id="3-1-1-2 (1a)" label="3-1-1-2 (1a)">\[3-1-1-2 (1a)\]</span> The
**<u>storm</u> damaged** the roads.

<span id="3-1-1-2 (1b)" label="3-1-1-2 (1b)">\[3-1-1-2 (1b)\]</span> She
**wanted <u>to go</u>** to school.

<span id="3-1-1-2 (1c)" label="3-1-1-2 (1c)">\[3-1-1-2 (1c)\]</span> The
student **<u>playing</u>** the violin **likes** Bach.

<span id="3-1-1-2 (1d)" label="3-1-1-2 (1d)">\[3-1-1-2 (1d)\]</span> The student,
who is **<u>playing</u>** the violin, **likes** Bach.

The combination of semantic type and information packaging determines
whether or not a particular word in a particular context is identified
as an event. The morphological structure of a word (i.e., whether or not
it derives from a verb) doesn’t factor into whether or not it is
identified as an event. For example, not all event nominals are derived
from verbs, as in [\[3-1-1-2 (2a)\]](#3-1-1-2 (2a)); and, not all words
derived from verbs actually refer to processes, as in
[\[3-1-1-2 (2b)\]](#3-1-1-2 (2b)).

<span id="3-1-1-2 (2)" label="3-1-1-2 (2)">\[3-1-1-2 (2)\]</span>

<span id="3-1-1-2 (2a)" label="3-1-1-2 (2a)">\[3-1-1-2 (2a)\]</span> He is
**planning** a **<u>ceremony</u>** for Saturday.

<span id="3-1-1-2 (2b)" label="3-1-1-2 (2b)">\[3-1-1-2 (2b)\]</span>
The bus <u>driver</u> **turned** the corner too sharply.

Even the same lexical item may or may not refer to a process, depending
on context as in ([\[3-1-1-2 (3)\]](#3-1-1-2 (3))) below.

<span id="3-1-1-2 (3)" label="3-1-1-2 (3)">\[3-1-1-2 (3)\]</span>

<span id="3-1-1-2 (3a)" label="3-1-1-2 (3a)">\[3-1-1-2 (3a)\]</span>

The <u>**final exam**</u> began at 8:00.

<span id="3-1-1-2 (3b)" label="3-1-1-2 (3b)">\[3-1-1-2 (3b)\]</span>

One student **threw** their <u>final exam</u> in the trash.

In ([\[3-1-1-2 (3a)\]](#3-1-1-2 (3a))), *final exam* refers to a process and therefore
is identified as an event. In ([\[3-1-1-2 (3b)\]](#3-1-1-2 (3b))), however,
*final exam* refers to a physical object and therefore is not identified
as an event.

Participles (or other non-finite verb forms) are identified as events,
unless they are part of a compound. For example, *floating* in *floating
hospitals* is identified as an event, but *firing* in *firing squad* is
not, since it is part of a compound. One way to check for this
distinction is to see if the event described by the participle must be
ongoing at the reference time. For example, one can say *I saw the
firing squad* without having seen an actual firing event, whereas *I saw
the floating hospitals* implies that the seer witnessed the floating
event as well.

##### 3-1-1-3. States and entities

As mentioned above, anything that is predicated is identified as an
event, even if it is not a process. Two-place statives, such as *love*
in [\[3-1-1-3 (1)\]](#3-1-1-3 (1)), are annotated in the same way as predicated
processes, i.e. an event is identified and labelled with the predicate
in the language.

<span id="3-1-1-3 (1)" label="3-1-1-3 (1)">\[3-1-1-3 (1)\]</span>

My cat <u>**loves**</u> wet food.

Other types of predicated states and entities require a different
solutions based on their function and the strategy used to express them
in a language; we call these “nonverbal clauses”. The different
functional types of nonverbal clauses are shown below in Table 3.

<div id="tab:nonverbaltypes">

| **Semantics** | **Information-packaging** | **Example**                     |
| :------------ | :------------------------ | :------------------------------ |
| possession    | thetic/presentational     | The teacher has a dog.          |
| possession    | predicational             | The dog belongs to the teacher. |
| location      | thetic/presentational     | On the rock was a symbol.       |
| location      | predicational             | The symbol was on the rock.     |
| property      | predicational             | The cat is black.               |
| object        | predicational             | Panda is a cat.                 |
| object        | equational                | Panda is my cat.                |

</div>

There are four semantic types of nonverbal clauses: possession,
location, property, and object. All of these occur with predicational
information-packaging: the possessive relationship, location, property,
or object category are predicated of the possession or theme. Possession
and location are, in addition, used in a context in which the entire
information is presented as ‘thetic’ or ‘all-new’ in the terms of
Lambrecht’s theory of information structure (Lambrecht 1994; cf. the contrast between
‘have’ possession \[thetic\] and ‘belong’ possession \[predicational\]
in Heine 1997). One common thetic function is presentational, as in the examples
in Table 3 above. For objects, it can be
difficult to distinguish equational (corresponding to Lambrecht’s
identificational information structure) and predicational
information-packaging in context (see Stassen 1997:106-111). Object predication asserts that
the theme is part of a category of objects (i.e., *Panda* fits within
the category of *cat*), whereas equational sentences indicate that two
referents are the same (i.e., *Panda* is the same referent as *my cat*).

For these nonverbal clause categories, the event identified is labelled
with a special [Abstract?] UMR predicate that indicates the relevant combination of
semantics and information-packaging. These are shown below in Table 4. For the labelling of participants with these
nonverbal clause predicates, see §[4](#participantroles).FIX HYPERLINK

<div id="tab:nonverbalpreds">

| **Clause type**                  | **UMR Predicate** |
| :------------------------------- | :---------------- |
| thetic/presentational possession | have-03           |
| predicative possession           | belong-01         |
| thetic/presentational location   | exist-91          |
| predicative location             | have-location-91  |
| property predication             | have-mod-91       |
| object predication               | have-role-91      |
| equational                       | identity-91       |


</div>

States in modification, as in [\[3-1-1-3 (2a)\]](#3-1-1-3 (2a)) and
[\[3-1-1-3 (2b)\]](#3-1-1-3 (2b)), and states in reference, as in
[\[3-1-1-3 (2c)\]](#3-1-1-3 (2c)), are not identified as events.

<span id="3-1-1-3 (2)" label="3-1-1-3 (2)">\[3-1-1-3 (2)\]</span>

<span id="3-1-1-3 (2a)" label="3-1-1-3 (2a)">\[3-1-1-3 (2a)\]</span> The
<u>tall</u> man...

<span id="3-1-1-3 (2b)" label="3-1-1-3 (2b)">\[3-1-1-3 (2b)\]</span> The man,
<u>who is tall</u>...

<span id="3-1-1-3 (2c)" label="3-1-1-3 (2c)">\[3-1-1-3 (2c)\]</span> His
<u>happiness</u>...

Similarly, entities in modification, as in [\[3-1-1-3 (3a)\]](#3-1-1-3 (3a)),
and entities in reference, as in [\[3-1-1-3 (3b)\]](#3-1-1-3 (3b)), are not
identified as events.

<span id="3-1-1-3 (3)" label="3-1-1-3 (3)">\[3-1-1-3 (3)\]</span>

<span id="3-1-1-3 (3a)" label="3-1-1-3 (3a)">\[3-1-1-3 (3a)\]</span> The man,
<u>who is a doctor</u>...

<span id="3-1-1-3 (3b)" label="3-1-1-3 (3b)">\[3-1-1-3 (3b)\]</span> The
<u>doctor</u>

Causal relationships follow the same rules as states and entities. They
are identified as events when they are predicated, as in
[\[3-1-1-3 (4a)\]](#3-1-1-3 (4a)), but they are not identified as events
otherwise, like in [\[3-1-1-3 (4b)\]](#3-1-1-3 (4b)).

<span id="3-1-1-3 (4)" label="3-1-1-3 (4)">\[3-1-1-3 (4)\]</span>

<span id="3-1-1-3 (4a)" label="3-1-1-3 (4a)">\[3-1-1-3 (4a)\]</span> The
**explosion <u>caused</u>** the house **to collapse**.

<span id="3-1-1-3 (4b)" label="3-1-1-3 (4b)">\[3-1-1-3 (4b)\]</span> The house
**collapsed** <u>because</u> of the **explosion**.

##### 3-1-1-4. Implicit events

Since UMR annotates meaning, and not form, there are situations where
events are identified in the absence of explicit linguistic material.
These correspond to events which are implicit, given the context, but
not overtly expressed. We encourage annotators to be conservative on
this front; when in doubt, don’t add an implicit event.

We’ve identified two types implicit events: those where the implicit
event corresponds to an event mentioned earlier in the text (as in
[\[3-1-1-4 (1)\]](#3-1-1-4 (1))), and those where it does not (as in
[\[3-1-1-4 (2)\]](#3-1-1-4 (2))).

<span id="3-1-1-4 (1)" label="3-1-1-4 (1)">\[3-1-1-4 (1)\]</span>

<span id="3-1-1-4 (1a)" label="3-1-1-4 (1a)">\[3-1-1-4 (1a)\]</span> John was **smoking** on
the corner of the street, but when he **saw** me, he stopped <u>
**\[smoking\]**</u>.

<span id="3-1-1-4 (1b)" label="3-1-1-4 (1b)">\[3-1-1-4 (1b)\]</span> They **told** me “a card
was **left** on Tuesday” (no it wasn’t <u>**\[left\]**</u> *of
course)...*

In [\[3-1-1-4 (1a)\]](#3-1-1-4 (1a)), there is an implicit second *smoking* event and
in [\[3-1-1-4 (1b)\]](#3-1-1-4 (1b)), there is an implicit second *leave* event. These
implicit events should be annotated as co-referential with the event
mentioned earlier in the text (see §[3](#coref)).

In [\[3-1-1-4 (2)\]](#3-1-1-4 (2)), however, the implicit events don’t
have a relationship with an event previously mentioned in the text;
instead, they refer to generic events which can be filled in from
context.

<span id="3-1-1-4 (2)" label="3-1-1-4 (2)">\[3-1-1-4 (2)\]</span>

<span id="3-1-1-4 (2a)" label="3-1-1-4 (2a)">\[3-1-1-4 (2a)\]</span> **Phoned** Amtrak on
Wednesday, <u>**\[they said\]**</u> *“We **need** a consignment
number”.*

<span id="3-1-1-4 (2b)" label="3-1-1-4 (2b)">\[3-1-1-4 (2b)\]</span> “I have **ordered** the Coast
Guard and our entire naval force in the (Central Philippines) region
<u>**\[to go\]**</u> to the area,” she **said**.

In [\[3-1-1-4 (2a)\]](#3-1-1-4 (2a)), the quotation marks make it clear that there is an
implicit *say* event. In [\[3-1-1-4 (2b)\]](#3-1-1-4 (2b)), we can identify a very general
*go* event, since *ordered...to the area* implies a motion event. For
these types of implicit events, the most abstract, least specific event
should be identified. For example in [\[3-1-1-4 (2b)\]](#3-1-1-4 (2b)), we could make an
assumption based on context clues (e.g., *Coast Guard, naval force*),
that the type of motion event is *sail*. But, that assumption may not be
accurate (and may not be shared amongst annotators); therefore, the most
general event possible should be identified.



 #### Part 3-1-2. Named entities
 
Following AMR, each named entity in a text is annotated with a type. However, the vocabuary of the named entity types are adpated from AMR so that they reflect the characterization of additional languages and thus made uniform across languages. Example [\[3-1-2 (1)\]](#[3-1-2 (1)) has a *country* entity and a *person* entity. 

<span id="3-1-2 (1)" label="3-1-2 (1)">\[3-1-2 (1)\]</span> Edmond Pope is an American businessman.
```                    
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

 #### Part 3-1-3. Concept-word mismatches
 
Cross-linguistically, concepts are not always mapped onto words in the
same way. Many low-resource languages are morphologically more complex
than languages like English, and they often express in a single word
concepts for which English needs multiple words. For a number of
reasons, UMR does not require the decomposition of morphologically
complex words into morphemes that individually map to concepts, but
instead, such words can as a whole map to multiple concepts. How exactly
this mapping between single, (often) morphologically complex words and
multiple concepts is achieved depends on which semantic categories are
involved and how they behave across languages. This section provides
guidance on the annotation of predicates and arguments in five different
types of constructions where the mapping between words and concepts is
not straightforward.

 ##### Part 3-1-3-1. Predicate and argument as one word

In languages that make use of verbal argument indexation (i.e.
pronominal affixes on the verb to cross-reference semantic arguments) or
noun incorporation, predicates and their arguments can be expressed
together in a single word. Both issues are illustrated in 
[3-1-3-1 (1)](#3-1-3-1 (1)) from Arapaho. Here, what is
expressed as a multi-word sentence in the English translation takes the
form of a single Arapaho word. The pronominal suffix *-o'* indicates
that a first person argument acts on a third person argument. The
lexical item for 'head', *e'ei*, is incorporated in the verb, and the
classifier *-s* indicates that the instrument is a blade-like implement.
So, this single word expresses the predicate, and the Actor, Undergoer,
Theme, and Instrument arguments of this state of affairs.

<span id="3-1-3-1 (1)" label="3-1-3-1 (1)">\[3-1-3-1 (1)\]</span>
```
nih-teb-e'ei-s-o'
PST-break/remove.stick.like-head-by.blade.CAUS-1SG/3SG
'I cut his head off with a knife.'

(n / teb-e'ei-s ‘break/remove.stick.like’
    :Actor (p / person :ref 1SG)
    :Undergoer (p2 / person :ref 3SG)
    :Theme (t / thing :ref obviative)
    :Aspect Performance
    :Modstrength Aff)
```

When languages use verbal affixes to index arguments, these arguments
then may or may not be expressed through independent NPs elsewhere in
the clause. UMR treats such indexed arguments in the same way as it does
free pronouns - they are identified as arguments of the verb. So, even
though there is no overt word in the sentence above referring to a first
person actor or a third person undergoer, these arguments are
nevertheless identified and annotated (using a named-entity concept, in
this case 'person' or 'thing', as they are clearly identifiable to
native speakers of the language).

Noun incorporation constructions come in different types across
languages (Mithun 1984). Some constructions, such as the one illustrated by *-e'ei*
'head' above, are not very grammaticalized. Here, the incorporated noun
functions as an argument of the verb, meaning that no overt NP can be
present in the clause to fill this semantic role. So, while UMR treats
the whole stem *teb-e'ei-s* as the predicate, it also identifies a
separate concept for 'head', which has the :Theme participant role as
seen in the UMR corresponding to example
[\[3-1-3-1 (1)\]](#3-1-3-1 (1)).

On the other hand, in more grammaticalized noun incorporation
constructions, the incorporated noun does not "replace" one of the
verbal arguments. Instead, the incorporated noun only denotes a very
general class of objects, and an independent NP can be present in the
clause to specify the kind of object at hand. Such noun incorporation
constructions are often referred to as "verbal classifiers". For
example, the Arapaho instrumental suffix *-s* indicates that the
"remove"-event is done by means of a blade-like implement, but still an
independent NP can appear to specify the instrument. For such
grammaticalized noun incorporation constructions, no separate concept
corresponding to the incorporated noun is identified. A participant
with the :Instrument role is only identified if it is expressed as an
overt NP in the clause.

This treatment of noun incorporation means that a certain amount of
linguistic analysis must be done prior to UMR annotation. If the
language at hand has one or more noun incorporation construction(s),
annotators need to know for any individual construction whether or not
it allows the expression of the incorporated participant as an
independent overt NP. Of course, grammaticalization is a continuous
process, and therefore noun incorporation constructions are likely to be
found on a continuum between these two end points. However, we map this
continuum onto a discrete choice for annotators by taking the ability of
an incorporated noun to co-occur with an independent NP as criterial.

##### Part 3-1-3-2. Valency-changing operations

Secondly, constructions used to change the valency of verbs (causatives,
applicatives, reflexives etc.) can cross-linguistically either express
the two concepts at hand in separate words (e.g. English *I **made** him
**eat***), or combine the two concepts into a single word (e.g. Sanapaná
*as-**tav-kes**-ke'* 'I made her/him eat'). In order to assess whether
one or two concepts should be identified for UMR annotation, unity under
negation is chosen as a criterion.

In English Causatives, for instance, negation can apply to the causing
event and to the caused event separately as in
[\[3-1-3-2 (1)\]](#3-1-3-2 (1)), indicating that the causing event and the
caused event are construed as independent predicates. Therefore, a
"cause"-event is identified in addition to the "drink"-event expressed
by the verb root.

<span id="3-1-3-2 (1)" label="3-1-3-2 (1)">\[3-1-3-2 (1)\]</span> 

<span id="3-1-3-2 (1a)" label="3-1-3-2 (1a)">\[3-1-3-2 (1a)\]</span>

Grandmother made the kid drink the water.
```
(d/ drink
    :Cause (m/ make
    	:Actor (g/ grandmother)
    	:Aspect Performance
    	:Modstr Aff)
    :Actor (k/ kid)
    :Undergoer (w/ water)
    :Aspect Performance
    :Modstr Aff)

```
<span id="3-1-3-2 (1b)" label="3-1-3-2 (1b)">\[3-1-3-2 (1b)\]</span>

Grandmother did not make the kid drink the water.

<span id="3-1-3-2 (1c)" label="3-1-3-2 (1c)">\[3-1-3-2 (1c)\]</span>

Grandmother made the kid not drink the water.

Kukama, on the other hand, has a morphological causative, as in
[\[3-1-3-2 (2)\]](#3-1-3-2 (2)). The caused event and causing event cannot be
negated independently: if
[\[3-1-3-2 (2)\]](#3-1-3-2 (2)) is negated, negation necessarily scopes over
both, indicating that this form is construed in Kukama as denoting a
single event. Therefore, only a single predicate is identified
(corresponding to the whole verb stem *kuratata* 'make drink').

<span id="3-1-3-2 (2)" label="3-1-3-2 (2)">\[3-1-3-2 (2)\]</span> 
```
nai		kurata-ta	churan=ui	uni-pu
grandmother	drink-CAUS	kid=PST		water-INST
'Grandmother made the kid drink the water.'

(k/ kuratata 'make drink'
    :Causer (n/ nai 'grandmother')
    :Actor (c/ churan 'kid')
    :Undergoer (u/ uni 'water')
    :Aspect Performance
    :Modstr Aff)
```

This criterion will be used for all valency change concepts: if the
"lexical" concept expressed by the verb root and the valency change
concept can be negated independently, two events are identified, whereas
if they cannot be negated independently, only one event is identified
(corresponding to the derived verb stem). The semantics and valency of
such derived forms will be inferred from the participant role annotation
associated with the verb. Which valency changes lead to which argument
structures is detailed in section 3.2.1 of these guidelines.

##### Part 3-1-3-3. TAM categories

Third, some semantic categories such as (phasal) aspect, temporal
relations, and modal relations, can be expressed cross-linguistically
either through bound morphology or through separate words (often called
"auxiliaries").

Phasal aspectual meanings such as inchoative, completive, and
continuative, firstly, are never identified as separate events, even if
they are expressed through independent words. Instead, they will simply
inform the Aspect attribute label of the event they modify (section
3.3.1). This principle is illustrated in example
[\[3-1-3-3 (1)\]](#3-1-3-3 (1)). In
Manipuri, the inchoative concept and the "close"-meaning form part of
the same word, while in the English translation, they are expressed as
two different words (example from Bhat 1999). Nevertheless, in both the English and the Manipuri
UMR, only one event is identified (corresponding to concept of property
predication, in this case).

<span id="3-1-3-3 (1)" label="3-1-3-3 (1)">\[3-1-3-3 (1)\]</span> 
```
ce	əsi	mu-re
paper	this	black-change
'This paper has become black.'

(h/ have-mod-91					(h/ have-mod-91
    :ARG0 (c/ ce 'paper')			    :ARG0 (p/ paper)
    	:mod (s/ əsi 'this')			        :mod (t/ this)
    :ARG1 (m/ mu 'black')			    :ARG1 (b/ black)
    :Aspect Performance				    :Aspect Performance
    :Modstr Aff)				    :Modstr Aff)
```

Similarly, modal and temporal auxiliaries will not be identified
independently as events, but will instead inform the modal and temporal
dependency annotation: in English, for example, modal auxiliaries such
as *might* and *should* in *He **might/should** go to school* are not
identified as independent events, and neither are temporal auxiliaries
such as *have* and *be* in *She **has gone/is going** to school*. How
such meanings exactly inform the temporal and modal annotation is
detailed in sections 4.2 and 4.3 of these guidelines.

For some semi-modal concepts, there may be language-internal semantic
evidence that they are construed as independent concepts. For instance,
in the English desiderative construction in
[\[3-1-3-3 (2)\]](#3-1-3-3 (2)), the desire-event can be modalized
independently of the "go"-event, indicating that desires are construed
as independent events in English. The UMR therefore has predicates for
both *want* and *go*.

<span id="3-1-3-3 (2)" label="3-1-3-3 (2)">\[3-1-3-3 (2)\]</span> 
<span id="3-1-3-3 (2a)" label="3-1-3-3 (2a)">\[3-1-3-3 (2a)\]</span> She wants to go to school.
```
(w/ want-01
    :ARG0 (p/ person :ref 3SGF)
    :ARG1 (g/ go-01
    	:ARG1 p
        :ARG4 (s/ school)
        :Aspect Performance
        :MOD w)
    :Aspect State
    :Modstr Aff)
```

<span id="3-1-3-3 (2b)" label="3-1-3-3 (2b)">\[3-1-3-3 (2b)\]</span> She may want to go to school.

However, if in a language the desire-event cannot be modalized
independently from the desired event, no separate event is identified
for the desire-semantics. Instead, the desiderative is taken into
account in the modal annotation, as detailed in section 4.3. For three
other semi-modal concepts, the same guidelines as to concept-word
mismatches are used as for desideratives: this is the case for conatives
('try to'), optatives ('wish that'), and frustratives ('fail to').

##### Part 3-1-3-4. Associated Motion

Associated motion constructions are treated in a similar way to
semi-modals. If associated motion events can have their own argument
structure (i.e. if they can co-occur with NPs expressing start points or
end points of motion events), these motion events are identified as
separate predicates in the UMR. If they cannot take their own argument
structure, only one event is identified.

For instance, the Sanapaná associated motion construction in
[\[3-1-3-4 (1)\]](#3-1-3-4 (1)) expresses that the sleeping-event takes place during a motion event
towards the deictic center: the suffix *-ant* essentially means that the
event expressed by the verb root happens "while coming here". As shown
in [\[3-1-3-4 (1)\]](#3-1-3-4 (1)), this construction can co-occur with a spatial NP. However, such a spatial NP can only express the location of the sleeping-event rather
than the goal or the start point of the motion event. It is therefore
better analyzed as a circumstantial locative belonging to the
"sleep"-event expressed by the verb root than as an argument of the
motion event. The motion event itself therefore has no independent
argument structure, and only one event is identified for UMR annotation.

<span id="3-1-3-4 (1)" label="3-1-3-4 (1)">\[3-1-3-4 (1)\]</span> 
```
en-na'-ten-ek-ant-a'		La	Esperanza
1PL-DSTR-sleep-PST/HAB-NOM	La	Esperanza
'We slept in La Esperanza while coming here'

(t/ enna'tenekanta' 'sleep while coming'		(s/ sleep-01
    :Undergoer (p/ person :ref 1PL)			    :ARG0 (p/ person :ref 1PL)
    :Place (l/ location					    :Place (l/ location
    	:name (n/ name					        :name (n/ name
            :op1 ("La")						    :op1 ("La")
            :op2 ("Esperanza")))				    :op2 ("Esperanza")))
    :Aspect State					    :Temporal (c/ come-01
    :Modstr Aff)					        :ARG1 p
    								:ARG4 (h/ here)
                                                        	:Aspect Activity
                                                        	:Modstr Aff)
                                                    	    :Aspect State
                                                   	    :Modstr Aff)
```

The English "venitive" construction in the translational equivalent of
[\[3-1-3-4 (1)\]](#3-1-3-4 (1)), however, can co-occur with an NP which is clearly an argument of the "come"-event: one could say, for instance *We slept in La Esperanza
while coming here **from Puerto Casado***. Therefore, the motion event
and the "sleep"-event are construed in English as two independent
events, and are annotated in UMR as two separate predicates.

##### Part 3-1-3-5. Non-verbal clauses

Many types of "non-verbal clauses", such as predicate nominals and
predication of properties, possession, and location (see section 3-1-1-3 for the predicates UMR predicates that are used to annotate these meanings), show different
mappings between concepts and words across languages. According to typological studies by Stassen (1997, 2009), Heine (1997), and Creissels (2019), there are three cross-linguistically common strategies for the expression of such meanings. English uses an
easily identifiable "verbal" predicate with argument NPs, as seen in the
English translational equivalents of the Kukama examples in
[\[3-1-3-5 (1)\]](#3-1-3-5 (1)) and [\[3-1-3-5 (2)\]](#3-1-3-5 (2)). In English, these constructions do not pose
serious problems to the predicate-argument structure of UMR - one could
simply identify the "have" or "be"-verb as a predicate, and the NPs in
the clause as its arguments.

In the Kukama object predication construction in
[\[3-1-3-5 (1)\]](#3-1-3-5 (1)), however, the predicate does not map to
an overt word: object predication is expressed through juxtaposition of
two NPs, with the predicational meaning implicit but inherent in the
construction. In the Kukama thetic possession construction in [\[3-1-3-5 (2)\]](#3-1-3-5 (2)), on the other hand, the possessum
and the relation of possession are expressed together as a single word
which functions as a predicate: something that is typically thought of
as an "argument" is predicativized. In languages that use the construction type exemplified in [\[3-1-3-5 (2)\]](#3-1-3-5 (2)), there is only one of the participants that can act as the predicate cross-linguistically. For example, in languages that use a [\[3-1-3-5 (2)\]](#3-1-3-5 (2))-type strategy for object predication, it is always the object category participant and never the theme participant that morphosyntactically looks like a predicate. Both these structures pose problems
for the annotation of predicate-argument structure if we want to adhere
to our position of holistic annotation of words, since there is no
separate material that can be identified as a predicate.

<span id="3-1-3-5 (1)" label="3-1-3-5 (1)">\[3-1-3-5 (1)\]</span> 
```
ajan	kunumi		tsumi
this	young.man	shaman
'This young man is a shaman.'

(h/ have-role-91						(h/ have-role-91
    :ARG0 (k/ kunumi 'young man')				    :ARG0 (m/ man)
    	:mod (a/ ajan 'this')					        :mod (y/ young)
    :ARG1 (t/ tsumi 'shaman')						:mod (t/ this)
    :Aspect State						    :ARG1 (s/ shaman)
    :Modstr Aff)						    :Aspect State
    								    :Modstr Aff)
```

<span id="3-1-3-5 (2)" label="3-1-3-5 (2)">\[3-1-3-5 (2)\]</span> 
```
Mijiri-tin	ɨara-yara
Miguel-CER	canoe-owner
'Miguel does have a canoe.' lit. 'Miguel is a canoe-owner.'

(a/ ɨara-yara 'have canoe'					(h/ have-03
    :ARG0 (m/ Mijiri 'Miguel')					    :ARG0 (m/ Miguel)
    :ARG1 (a/ ɨara 'canoe')					    :ARG1 (c/ canoe)
    :Aspect State						    :Aspect State
    :Modstr Aff)						    :Modstr Aff)
```

We propose a set of seven abstract concept predicates each corresponding
to a discrete "non-verbal clause" function (table
[\[tab:nonverbal\]](#tab:nonverbal)). When there is no overt predicate-word, as
in [\[3-1-3-5 (1)\]](#3-1-3-5 (1)), we assume that annotators will be able
to recognize the type of non-verbal clause function they are dealing
with. They should use an abstract predicate concept from table
[\[tab:nonverbal\]](#tab:nonverbal) as predicative core of the graph, and use the :ARG0 and :ARG 1 numbered argument roles to link the arguments to this predicate as specified in
the table (see also section 3-2-1-1-1 for more in-depth treatment of the argument structure annotation with these predicates).

In constructions with predicativized arguments, such as
[\[3-1-3-5 (2)\]](#3-1-3-5 (2)), UMR takes the same approach as for
pronominal affixation. Both a predicate concept and an argument concept
are identified separately, but linked to the same word token in the
sentence - in this case *ɨara-yara*. As can be seen in the example UMRs
above, the resulting graphs have similar structures regardless of
whether a languages uses an overt-predicate strategy, a zero-predicate
(juxtaposition) strategy, or a predicativized argument strategy for such
"non-verbal clause" meanings.


<span id="tab:nonverbal" label="tab:nonverbal">\[tab:nonverbal\]</span>
|     Clause Type      |              Predicate               |           ARG0          |         ARG1         |
| :-------: | :----------------------------------: | :------------------------------: | :-------------------------: |
| Thetic Possession  |         have-03         |      possessor       |     possessum      |
|  Predicative Possession   |            belong-01             |       possessum       | possessor |
|     Thetic Location      |     exist-91    |       location        |      theme      |
| Predicative Location  |         have-location-91         |      theme       |     location      |
| Property Predication  |         have-mod-91         |      theme       |     property      |
| Object Predication  |         have-role-91         |      theme       |     object category      |
| Equational  |         identity-91         |      theme       |     equated referent      |
 
##### Part 3-1-3-6. Multi-word concepts

In languages with simpler morphology, the opposite situation, *multi-word concepts* may arise. Multi-word concepts can simply be handled by
concatenating the lemmatized words, as in [\[3-1-3-6 (1)\]](#3-1-3-6 (1)).

<span id="3-1-3-6 (1)" label="3-1-3-6 (1)">\[3-1-3-6 (1)\]</span>

<span id="3-1-3-6 (1a)" label="3-1-3-6 (1a)">\[3-1-3-6 (1a)\]</span> So I normally steep it in hot water , then take it out and stir - fry it.
```
(c / cause-01
      :ARG1 (a2 / and
            :op1 (s / steep-01
	          :aspect Habitual
                  :ARG0 (i / i)
                  :ARG1 (i2 / it)
                  :ARG2 (w / water
                        :ARG1-of (h / hot-05)))
            :op2 (a / and
                  :op1 (t / take-out-11
		        :aspect Habitual
                        :ARG0 i
                        :ARG1 i2)
                  :op2 (s2 / stir-01
		        :aspect Habitual
                        :ARG0 i
                        :ARG1 i2)
                  :op3 (f / fry-01
		        :aspect Habitual
                        :ARG0 i
                        :ARG1 i2)
                  :time (t3 / then)))
      :ARG1-of (n / normal-02))
```

<span id="3-1-3-6 (1b)" label="3-1-3-6 (1b)">\[3-1-3-6 (1b)\]</span> The moral aspects of the movement intrigued him as well
```
(i / intrigue-01
      :aspect Performance
      :ARG0 (a / aspect
            :ARG1-of (m / moral-02)
            :poss (m2 / movement-07))
      :ARG1 (h / he)
      :mod (a2 / as-well))
```


#### Part 3-1-4. Word senses
 
 UMR allows concepts to be word senses. In order to annotate word sense, it is necessary to first have a sense inventory for all words that need to be sense disambiguated. For languages that do not have a sense inventory, the concept can simply be lemmas. It is also possible that a language only has a sense inventory for a subset of the words. This is the case with English [\[3-1-4 (1)\]](#3-1-4 (1)) and Chinese [\[3-1-4 (2)\]](#3-1-4 (2)), where word senses are defined for predicates together with their arguments in *frame files*.

<span id="3-1-4 (1)" label="3-1-4 (1)">\[3-1-4 (1)\]</span> The school has approximately 570 pupils.
``` 
(h / have-03
      :ARG0 (s / school)
      :ARG1 (p / pupil
            :quant (a / approximately :op1 570)))
```

<span id="3-1-4 (2)" label="3-1-4 (2)">\[3-1-4 (2)\]</span>
 ```
 并且 还 有 很多 高层 的 人物 哦 ！
There will even be many VIPs!
(x11 / and
      :op2  (x3 / 有-03
               :mod (x2 / 还)
               :arg1  (x7 / 人物
                         :mod  (x5 / 高层)
                         :quant (x4 / 很多))
            :mode  Expressive))
```
 


 
 #### Part 3-1-5. Scope for Quantification and negation

To facilitate the translation of UMR into first-order expressions to support logical inference,
we add a **scope** concept to represent the relative order of the predicate, quantified concept and negated concept.
In most cases, the order of these elements are interpreted in textual order, and do not need an over scope annotation.
The scope annotation is only needed when these elements are interpreted "out-of-order", as in [\[3-1-5 (1)\]](#3-1-5 (1)).

<span id="3-1-5 (1)" label="3-1-5 (1)">\[3-1-5 (1)\]</span>
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

#### Part 3-1-6. Discourse-relations
 
### Part 3-2. UMR relations 

   #### Part 3-2-1. Participant roles 
   
Every entity and event identified as a participant is related to an
event (the event that it is dependent on) and annotated with a
participant role label. The participant role annotation looks rather
different at the different stages of the road map. The factor which
determines where a language begins on the road map is whether there is
an existing PropBank-style lexicon (frame files) for the language, which defines predicate-specific roles. An English PropBank
frame file is shown in [\[3-2-1 (1)\]](#3-2-1 (1)).

<span id="3-2-1 (1)" label="3-2-1 (1)">\[3-2-1 (1)\]</span>
```

Predicate: give.01  
	Roles:    
	Arg0: giver   
	Arg1: thing given    
	Arg2: entity given to    

```

Following AMR, UMR uses PropBank frame files to annotate lexicalized
participant roles. But, this only works for languages which have
PropBank-style frame files. This is considered the ‘Stage 2’ participant
role annotation (see §[3-2-1-2](#3-2-1-2)). The Stage 1 annotation involves
using a set of general participant roles, while building a lexicon of
PropBank-style frame files in order to move towards Stage 2 annotation.

Some types of valency alternations (or, argument structure alternations)
are indicated in the participant role annotation; other types of
alternations are not annotated in UMR. Not all valency alternations have
the same relationship between the basic construction and the non-basic
construction. Givón (1994) distinguishes semantic and pragmatic valency
alternations. In semantic alternations, the basic and non-basic
constructions differ in terms of the semantic content that they express,
i.e., they don’t refer to the same “real-world” event. Reciprocals are
an example of a semantic alternation, seen below in
[\[3-2-1 (2)\]](#3-2-1 (2)) from Torau (Parkinson 2018:53).

<span id="3-2-1 (2)" label="3-2-1 (2)">\[3-2-1 (2)\]</span>

<span id="3-2-1 (2a)" label="3-2-1 (2a)">\[3-2-1 (2a)\]</span>

ta-di=lo daki-a tioni arimi ta besu  
<span class="smallcaps">pfv</span>-3<span class="smallcaps">pl.</span>S=go
find-3<span class="smallcaps">sg</span>O man feel.sorry
3<span class="smallcaps">sg.pfv</span> be.hungry  
‘When they found him, the poor many was hungry.’

<span id="3-2-1 (2b)" label="3-2-1 (2b)">\[3-2-1 (2b)\]</span>

ta-di=lama ari da-daki uua=i  
<span class="smallcaps">pfv</span>-3<span class="smallcaps">pl</span>S=<span class="smallcaps">tam</span>
<span class="smallcaps">recp</span>
<span class="smallcaps">rdp</span>-find
in.that.direction=<span class="smallcaps">loc</span>  
‘They had found each other.’

The event described in [\[3-2-1 (2a)\]](#3-2-1 (2a)) is different than the
event described in [\[3-2-1 (2b)\]](#3-2-1 (2b)). This is in contrast to
valency alternations which reflect a pragmatic difference between the
basic and non-basic construction. With pragmatic alternations, both
constructions refer to the same “real-world” event, but they package
that information differently, often in terms of the topicality (or,
discourse salience) of participants. Passive constructions are an
example of a pragmatic valency alternation, as seen in
[\[3-2-1 (3)\]](#3-2-1 (3)) from Balinese (Shibatani and Artawa 2013).

<span id="3-2-1 (3)" label="3-2-1 (3)">\[3-2-1 (3)\]</span>

<span id="3-2-1 (3a)" label="3-2-1 (3a)">\[3-2-1 (3a)\]</span> Anake muani
cenik ento ngajeng buahe ento. anak=e muani cenik ento ngajeng buah=e
ento  
person=<span class="smallcaps">def</span> male small that eat
fruit=<span class="smallcaps">def</span> that  
‘The boy ate the fruit.’

<span id="3-2-1 (3b)" label="3-2-1 (3b)">\[3-2-1 (3b)\]</span> Buahe ento
ajenga teken anake muani cenik ento. buah=e ento ajeng=a teken anak=e
muani cenik ento  
fruit=<span class="smallcaps">def</span> that
eat=<span class="smallcaps">pass</span> by
person=<span class="smallcaps">def</span> male small that  
‘The fruit was eaten by the boy.’

Here, [\[3-2-1 (3a)\]](#3-2-1 (3a)) and [\[3-2-1 (3b)\]](#3-2-1 (3b)) could
refer to the same event, with the main difference being the saliency or
topicality of *anak=e muani cenik* ‘the boy’.

Broadly, UMR indicates semantic valency alternations with the
participant role annotation, while pragmatic alternations are not
reflected in the UMR. This means that the participant role annotations
for [\[3-2-1 (2a)\]](#3-2-1 (2a)) and [\[3-2-1 (2b)\]](#3-2-1 (2b)) would be
different, where as the participant role annotation for
[\[3-2-1 (3a)\]](#3-2-1 (3a)) and [\[3-2-1 (3b)\]](#3-2-1 (3b)) would be the
same. The annotations for valency alternations also depend on the stage
of the road map, so that will be detailed below.

##### 3-2-1-1. Stage 1

At Stage 1, a set of general (i.e., non-lexicalized) semantic roles are
used. These certainly will not map exactly to the grammatical marking of
argument phrases in any language, but this set of roles was selected
based on cross-linguistic patterns of argument marking. The set of
participant role labels, a brief description for each label, and
examples are shown below in Table 5.

<div id="tab:generalroles">

| **UMR Annotation**                         | **Definition**                                                                                                 | **Example**                                                                                                                |
| :----------------------------------------- | :------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------- |
| <span class="smallcaps">`actor`</span>       | animate entity that initiates the action                                                                       | **the doctor** laughed <br /> **the boy** ate a salad                                                                             |
| <span class="smallcaps">`undergoer`</span>   | entity (animate or inanimate) that is affected by the action                                                   | **the papers** burned <br /> he burned **the onions**                                                                             |
| <span class="smallcaps">`theme`</span>       | entity (animate or inanimate) that moves from one entity to another entity, either spatially or metaphorically | she put **the books** on the shelf <br /> she tore **a page** from the book <br /> he gave **a sandwich** to me <br /> she told him **a story** |
| <span class="smallcaps">`recipient`</span>   | animate entity that gains possession (or at least temporary control) of another entity                         | he gave a sandwich **to me** <br /> she told **him** a story                                                                      |
| <span class="smallcaps">`force`</span>       | inanimate entity that initiates the action                                                                     | **the wind** knocked down the tree                                                                                         |
| <span class="smallcaps">`causer`</span>      | animate entity that acts on another animate entity to initiate the action                                      | **the mother** made her child eat the broccoli                                                                             |
| <span class="smallcaps">`experiencer`</span> | animate entity that cognitively or sensorily experiences a <span class="smallcaps">`stimulus`</span>             | **the dog** heard a sound                                                                                                  |
| <span class="smallcaps">`stimulus`</span>    | entity (animate or inanimate) that is experienced by an <span class="smallcaps">`experiencer`</span>             | the dog heard **a sound**                                                                                                  |
| <span class="smallcaps">`instrument`</span>  | inanimate entity that is manipulated by an external causer in order to initiate the action                     | she hit him with **a broom**                                                                                               |
| <span class="smallcaps">`companion`</span>   | animate entity that acts with the <span class="smallcaps">`actor`</span> to initiate the action                  | he cooked dinner with **his wife**                                                                                         |
| <span class="smallcaps">`material`</span>    | entity (inanimate) that is transformed into a new entity                                                       | he made a roux with **flour and butter**                                                                                   |
| <span class="smallcaps">`source`</span>      | entity from which the <span class="smallcaps">`theme`</span> detaches                                            | he plucked a flower from the **the bush**                                                                                  |
| <span class="smallcaps">`place`</span>       | location at which the action takes place                                                                       | he read a book in **the garden**                                                                                           |
| <span class="smallcaps">`start`</span>       | location at which a motion event begins                                                                        | she biked from **her house**                                                                                               |
| <span class="smallcaps">`goal`</span>        | location at which the action ends, the end point at which the <span class="smallcaps">`theme`</span> arrives     | she put the books on **the shelf**                                                                                         |
| <span class="smallcaps">`affectee`</span>    | animate entity which the action has a positive or negative influence on, i.e. beneficiary or maleficiary       | he made a cake for **the dog** <br /> she stole a watch from **the CEO**                                                          |
| <span class="smallcaps">`cause`</span>       | inanimate entity that causes the action to happen                                                              | he was late because of **the fire**                                                                                        |
| <span class="smallcaps">`manner`</span>      | manner in which the action takes place                                                                         | she exercised by **lifting weights**                                                                                       |
| <span class="smallcaps">`reason`</span>      | motivation for the <span class="smallcaps">`actor`</span> to initiate the action                                 | they got married because **they are in love**                                                                              |
| <span class="smallcaps">`purpose`</span>     | intended event that results from the action                                                                    | they dropped water in order to **fight the fires**                                                                         |
| <span class="smallcaps">`temporal`</span>    | event that has a temporal relation with the action                                                             | she left after **dinner**                                                                                                  |
| <span class="smallcaps">`extent`</span>      | measurement phrase                                                                                             | he ran **seven miles**                                                                                                     |
| <span class="smallcaps">`other`</span>       | this role can be used when an annotator is unsure of which role is appropriate                                 |                                                                                                                            |

Table 5: UMR Non-lexicalized roles
</div>

These general semantic roles can be categorized based on the types of
events with which they occur, shown in Table 6. Some
participant roles express the external cause of an event; these can
occur with many semantic classes of events. Similarly, the
“circumstantial” type semantic roles can occur with a wide range of
semantic event classes.

<div id="tab:catroles">

|            **External Cause**             |                        **Central Event**                         |           **Circumstantial**            |
| :---------------------------------------: | :--------------------------------------------------------------: | :-------------------------------------: |
|   <span class="smallcaps">`actor`</span>    |                        (CHANGE OF) STATE:                        | <span class="smallcaps">`affectee`</span> |
| <span class="smallcaps">`companion`</span>  |        <span class="smallcaps">`material, undergoer`</span>        |  <span class="smallcaps">`place`</span>   |
| <span class="smallcaps">`instrument`</span> |                         MOTION/LOCATION:                         |  <span class="smallcaps">`manner`</span>  |
|   <span class="smallcaps">`force`</span>    | <span class="smallcaps">`theme, goal, start, source, place`</span> | <span class="smallcaps">`purpose`</span>  |
|   <span class="smallcaps">`causer`</span>   |                            TRANSFER:                             |  <span class="smallcaps">`reason`</span>  |
|                                           |         <span class="smallcaps">`theme, recipient`</span>          |  <span class="smallcaps">`cause`</span>   |
|                                           |                          EXPERIENTIAL:                           | <span class="smallcaps">`temporal`</span> |
|                                           |       <span class="smallcaps">`experiencer, stimulus`</span>       |  <span class="smallcaps">`extent`</span>  |

Table 6: Categorization of UMR non-lexicalized roles
</div>

For the roles that characterize the central participant(s) in the event,
the best way to decide which participant role label a given participant
should receive is to consider the semantic class of the event. The
<span class="smallcaps">`undergoer`</span> role only occurs with
change-of-state events, construed broadly to include creation and
contact events as well. The <span class="smallcaps">`undergoer`</span>
role is used for the entity that undergoes the change-of-state, is the
endpoint of force in a contact event, or is created in a creation event,
as seen in [\[3-2-1-1 (1)\]](#3-2-1-1 (1)). The <span class="smallcaps">`material`</span>
role only occurs with creation events, as in
[\[3-2-1-1 (1c)\]](#3-2-1-1 (1c)), and is used for the raw materials
that are transformed into the created object.

<span id="3-2-1-1 (1)" label="3-2-1-1 (1)">\[3-2-1-1 (1)\]</span>

<span id="3-2-1-1 (1a)" label="3-2-1-1 (1a)">\[3-2-1-1 (1a)\]</span>
```
The ice cube melted.  

(m / melt  
	:undergoer (i / ice cube))
```
<span id="3-2-1-1 (1b)" label="3-2-1-1 (1b)">\[3-2-1-1 (1b)\]</span> 
```
The enemy sank the ship. 

(s1 / sank  
	:actor (e / enemy) 
	:undergoer (s2 / ship))

```
<span id="#3-2-1-1 (1c)" label="#3-2-1-1 (1c)">\[#3-2-1-1 (1c)\]</span> 
```
She built a house out of wood. 

(b / build  
	:actor (s / she)  
	:undergoer (h / house) 
	:source (w / wood))
```
<span id="#3-2-1-1 (1d)" label="#3-2-1-1 (1d)">\[#3-2-1-1 (1d)\]</span> 
```
He hit the stick against the fence.  

(h1 / hit 
	:actor (h2 / he)  
	:instrument (s / stick)  
	:undergoer (f / fence)) 
```

The <span class="smallcaps">experiencer</span> and
<span class="smallcaps">stimulus</span> roles always occur with
experiential events, as seen in [\[3-2-1-1 (4)\]](#3-2-1-1 (4)). The
<span class="smallcaps">experiencer</span> role is used for the
mental-level entity which attends to, reacts to, or passively
experiences the <span class="smallcaps">stimulus</span> role.

<span id="3-2-1-1 (4)" label="3-2-1-1 (4)">\[3-2-1-1 (4)\]</span>

<span id="3-2-1-1 (4a)" label="3-2-1-1 (4a)">\[3-2-1-1 (4a)\]</span>
```
The audience listened to the concerto.  

(l / listen
	:experiencer (a / audience) 
	:stimulus (c / concerto))
```
<span id="3-2-1-1 (4b)" label="3-2-1-1 (4b)">\[3-2-1-1 (4b)\]</span>
```
The cat startled me.

(s / startle  
	:experiencer (m / me)
	:stimulus (c / cat)) 
```


The `start, goal`, and
`source` roles only occur with motion
events; `place` has two different uses, one
with Motion/Location events and one with other event classes.
`start`,
`goal`, and
`place` are used for locations –
`start` is the location from which motion
originates, as in [\[3-2-1-1 (5a)\]](#[3-2-1-1 (5a)),
`goal` is the location in which motion
ends, as in [\[[3-2-1-1 (5b)\]](#3-2-1-1 (5b)) and [\[3-2-1-1 (5c)\]](#3-2-1-1 (5c)),
and `place` is used for static locations,
as in [\[3-2-1-1 (5d)\]](#3-2-1-1 (5d)). The
`source` role is in the removal subclass of
motion events; it is used for the entity from which the
`theme` is removed, as in
[\[3-2-1-1 (5e)\]](#3-2-1-1 (5e)). With motion events, the
`theme` role is used for the entity that
moves (unless the motion is volitional), as in
[\[3-2-1-1 (5a)\]](#3-2-1-1 (5a)).

<span id="3-2-1-1 (5)" label="3-2-1-1 (5)">\[3-2-1-1 (5)\]</span>

<span id="[3-2-1-1 (5a)" label="[3-2-1-1 (5a)">\[[3-2-1-1 (5a)\]</span> 
```
She walked home from the store.

(f / fall 
	:theme (l / leaf)  
	:goal (g / ground))  
```
<span id="3-2-1-1 (5b)" label="3-2-1-1 (5b)">\[3-2-1-1 (5b)\]</span> 
```
The leaf fell to the ground.

(w / walk 
	:actor (s1 / she) 
	:goal (h / home)  
	:start (s2 / store))  
```
<span id="3-2-1-1 (5c)" label="3-2-1-1 (5c)">\[3-2-1-1 (5c)\]</span> 
```
He put the books in a box.

(p / put  
	:actor (h / he)  
	:theme (b1 / books)  
	:goal (b2 / box))  

```
<span id="3-2-1-1 (5d)" label="3-2-1-1 (5d)">\[3-2-1-1 (5d)\]</span> 
```
She is sitting on the couch.

(s1 / sit  
	:actor (s2 / she)  
	:place (c / couch))  
```
<span id="3-2-1-1 (5e)" label="3-2-1-1 (5e)">\[3-2-1-1 (5e)\]</span> 
```
He picked some berries from the bush.

(p / pick
	:actor (h / he) 
	:theme (b1 / berries)  
	:source (b2 / bush)) 
```
The `recipient` role only occurs with
transfer events, or metaphorical transfer events like communication.
With these events, the initiator of the transfer is an
`actor`, the entity that is transferred is
the `theme` and the entity that the
`theme` is transferred to is labelled as
the `recipient`. For transfer of possession
events that express the original possessor of the
`theme`, the original possessor is
annotated as `affectee`, as in
[\[3-2-1-1 (6d)\]](#3-2-1-1 (6d)).

<span id="3-2-1-1 (6)" label="3-2-1-1 (6)">\[3-2-1-1 (6)\]</span>

<span id="3-2-1-1 (6a)" label="3-2-1-1 (6a)">\[3-2-1-1 (6a)\]</span> 
```
He gave the cat some wet food.

(g / give  
	:actor (h / he)  
	:theme (w / wet food)  
	:recipient (c / cat))
```

<span id="3-2-1-1 (6b)" label="3-2-1-1 (6b)">\[3-2-1-1 (6b)\]</span> 
```
I showed the pictures to her.

(s / show  
	:actor (i / I)  
	:theme (p / picture)
	:recipient (h / her)) 
```

<span id="3-2-1-1 (6c)" label="3-2-1-1 (6c)">\[3-2-1-1 (6c)\]</span> 
```
She told me that they they’re attending.

(t1 / tell`  
	:actor (s / she)  
	:recipient (m / me)  
	:theme ( a / attend  
	:actor (t2 / they))) 
```

<span id="3-2-1-1 (6d)" label="3-2-1-1 (6d)">\[3-2-1-1 (6d)\]</span> 
```
She stole the information from a competitor.

(s1 / steal
	:actor (s2 / she)
	:theme (i / information) 
	:source (c / competitor)) 
```

The other participant roles can occur pretty much freely with any semantic class of event. The external cause roles are used to annotate entities that bring about the central event. The
`actor` role is used for “active”
single-participant events, in which the single participant acts
volitionally to bring about the event, as in
[\[3-2-1-1 (7a)\]](#3-2-1-1 (7a)). This contrasts with “inactive”
single-participant events, in which the single participant undergoes a
change outside of its control, as in [\[3-2-1-1 (1a)\]](#3-2-1-1 (1a))
above. See Appendix [8](#ap:verbspr) for examples of single-participant
verbs and their participant role annotation. The
<span class="smallcaps">actor</span> role is also used for animate
entities that initiate an action, as in [\[3-2-1-1 (1b)\]](#3-2-1-1 (1b))
above.

The `companion` role is used for the entity
that helps the `actor` bring about the
action, as in [\[3-2-1-1 (7b)\]](#3-2-1-1 (7b)). Note that this role is only annotated when the `companion`
participant is expressed separately from the
`actor`. Plural participants and conjoined
participants, as in [\[3-2-1-1 (7c)\]](#3-2-1-1 (7c)) and
[\[3-2-1-1 (7d)\]](#3-2-1-1 (7d)), are annotated with a single
`actor` role. In some languages, a marker
may be ambiguous between a comitative marker and a conjunction. When the two participants are expressed separately in the clause, they should be treated as separate participants, annotated with`actor` and `companion`. When they are expressed
together, they are treated as a single
`actor` participant.

The `instrument` role is used for an entity
that is manipulated by one of the other external cause roles, often an `actor`, in order to initiate the action.
The entity which manipulates the
`instrument` may or may not be present in
the clause; see [\[3-2-1-1 (7e)\]](#3-2-1-1 (7e)) and
[\[3-2-1-1 (7f)\]](#3-2-1-1 (7f)).

The `force` role is used for physical
entities which initiate an action, or cause another entity to undergo a
change, as in [\[3-2-1-1 (7g)\]](#3-2-1-1 (7g)). Finally, the
`causer` role is used for the external
initiator in some causative constructions, see [4.1.2](#pr0:alts).


<span id="3-2-1-1 (7)" label="3-2-1-1 (7)">\[3-2-1-1 (7)\]</span>

<span id="3-2-1-1 (7a)" label="3-2-1-1 (7a)">\[3-2-1-1 (7a)\]</span>
```
He winked.

(w / wink
	:actor (h / he))
```

<span id="3-2-1-1 (7b)" label="3-2-1-1 (7b)">\[3-2-1-1 (7b)\]</span> 
```
Jane wrote the paper with Chris.

(w / write 
	:actor (J / Jane)  
	:companion (C / Chris)  
	:undergoer (p / paper)) 
```

<span id="3-2-1-1 (7c)" label="3-2-1-1 (7c)">\[3-2-1-1 (7c)\]</span> 
```
They wrote the paper.

(w / write  
	:actor (t / they)
	:undergoer (p / paper))
```

<span id="3-2-1-1 (7d)" label="3-2-1-1 (7d)">\[3-2-1-1 (7d)\]</span> 
```
Jane and Chris wrote the paper.

(w / write
	:actor (J / Jane and Chris) 
	:undergoer (p / paper))  
```

<span id="3-2-1-1 (7e)" label="3-2-1-1 (7e)">\[3-2-1-1 (7e)\]</span> 
```
She sliced the bread with a knife.

(s / slice
	:actor (s / she) 
	:instrument (k / knife) 
	:undergoer (b / bread))
```

<span id="3-2-1-1 (7f)" label="3-2-1-1 (7f)">\[3-2-1-1 (7f)\]</span>
```
The knife sliced through the bread.

(s / slice 
	:instrument (k / knife)  
	:undergoer (b / bread)) 
```

<span id="3-2-1-1 (7g)" label="3-2-1-1 (7g)">\[3-2-1-1 (7g)\]</span> 
```
The storm damaged the power lines.

(d / damage 
	:actor (s / storm)  
	:undergoer (p / power lines)) 
```

See Table 5 for examples of the circumstantial
roles. In addition, there is an `other`
placeholder role that can be used when annotators are unsure of which participant role annotation is accurate for a particular participant. Also see Appendix [8](#ap:verbspr) for a list of verbs and how their microroles are annotated.

At Stage 1, participant roles that aren’t explicitly expressed in the clause do not have to be annotated, even if they are implied by the context. If the annotator is certain about them, however, they can be annotated. For example, in [\[3-2-1-1 (8)\]](#3-2-1-1 (8)), the
`goal` is left implicit; at Stage 1, this
role may be left out of the annotation.

<span id="3-2-1-1 (8)" label="3-2-1-1 (8)">\[3-2-1-1 (8)\]</span> 
```
They loaded the boxes.

(l  load  
	:actor (t / they)  
	:theme (b / boxes)) 
```

###### 3-2-1-1-1. Nonverbal clauses

There is a small set of predicates that use lexicalized roles at all stages of the road map; therefore, frame files for these predicates are created at Stage 1 annotation. These are the nonverbal clause predicates shown in Table 7. These are repeated below with their participant role annotation.

Each nonverbal clause predicate has an `ARG0` and an `ARG1`; these map
to the semantic roles as shown in Table 7.

<div id="tab:nonverbalprs">

| **Clause type**                  | **UMR Predicate** | **ARG0**     | **ARG1**           |
| :------------------------------- | :---------------- | :----------- | :----------------- |
| thetic/presentational possession | `have-03 `          | *possessor*  | *possession*       |
| predicative possession           | `belong-01`         | *possession* | *possessor*        |
| thetic/presentational location   | `exist-91`          | *location*   | *theme*            |
| predicative location             | `have-location-91`  | *theme*      | *location*         |
| property predication             | `have-mod-91`       | *theme*      | *property*         |
| object predication               | `have-role-91`      | *theme*      | *object category*  |
| equational                       | `identity-91`       | *theme*      | *equated referent* |

Table 7: Nonverbal clause predicates

</div>

The argument that can be predicativized in some languages is always
`ARG1`. The examples in [\[3-2-1-1-1 (1)\]](#3-2-1-1-1 (1)) show how
nonverbal clauses are annotated with participant roles. Note that these
annotations will be the same at every stage of the road map.

<span id="3-2-1-1-1 (1)" label="3-2-1-1-1 (1)">\[3-2-1-1-1 (1)\]</span>

<span id="3-2-1-1-1 (1a)" label="3-2-1-1-1 (1a)">\[3-2-1-1-1 (1a)\]</span>
Thetic/presentational Possession - Kukama <br />

```
Mijiri-tin  ɨara-yara  
Miguel-cer  canoe-owner  
‘Miguel does have a canoe.’ (Lit. ‘Miguel is a canoe-owner’)

(e / ɨara-yara ‘has canoe’ 
	:ARG0 (m / Mijiri ‘Miguel’) 
	:ARG1 (i / ara ‘canoe’)) 
```

<span id="3-2-1-1-1 (1b)" label="3-2-1-1-1 (1b)">\[3-2-1-1-1 (1b)\]</span> Predicative
Possession - English <br />
```
The dog belongs to the teacher.  
  
(b / belong-01
	:ARG0 (d / dog) 
	:ARG1 (t / teacher)) 
```

<span id="3-2-1-1-1 (1c)" label="3-2-1-1-1 (1c)">\[3-2-1-1-1 (1c)\]</span> Thetic/presentational Location - English <br />
```
On the rock was a symbol.  
  
(e / exist-91
	:ARG0 (r / rock)
	:ARG1 (s / symbol))  
```

<span id="3-2-1-1-1 (1d)" label="3-2-1-1-1 (1d)">\[3-2-1-1-1 (1d)\]</span> Predicative
Location - Yabem (Dempwolff 1939) <br />
```
àndu  kê-kô 	malac  
house 3sg-be.at village  
‘The house is in the village.’

(h / have-location-91
	:ARG0 (a / àndu ‘house’)
	:ARG1 (m / malac ‘village’))
```

<span id="3-2-1-1-1 (1e)" label="3-2-1-1-1 (1e)">\[3-2-1-1-1 (1e)\]</span> Property
Predication - English <br />
```
The cat is black.  
  
(h / have-mod-91
	:ARG0 (c / cat) 
	:ARG1 (b / black))  

```

<span id="3-2-1-1-1 (1f)" label="3-2-1-1-1 (1f)">\[3-2-1-1-1 (1f)\]</span> Object Predication - Kukama <br />

```
ajan kunumi 	tsumi  
this young.man 	shaman  
‘This young man is a shaman.’

(h / have-role-91
	:ARG0 (k / kunumi ‘young man’)
	:ARG1 (t / tsumi ‘shaman’))  
```

<span id="3-2-1-1-1 (1g)" label="3-2-1-1-1 (1g)">\[3-2-1-1-1 (1g)\]</span> Object Equational - English <br />
```
She is the winner.  
  
(h / identity-91
:ARG0 (s / s)` 
:ARG1 (w / winner))
```

###### 3-2-1-1-2. Valency alternations
 
Certain types of semantic valency alternations are reflected in the participant role annotation. At Stage 1, these alternations influence the choice of general participant role labels. For information-packaging alternations, such as
passives, antipassives, or valency-rearranging applicatives,
participants are annotated in the same way as in the basic construction
in the language. If a participant is omitted, for example the agent in a passive construction as in [\[3-2-1-1-2 (1)\]](#3-2-1-1-2 (1)) from Berber (Guerssel 1986:52), then it simply isn’t annotated at Stage 1. This means that agentless passives and anticausatives will have the same participant role annotation at Stage 1. 

<span id="3-2-1-1-2 (1)" label="3-2-1-1-2 (1)">\[3-2-1-1-2 (1)\]</span>

<span id="3-2-1-1-2 (1a)" label="3-2-1-1-2 (1a)">\[3-2-1-1-2 (1a)\]</span> <br />
```
Y-usy 		wrba 	tafirast.  
3ms-pick.up 	boy:cst pear  
‘The boy picked up the pear.’

(u / usy ‘pick up’  
	:actor (w / wrba ‘boy’) 
	:undergoer (t / tafirast ‘pear’))
```

<span id="3-2-1-1-2 (1b)" label="3-2-1-1-2 (1b)">\[3-2-1-1-2 (1b)\]</span> <br />
```
T-ttw-asy
tfirast.  
3fs-detr-pick.up pear  
‘The pear was picked up.’

(t / ttw-asy ‘pick up’  
	:undergoer (t / tafirast ‘pear’)) 
```

**Causatives.** There are a few different types of causatives that
require different annotation solutions. For most causatives of
transitives, the causer is annotated as
`causer`, the causee as
`actor`, and the rest of the participants
receive the same annotation labels that they would in a a non-causative
construction. In [\[3-2-1-1-2 (2)\]](#3-2-1-1-2 (2)) from Kukama, *nai*
‘grandmother’ is annotated as `causer`,
the causee *churan* ‘kid’ is annotated as
`actor`, and *uni* ‘water’ as `undergoer`.

<span id="3-2-1-1-2 (2)" label="3-2-1-1-2 (2)">\[3-2-1-1-2 (2)\]</span>
```
nai 		kurata-ta churan=ui u	ni=pu  
grandmother 	drink-cau kid=pst 	water=ins  
‘Grandmother made the kid drink the water.’

(k / kuratata ‘make drink’  
	:causer (n / nai ‘grandmother’)  
	:actor (c / churan ‘kid’)  
	:undergoer (u / uni ‘water’))  
```

There are certain causatives of transitives which do not use the `causer` role. These are constructions which express transfer events, including mental/cognitive transfer. Some
languages express these types of events with monomorphemic verbs, like English, but other languages use causatives of transitive verbs.
Languages may differ in terms of which types of causative constructions are construed as transfer; in order to annotate the same semantic events in the same way across languages, the `actor, theme, recipient` roles are used for transfer of possession	(giving), sending, and mental transfer, which includes showing and communication. Bezhta in [\[3-2-1-1-2 (3b)\]](#3-2-1-1-2 (3b)) (Comrie, Khalilov, Khalilova 2015:560) uses the causative of *b-egā-yo* ‘see’ as equivalent to English *show*.


<span id="3-2-1-1-2 (3)" label="3-2-1-1-2 (3)">\[3-2-1-1-2 (3)\]</span>

<span id="3-2-1-1-2 (3a)" label="3-2-1-1-2 (3a)">\[3-2-1-1-2 (3a)\]</span> <br />
```
hogco-l 	raɬad 		b-egā-yo  
he.obl-lat 	sea(iii) 	iii-see-pst  
‘He saw the sea.’ 

(b / b-egā ‘see’
	:experiencer (h / hogco ‘he’)
	:stimulus (r / raɬad ‘sea’))

```

<span id="3-2-1-1-2 (3b)" label="3-2-1-1-2 (3b)">\[3-2-1-1-2 (3b)\]</span>
```
hogco 		kibba-l 	raɬad 		b-ega-l-lo  
he.obl(erg) 	girl.obl-lat 	sea(iii) 	iii-see-caus-pst  
‘He showed the sea to the girl.’

(b / b-ega-l ‘show’
	:actor (h / hogco ‘he’)
	:theme (r / ra`&#620;`ad ‘sea’)
	:recipient (k / kibba ‘girl’))
```

For causatives of ditransitives, the causer receives the
`causer` role, the causee the `actor` role, and the other participants receive the same annotation as in a non-causative construction. This can be seen in [\[3-2-1-1-2 (4)\]](#3-2-1-1-2 (4)) from Shipibo-Konibo
(Valenzuela 2003:612). If ‘the man’ was expressed in the clause, that participant would be annotated as `recipient`.


<span id="3-2-1-1-2 (4)" label="3-2-1-1-2 (4)">\[3-2-1-1-2 (4)\]</span> <br />
```
Ja-tian 	ja 	xontako 		jawen 	tita-n 		xoi 			meni-ma-\[a\]i 	keen-yama-\[a\]i-bi...  
that-temp 	that 	unmarried.girl:abs 	pos3 	mother-erg 	roasted.meat/fish:abs 	give-caus-inc 	want-neg-sds-em  
‘Then her mother makes the unmarried girl give roasted meat/fish (to the
man who had asked her in matrimony) even though she doesn’t want to...’

(m / meni-ma ‘make give’ 
	:causer (t / tita ‘mother’) 
	:actor (x1 / xontako ‘unmarried girl’) 
	:theme (x2 / xoi ‘roasted meat’)) 

```

There are two types of causatives of intransitives, based on the two types of intransitives. For intransitives whose single participant corresponds to an `undergoer` role, such as
change-of-state verbs in many languages, the causer is annotated as `actor` and the single participant retains
its `undergoer`label. This can be seen in
[\[3-2-1-1-2 (5)\]](#3-2-1-1-2 (5)) from Falam Chin (King 2011:195) below.


<span id="3-2-1-1-2 (5)" label="3-2-1-1-2 (5)">\[3-2-1-1-2 (5)\]</span>

<span id="3-2-1-1-2 (5a)" label="3-2-1-1-2 (5a)">\[3-2-1-1-2 (5a)\]</span> <br /> 
```
Ka 	kedam 	hri 	a 	cat.  
1sg 	shoe 	string 3sg.nom 	broken.1  
‘My shoelace is broken/broke.’

(c / cat ‘broken’ 
	:undergoer (k / kedam hri ‘shoelace’)) 
```

<span id="3-2-1-1-2 (5b)" label="3-2-1-1-2 (5b)">\[3-2-1-1-2 (5b)\]</span> <br /> 
```
Thangte in 	ka 	kedam 	hri 	a 	cat-ter.  
Thangte erg 	1sg 	shoe 	string 	3sg.nom broken.1-caus  
‘Thangte broke my shoelace.’

(c / cat-ter ‘break’  
	:actor (t / Thangte)
	:undergoer (k / kedam hri ‘shoelace’))
```

Regardless of whether the causative or anticausative verb is derived (or, neither is derived), the anticausative/intransitive meaning is annotated with a single `undergoer` participant and the causative/transitive meaning is annotated with an
`actor` and an `undergoer` participant.

When the single participant of the intransitive corresponds to the
`actor` role, then the causer receives the `causer` annotation and the single participant retains its `actor` label. This
can be seen in [\[3-2-1-1-2 (6)\]](#3-2-1-1-2 (6)) from Falam Chin (King 2011:195) below.

<span id="3-2-1-1-2 (6)" label="3-2-1-1-2 (6)">\[3-2-1-1-2 (6)\]</span>

<span id="3-2-1-1-2 (6a)" label="3-2-1-1-2 (6a)">\[3-2-1-1-2 (6a)\]</span> <br />
```
Cinte a 	hni.  
Cinte 3sg.nom 	laugh.1  
‘Cinte laughed.’ 

(h / hni ‘laugh’
	:actor (C / Cinte)) 
```

<span id="3-2-1-1-2 (6a)" label="3-2-1-1-2 (6a)">\[3-2-1-1-2 (6a)\]</span> <br /> 
```
Parte 	in 	Cinte a 	hni-ter.  
Parte 	erg 	Cinte 3sg.nom 	laugh.1-caus  
‘Parte made Cinte laugh.’

(h / hni-ter ‘make laugh’ 
	:causer (P / Parte) 
	:actor (C / Cinte))  
```

**Applicatives.**  Peterson (2007) distinguishes between “valency-increasing” applicatives and “valency-rearranging” applicatives. In valency-rearranging applicatives, a participant is expressed as an oblique in the basic construction and expressed as a core argument in the applicative construction; they are generally associated with the increased saliency or topicality of the oblique participant. Therefore, these fit into the category of pragmatic valency alternations, and both the basic and applicative construction receive the same participant role
annotation. This can be seen in
[\[3-2-1-1-2 (7)\]](#3-2-1-1-2 (7)) from Falam Chin (King 2011:240).

<span id="3-2-1-1-2 (7)" label="3-2-1-1-2 (7)">\[3-2-1-1-2 (7)\]</span>

<span id="3-2-1-1-2 (7a)" label="3-2-1-1-2 (7a)">\[3-2-1-1-2 (7a)\]</span>
```
Parte in 	Thangte hrang=ah 	hmeh 	a 	suang.  
Parte erg 	Thangte for=loc 	curry 	3sg.nom cook.1  
‘Parte cooked some curry for Thangte.’

(s / suang ‘cook’
	:actor (P / Parte)
	:undergoer (h / hmeh ‘curry’) 
	:affectee (T / Thangte))
```

<span id="3-2-1-1-2 (7b)" label="3-2-1-1-2 (7b)">\[3-2-1-1-2 (7b)\]</span>
```
Parte in 	Thangte hmeh 	a 	suan-sak  
Parte erg 	Thangte curry 	3sg.nom cook.2-ben  
‘Parte cooked Thangte some curry.’

(s / suang-sak ‘cook for’
	:actor (P / Parte)
	:undergoer (h / hmeh ‘curry’) 
	:affectee (T / Thangte)) 
```

Whether the beneficiary, *Thangte*, is expressed as an oblique or a core argument, it is annotated as `affectee`. Valency-increasing applicatives involve the addition of a participant, compared to the basic construction. Here, the added participant is
simply annotated with the appropriate semantic role. This can be seen in ADD EXAMPLE.

**Reflexives & Reciprocals** For reflexive and reciprocal constructions, the single participant is annotated with both of the semantic role labels which it is fulfilling in the construction. This can be in [\[3-2-1-1-2 (8a)\]](#3-2-1-1-2 (8a)) and [\[3-2-1-1-2 (8b)\]](#3-2-1-1-2 (8b)) from Supyire (Carlson 1994:416-7).

<span id="3-2-1-1-2 (8)" label="3-2-1-1-2 (8)">\[3-2-1-1-2 (8)\]</span>

<span id="3-2-1-1-2 (8a)" label="3-2-1-1-2 (8a)">\[3-2-1-1-2 (8a)\]</span>
```
U 	a 	ù-yé 	bánì  
he 	perf 	he-refl wound  
‘He has wounded himself.’

(b / bánì ‘wound’ 
	:actor (u / u ‘he’) 
	:undergoer (u)) 
```

<span id="3-2-1-1-2 (8b)" label="3-2-1-1-2 (8b)">\[3-2-1-1-2 (8b)\]</span><br /> 
```
Pi 	a 	pì-yé 		kánù  
they 	perf 	they-refl 	love  
‘They loved each other.’

(k / kánù ‘love’
	:actor (p / pi ‘they’)
	:undergoer (p))
```

##### 3-2-1-2. Stage 2

The Stage 2 participant role annotation requires access to
PropBank-style frame files in the language for a large number of
predicates. At this stage, each predicate identified as event is linked
to its corresponding frame file. The participants dependent on that
event are annotated with the lexicalized roles, as determined by the
frame file. This can be seen in [\[3-2-1-2 (1)\]](#3-2-1-2 (1)) below.  

```
predicate: tease.02
	roles:
	ARG0: teaser
	ARG1: teased 
	ARG2: about what
```

<span id="3-2-1-2 (1)" label="3-2-1-2 (1)">\[3-2-1-2 (1)\]</span>

```
He teased the boy about his hat.

(h / tease.02
	:ARG0 (h / he)
	:ARG1 (b / boy)
	:ARG2 (h / hat))
```

Since the nonverbal clause functions require the use of lexicalized predicates at Stage 1, these are annotated in the same way at Stage 2 (see 3-2-1-1-1). Unlike Stage 1, implicit participants are
annotated for their semantic role at Stage 2. This is shown in
[\[3-2-1-2 (2)\]](#3-2-1-2 (2)).

<span id="3-2-1-2 (2)" label="3-2-1-2 (2)">\[3-2-1-2 (2)\]</span> 
```
She parked the truck in the driveway. They loaded the boxes.

(h / park.01
	:ARG0 (s / she)
	:ARG1 (t / truck)
	:ARG2 (d / driveway)) 

(h / load.01
	:ARG0 (t2 / they)
	:ARG1 (t)  
	:ARG2 (b / boxes))
```

The second sentence in [\[3-2-1-2 (2)\]](#3-2-1-2 (2)) does not
include explicit mention of the truck, but it is understood from the
context that the truck is the goal participant of the loading event.
Therefore, at Stage 2, these implicit roles receive participant role
annotation.

###### 3-2-1-2-1.Valency alternations

The approach to valency alternations at Stage 2 is largely the same as
that detailed for Stage 1 in 3-2-1-1-2. However, at Stage 2,
predicates with valency-changing morphology should have their own frame
files with lexicalized arguments. Therefore, the annotation of
participant roles for valency alternations is the same as that for other
types of predicates. The predicate is matched with its frame files and
the participants are annotated accordingly.

##### 3-2-1-3. Inverse participant roles

AMR, the predecessor of UMR, makes use of ``inverse`` participant roles for a number of different purposes, such as the annotation of events that function as modifiers of referring expressions (typically relative clauses or participles, see section 3-1-1), the annotation of embedded interrogatives, and the annotation of participant nominalizations. These three uses of inverse participant roles are illustrated in [\[3-2-1-3 (1)\]](#3-2-1-3 (1)). The use of, for example, the :ARG1-of relation in [\[3-2-1-3 (1a)\]](#3-2-1-3 (1a)), which is the inverse of the numbered argument role :ARG1, allows us to maintain a single-rooted graph structure by embedding the ``seeing``-event underneath the participant it modifies (``sweater``). Such event concept nodes which are linked to other concepts by means of inverse participant roles can then further take their own full argument structure annotation and attribute values for e.g. aspect. Such inverses of numbered argument roles also allow us to make use of PropBank framefiles as much as possible: by annotating ``runner`` in [\[3-2-1-3 (1c)\]](#3-2-1-3 (1c)) as (p / person :ARG0-of r / run.02), we can directly link this annotation to the existing lexicon rather than having to enter an ad-hoc object concept node (r / runner) or something similar.

<span id="3-2-1-3 (1)" label="3-2-1-3 (1)">\[3-2-1-3 (1)\]</span>

<span id="3-2-1-3 (1a)" label="3-2-1-3 (1a)">\[3-2-1-3 (1a)\]</span> 
I bought the sweater that you saw.
```
(b / buy.01
	:ARG0 (i / I)
	:ARG1 (s / sweater
		:ARG1-of (s2 / see.01
			:ARG0 (y/ you)
			:Aspect State))
	:Aspect Performance)
```

<span id="3-2-1-3 (1b)" label="3-2-1-3 (1b)">\[3-2-1-3 (1b)\]</span> 
I didn't see whether he bought the sweater.
```
(s / see.01
	:ARG0 (i / I)
	:ARG1 (t / truth-value
		:polarity-of (b/ buy.01
			:ARG0 (h/ he)
			:ARG1 (s/ sweater)
			:Aspect Performance))
	:Aspect State
	:Polarity -)
```

<span id="3-2-1-3 (1c)" label="3-2-1-3 (1c)">\[3-2-1-3 (1c)\]</span> 
The runner was wearing a sweater.
```
(w / wear.01
	:ARG0 (p / person
		:ARG0-of (r / run.02))
	:ARG1 (s / sweater)
	:Aspect State)
```

UMR expands upon this AMR system of inverse relations by adding inverses for the general (i.e. non-predicate-specific) participant roles to be used at stage 1 of the road map. So, in addition to having inverses of numbered participant roles, there are now also :Actor-of and :Undergoer-of roles, and analogues for each of the general participant roles described in table 5 in section 3-2-1-1. Example [\[3-2-1-3 (1a)\]](#3-2-1-3 (2)) below illustrates the use of the inverse :Stimulus-of role to annotate the same relative clause as in [\[3-2-1-3 (1a)\]](#3-2-1-3 (1a)) above.

<span id="3-2-1-3 (2)" label="3-2-1-3 (2)">\[3-2-1-3 (2)\]</span> 
I bought the sweater that you saw.
```
(b / buy.01
	:Actor (i / I)
	:Theme (s / sweater)
		:Stimulus-of (s2 / see.01
			:Experiencer (y/ you)
			:Aspect State)
	:Aspect Performance)
```

One more context in which inverse participant roles are used is in the annotation of certain relations that are mostly thought of (and mostly expressed in languages) as nominal modification - specifically, kinship relations and certain other relational nouns, e.g. those designating functions within organizations. For the annotation of noun phrases like ``my father``, or ``the President of the University of New Mexico``, UMR uses a (p / person) concept node as the top of the graph, connected with an inverse participant role to a non-verbal clause predicate (which can then take further argument roles to express other elements in the NP). The most general, coarse-grained non-verbal clause predicate to be used in such annotations is have-role-91, although more specific predicates for frequently encountered concrete relation types are also available (FLESH OUT AND CREATE ROLESETS FOR PREDICATES). The use of these predicates in such annotations is illustrated in [\[3-2-1-3 (3)\]](#3-2-1-3 (3)).
  
<span id="3-2-1-3 (3)" label="3-2-1-3 (3)">\[3-2-1-3 (3)\]</span> 

<span id="3-2-1-3 (3a)" label="3-2-1-3 (3a)">\[3-2-1-3 (3a)\]</span> 
I met my father.
```
(m / meet.03
	:Arg0 (i / I)
	:Arg1 (p / person
		:ARG0-of (k / kinship-91
			:ARG1 i
			:ARG2 (f / father)))
	:Aspect Performance)
```

<span id="3-2-1-3 (3a)" label="3-2-1-3 (3a)">\[3-2-1-3 (3a)\]</span> 
I met the President of the University of New Mexico.
```
(m / meet.03
	:Arg0 (i / I)
	:Arg1 (p / person
		:ARG0-of (h / have-org-role-91
			:ARG1 (a / academic_org
				:name (n / name
					:op1 "University
					:op2 "of"
					:op3 "New"
					:op4 "Mexico"
					:wiki "University_of_New_Mexico"))
			:ARG2 (p / president)))
	:Aspect Performance)
```

  #### Part 3-2-2. Non-participant role UMR relations
  
Apart from predicate-specific and general participant roles, UMR also has a set of relations that are mainly used to mark NP-internal relations, to mark some types of modifiers of predicates, and to make the meanings of certain natural language expressions computationally tractable. Most of those relations are inherited from AMR, but for some of them, there are some changes in their use.

Some relations are used to describe entities in a standard, canonical form. This is the case, for example, for temporal relations such as :calendar, :century, :day, :dayperiod, :decade, :era, :month, :quarter, :season, :timezone, :weekday, :year, and :year2. The use of these relations is exemplified in [\[3-2-2 (1)\]](#3-2-2 (1)).

<span id="3-2-2 (1)" label="3-2-2 (1)">\[3-2-2 (1)\]</span> 

<span id="3-2-2 (1a)" label="3-2-2 (1a)">\[3-2-2 (1a)\]</span> 
March 23rd, 2021
```
(d / date-entity
	:year 2021
	:month 3
	:day 23)
```

<span id="3-2-2 (1b)" label="3-2-2 (1b)">\[3-2-2 (1b)\]</span> 
Friday the 13th
```
(d / date-entity
	:weekday (f / Friday)
	:day 13)
```

<span id="3-2-2 (1c)" label="3-2-2 (1c)">\[3-2-2 (1c)\]</span> 
3.30 pm Albuquerque time
```
(d / date-entity
	:time 15:30
	:timezone (z / MST))
```

Other relations mostly function to modify object concepts - they are often expressed in languages as modifiers within an NP of some sort. Semantically, modification relations in referring expressions come in two kinds: anchoring and typefying (Croft in prep.). Anchoring modifiers "situate the intended referent of the referring expression via reference to another object", in other words, they provide referential grounding for a referent expression. Many anchoring modification relations are construed in languages as possessive relations: ownership (which situates a referent via reference to its owner), part-whole relations (which situate a referent via reference to a larger entity it is a part of), and kinship relations (which situate a referent via reference to another person that has a particular kind of relation to it). As described in section 3-2-1-3, kinship relations are annotated through the ``kinship-91``, predicate, even when they are not predicated. For ownership and part-whole relations, UMR uses :poss and :part-of relations with the possessum or part as the parent and the possessor or whole as the daughter, as in [\[3-2-2 (2)\]](#3-2-2 (2)).

<span id="3-2-2 (2)" label="3-2-2 (2)">\[3-2-2 (2)\]</span> 

<span id="3-2-2 (2a)" label="3-2-2 (2a)">\[3-2-2 (2a)\]</span> 
John's car
```
(c / car
	:poss (p / person
		:name (n / name
			:op1 "John")))
```

<span id="3-2-2 (2b)" label="3-2-2 (2b)">\[3-2-2 (2b)\]</span> 
Guitar strings
```
(s / string
	:part-of (g / guitar)
	:ref Plural)
```

Typifying modifiers, on the other hand, "enrich the referent description by subcategorizing it or selecting the quantity (cardinality, amount, proportion, piece) of the
category or type denoted by the head noun." For such modifiers, a high-level, coarse-grained relation :mod is available. For example, in [\[3-2-2 (3a)\]](#3-2-2 (3a)), the modifier ``women`` does not narrow down the reference of ``magazine`` to a specific identifiable instance, but rather to a subclass of magazines. It is therefore annotated with the :mod relation, as opposed to a phrase like "that woman's magazine", where ``woman`` would be annotated with the :poss relation. A number of more fine-grained subtypes of the :mod relation are also available - :age, for indicating the age of referents as in [\[3-2-2 (3b)\]](#3-2-2 (3b)); :consist-of, for indicating the membership of groups [\[3-2-2 (3c)\]](#3-2-2 (3c)); and :topic, for indicating what a referent is about as in [\[3-2-2 (3d)\]](#3-2-2 (3d)).

<span id="3-2-2 (3)" label="3-2-2 (3)">\[3-2-2 (3)\]</span> 

<span id="3-2-2 (3a)" label="3-2-2 (3a)">\[3-2-2 (3a)\]</span> 
John's car
```
(c / car
	:poss (p / person
		:name (n / name
			:op1 "John")))
```

<span id="3-2-2 (3b)" label="3-2-2 (3b)">\[3-2-2 (3b)\]</span> 
The thirty year-old man
```
(m / man
	:age (t / temporal-quantity
		:quant 30
		:unit (y / year)))
```

<span id="3-2-2 (3c)" label="3-2-2 (3c)">\[3-2-2 (3c)\]</span> 
A swarm of bees
```
(s / swarm
	:consist-of (b / bee
		:ref Plural))
```

<span id="3-2-2 (3d)" label="3-2-2 (3d)">\[3-2-2 (3d)\]</span> 
Information about the case
```
(i / information
	:topic (c / case))
```

A number of relations serve to modify events rather than objects - they are used to annotate circumstantial locative and temporal information rather than participants. The :direction and :path relations are used to annotate cardinal directions and extended spatial paths, respectively, as in [\[3-2-2 (4a)\]](#3-2-2 (4a)) and [\[3-2-2 (4b)\]](#3-2-2 (4b)). The :duration and :frequency relations, illustrated in [\[3-2-2 (4c)\]](#3-2-2 (4c)) - [\[3-2-2 (4e)\]](#3-2-2 (4e)) are optionally used to annotate aspectual information that may be overtly present but that cannot be captured in the :Aspect attribute - as clarified in section 3-3-1, the latter abstracts away from duration and frequency information.

<span id="3-2-2 (4)" label="3-2-2 (4)">\[3-2-2 (4)\]</span> 

<span id="3-2-2 (4a)" label="3-2-2 (4a)">\[3-2-2 (4a)\]</span> 
He drove west.
```
(d / drive.01
	:ARG0 (h / he)
	:direction (w / west))
```

<span id="3-2-2 (4b)" label="3-2-2 (4b)">\[3-2-2 (4b)\]</span> 
He drove through the tunnel.
```
(d / drive.01
	:ARG0 (h / he)
	:path (t / tunnel))
```

<span id="3-2-2 (4c)" label="3-2-2 (4c)">\[3-2-2 (4c)\]</span> 
I visited New York City for a week.
```
(v / visit.01
	:ARG0 (i / I)
	:ARG1 (c / city
		:name (n / name
			:op1 "New"
			:op2 "York"
			:op3 "City"
			:wiki "New_York_City"))
	:duration (t / temporal-quantity
		:quant 1
		:unit (w / week))
	:Aspect Endeavor)
```

<span id="3-2-2 (4d)" label="3-2-2 (4d)">\[3-2-2 (4d)\]</span> 
I visited New York City twice.
```
(v / visit.01
	:ARG0 (i / I)
	:ARG1 (c / city
		:name (n / name
			:op1 "New"
			:op2 "York"
			:op3 "City"
			:wiki "New_York_City"))
	:frequency 2
	:Aspect Performance)
```

<span id="3-2-2 (4e)" label="3-2-2 (4e)">\[3-2-2 (4e)\]</span> 
I visit New York City every December.
```
(v / visit.01
	:ARG0 (i / I)
	:ARG1 (c / city
		:name (n / name
			:op1 "New"
			:op2 "York"
			:op3 "City"
			:wiki "New_York_City"))
	:frequency (r / rate-entity-91
		:ARG4 (d / date-entity
			:month 12))
	:Aspect Habitual)
```

The relations :name, :wiki, and :op are mostly used in the treatment of named entities. Whenever an entity is explicitly mentioned by name in the text to be annotated, it receives a :name relation, whose daughter is an (n / name) node. This node then has as many numbered :opX relations as the number of words this name consists of, each of which taking one of these words as their daughter. In [\[3-2-2 (4e)\]](#3-2-2 (4e)) above, for example, the (n / name) concept corresponding to "New York City" takes an :op1, :op1, and :op3 relation, one for each orthographic word. Named entities can also take a :wiki relation, whose daughter is the title of the Wikipedia page corresponding to the entity in question. Numbered :op relations are also used in coordination, as in [\[3-2-2 (5)\]](#3-2-2 (5)).

<span id="3-2-2 (5)" label="3-2-2 (5)">\[3-2-2 (5)\]</span> 

I saw a spider and a snake.
```
(s / see.01
	:ARG0 (i / I)
	:ARG1 (a / and
		:op1 (s2 / spider)
		:op2 (s3 / snake))
	:Aspect State)
```

The :ord, :quant, :range, :scale, :unit, and :value examples are used to annotate semantics of quantification, as illustrated in [\[3-2-2 (6)\]](#3-2-2 (6)). The :ord role is used to express ordinals. It always takes an (o / ordinal-entity) concept as its daughter, which in turn takes a :value relation to express the ordinal position, as in [\[3-2-2 (6a)\]](#3-2-2 (6a)). It may furthermore take a :range relation to indicate a specific time period in which the relevant ordinal position holds, as in [\[3-2-2 (6b)\]](#3-2-2 (6b)). The :value relation is, apart from ordinals, used for annotating percentages, phone numbers, e-mail addresses, and urls, as illustrated in [\[3-2-2 (6c)\]](#3-2-2 (6c)) adn [\[3-2-2 (6d)\]](#3-2-2 (6d)). The :quant relation is used for annotating both exact and approximate cardinalities of sets of countable objects as in [\[3-2-2 (6e)\]](#3-2-2 (6e)) and [\[3-2-2 (6f)\]](#3-2-2 (6f)), as well as for the number of "units" of non-countable substances, as in [\[3-2-2 (6g)\]](#3-2-2 (6g)). This latter use includes temporal durations and spatial distances, as in [\[3-2-2 (4c)\]](#3-2-2 (4c)) above. The :unit relation is used for both standardized, well-established units such as dollars in [\[3-3-2 (1a)\]](#3-3-2 (1a)) below or weeks in [\[3-2-2 (4c)\]](#3-2-2 (4c)) above, and for ad-hoc mensural constructions, such as cups in [\[3-2-2 (6g)\]](#3-2-2 (6g)). Lastly, the :scale relation is used for quantities where a :quant 0 value does not actually represent a 0-quantity, such as on the Richter or Decibel scale, as in [\[3-2-2 (6h)\]](#3-2-2 (6h))

<span id="3-2-2 (6)" label="3-2-2 (6)">\[3-2-2 (6)\]</span> 

<span id="3-2-2 (6a)" label="3-2-2 (6a)">\[3-2-2 (6a)\]</span> 
I visited New York for the third time.
```
(v / visit.01
	:ARG0 (i / I)
	:ARG1 (c / city
		:name (n / name
			:op1 "New"
			:op2 "York"
			:op3 "City"
			:wiki "New_York_City"))
	:ord (o / ordinal-entity
		:value 3)
	:Aspect Performance)
```

<span id="3-2-2 (6b)" label="3-2-2 (6b)">\[3-2-2 (6b)\]</span> 
I visited New York for the third time in six months.
```
(v / visit.01
	:ARG0 (i / I)
	:ARG1 (c / city
		:name (n / name
			:op1 "New"
			:op2 "York"
			:op3 "City"
			:wiki "New_York_City"))
	:ord (o / ordinal-entity
		:value 3
		:range (t / temporal-quantity
			:quant 6
			:unit (m / month)))
	:Aspect Performance)
```

<span id="3-2-2 (6c)" label="3-2-2 (6c)">\[3-2-2 (6c)\]</span> 
30 percent
```
(p / percentage-entity
	:value 30)
```

<span id="3-2-2 (6d)" label="3-2-2 (6d)">\[3-2-2 (6d)\]</span> 
http://umr-tool.cs.brandeis.edu/display_post
```
(u / url-entity
	:value "http://umr-tool.cs.brandeis.edu/display_post")
```

<span id="3-2-2 (6e)" label="3-2-2 (6e)">\[3-2-2 (6e)\]</span> 
Three houses
```
(h / house
	:quant 3)
```

<span id="3-2-2 (6f)" label="3-2-2 (6f)">\[3-2-2 (6f)\]</span> 
More than three houses
```
(h / house
	:quant (m / more-than
		:op1 3))
```

<span id="3-2-2 (6g)" label="3-2-2 (6g)">\[3-2-2 (6g)\]</span> 
Three cups of milk
```
(m / milk
	:quant 3
	:unit (c / cup))
```

<span id="3-2-2 (6h)" label="3-2-2 (6h)">\[3-2-2 (6h)\]</span> 
6.5 on the Richter scale
```
(s / seismic-quantity
	:quant 6.5
	:scale (r / richter))
```

The :example relation, illustrated in [\[3-2-2 (7a)\]](#3-2-2 (7a)) is used to annotate illustrative examples of object categories. The :polite relation is used to indicate that an utterance (often a command) is marked for deference with respect to the interlocutor, as in [\[3-2-2 (7b)\]](#3-2-2 (7b)). 

<span id="3-2-2 (7)" label="3-2-2 (7)">\[3-2-2 (7)\]</span> 

<span id="3-2-2 (7a)" label="3-2-2 (7a)">\[3-2-2 (7a)\]</span> 
Countries like Germany and France
```
(c / country
	:example (a/ and
		:op1 (c / country
			:name (n / name
				:op1 "Germany"
				:wiki "Germany"))
		:op2 (c / country
			:name (n / name
				:op1 "France"
				:wiki "France"))))
```

<span id="3-2-2 (7b)" label="3-2-2 (7b)">\[3-2-2 (7b)\]</span> 
Could you close the window?
```
(c / close.01
	:ARG0 (y / you)
	:ARG1 (w / window)
	:Aspect Performance
	:Mode Imperative
	:polite +)
```

The :condition and :concession relations are alternative ways of annotating the have-condition-91 and have-concession-91 predicates - their use is detailed in section 4.3.

Lastly, annotators have at their disposal an :other relation. If they encounter any concept that they believe needs to be included in the UMR annotation, but UMR does currently not have a defined procedure of annotating it, they may simply add it to the graph using this :other relation, linking it to the concept node that seems appropriate.

### Part 3-3. UMR attributes
  
#### Part 3-3-1. Aspect

The aspect annotation consists of a single value that is annotated for
every event identified in [3.1.1](##part-3-1-1-eventive-concepts). The aspect annotation doesn’t
have distinct annotation stages, unlike modality and participant roles.
Instead it relies on a typological lattice which ranges from very
coarse-grained to very fine-grained aspectual values. It’s expected that
languages at an earlier stage of semantic analysis or annotation will
tend to use more coarse-grained values, and languages at later stages of
annotation will tend to use more fine-grained values.

This is also heavily dependent on the aspectual distinctions that are
grammaticalized and/or obligatory in the language. For example, although
English has a long history of semantic analysis and many computational
resources, it has very little overt aspectual marking in its grammar and
therefore the most fine-grained aspect distinctions are very difficult
to judge in annotation. This aspect lattice is shown below. 

![Aspect lattice](aspect-lattice.png)

Below are the aspect values with a brief definition.

```habitual```: occurs/occurred usually or habitually  
```imperfective```: ambiguous between state and process  
```process```: unspecified type of process  
```atelic process```: process that does not reach a result state  
```perfective```: process that comes to an end  
```state```: unspecified type of state  
```reversible state```: acquired state that is not permanent  
```irreversible state```: acquired state that is permanent  
```inherent state```: state that is notacquired and permanent  
```point state```: state that is acquired and reversed at a single point in time  
```activity```: process that does not end  
```undirected activity```: process that does not end and does not progress linearly along a scale  
```directed activity```: process that does not end and does progress linearly along a scale  
```endeavor```: process that ends without reaching a result state  
```semelfactive```: process that ends without reaching a result state and happens at a single point in time  
```undirected endeavor```: process that ends without reaching a result state and does not progress linearly along a scale  
```directed endeavor```: process that ends without reaching a result state and progresses linearly along a scale  
```performance```: process that ends and  reaches a result state  
```incremental accomplishment```: process that ends and reaches a result state, and progresses linearly along a scale  
```nonincremental accomplishment```: process that ends and reaches a result state, and does not progress linearly along a scale  
```directed achievement```: process that ends and reaches a result state within a single point in time, and progresses linearly along a scale  
```reversible directed achievement```: process that ends and reaches a result state, which is not permanent, within a single point in time, and progresses linearly along a scale  
```irreversible directed achievement```: process that ends and reaches a result state, which is permanent, within a single point in time, and progresses linearly along a scale  

In order to select the appropriate annotation value for each event,
annotators proceed through a series of decisions.

##### Part 3-3-1-1. Event Nominals

The first decision concerns the morphosyntactic expression of the event. Events expressed as nominals often lack any grammatical clues as to their aspectual structure. This makes determining an aspectual
annotation value difficult. We do, however, know that these events are
processes, and not states, since nominals expressing states are not
identified as events. On the lattice,
```process``` is the aspectual value that includes all types of processes. Therefore, events expressed as event
nominals, as in [\[3-3-1-1 (1)\]](#3-3-1-1 (1)), are annotated as
```process```.


<span id="3-3-1-1 (1)" label="3-3-1-1 (1)">\[3-3-1 (1)\]</span>

<span id="3-3-1-1 (1a)" label="3-3-1-1 (1a)">\[3-3-1-1 (1a)\]</span> He presented his
research at **the meeting** yesterday.
```
(m / meeting  
	Aspect: process)  
```

<span id="3-3-1-1 (1b)" label="3-3-1-1 (1b)">\[3-3-1-1 (1b)\]</span> After **the game**, she
went home.  
```
(g / game  
	Aspect: process)  
```
<span id="3-3-1-1 (1c)" label="3-3-1-1 (1c)">\[3-3-1-1 (1c)\]</span> He had **the operation** on Tuesday.  

```
(o / operation  
	Aspect: process)  
```

Any event packaged in a referring expression is considered an event
nominal and annotated with <span class="smallcaps">procecss</span>. This
includes underived nominals, nominalizations, and gerunds, as in
[\[3-3-1-1 (2)\]](#3-3-1-1 (2)).

<span id="3-3-1-1 (2)" label="3-3-1-1 (2)">\[3-3-1-1 (2)\]</span>

<span id="3-3-1-1 (2a)" label="3-3-1-1 (2a)">\[3-3-1-1 (2a)\]</span> **The second training** was cancelled yesterday.  
```
(t / training  
	Aspect: process)  
```

<span id="3-3-1-1 (2b)" label="3-3-1-1 (2b)">\[3-3-1-1 (2b)\]</span> The dog
interrupted the meeting with **his barking**.  
```
(b / barking  
	Aspect: process)  
```

Note that *-ing* forms in English can occur in a variety of
constructions; they should only be treated as event nominals when they
are used in referring expressions (as in [\[3-3-1-1 (2a)\]](#3-3-1-1 (2a)) and
[\[3-3-1-1 (2b)\]](#3-3-1-1 (2b)) above). When they occur in other types of
constructions, as in [\[3-3-1-1 (3)\]](#3-3-1-1 (3)), they should not
receive an aspect annotation at this point and annotators should
continue on to the next step.

<span id="3-3-1-1 (3)" label="3-3-1-1 (3)">\[3-3-1-1 (3)\]</span> The
dog stopped **barking** for a few seconds.

Event nominals that occur in predicate nominal constructions, as in
[\[3-3-1-1 (4)\]](#3-3-1-1 (4)), are also not annotated at this point;
these are treated like other predicate nominal constructions.

<span id="3-3-1-1 (4)" label="3-3-1-1 (4)">\[3-3-1-1 (4)\]</span>

It was **an earthquake**.

##### Part 3-3-1-2. Habitual

The next step concerns the application of the
```habitual``` aspect value. This value should
be applied to all events that are presented as occurring usually or
habitually, as in [\[3-3-1-2 (1)\]](#3-3-1-2 (1)).


<span id="3-3-1-2 (1)" label="3-3-1-2 (1)">\[3-3-1-2 (1)\]</span>

<span id="3-3-1-2 (1a)" label="3-3-1-2 (1a)">\[3-3-1-2 (1a)\]</span> He **bakes** pies.
```
(b / bake  
	Aspect: habitual) 
```
<span id="3-3-1-2 (1b)" label="3-3-1-2 (1b)">\[3-3-1-2 (1b)\]</span> She **rides** her bike to work. 
```
(r / ride  
	Aspect: habitual)  
```
<span id="3-3-1-2 (1c)" label="3-3-1-2 (1c)">\[3-3-1-2 (1c)\]</span> They
**vacation** in Taos every winter.  
```
(v / vacation  
	Aspect: habitual)  
```
<span id="3-3-1-2 (1d)" label="3-3-1-2 (1d)">\[3-3-1-2 (1d)\]</span> They
**used to vacation** in Taos every winter.  
```
(v / vacation  
	Aspect: habitual)  
```

In English, present habitual events are signalled by the Simple Present
construction; past tense habitual events are expressed with the *used
to* construction. Note that the ```habitual```
annotation is not used for ability modals (e.g., *he can bake apple
pie*); these events should continue on to the next step.

##### Part 3-3-1-3. State

The next step assesses whether the event is a
```state```. The distinction between states and
processes is necessary for event identification (as states are only
identified as events when predicated). According to Vendler (1967), states are those events which are stative—that is, no change takes place over the course of the event. There are various ways to express states in predication, shown in [\[3-3-1-3 (1)\]](#3-3-1-3 (1)); note that all of the nonverbal clause types identified in [3.1.1](##part-3-1-1-eventive-concepts) and annotated with UMR predicates are annotated as ```state```.


<span id="3-3-1-3 (1)" label="3-3-1-3 (1)">\[3-3-1-3 (1)\]</span>

<span id="3-3-1-3 (1a)" label="3-3-1-3 (1a)">\[3-3-1-3 (1a)\]</span> My cat **loves** tuna. 
```
(l / love  
	Aspect: state)  
```
<span id="3-3-1-3 (1b)" label="3-3-1-3 (1b)">\[3-3-1-3 (1b)\]</span> The doctor **is tall**.  
```
(h / have-mod-91  
	Aspect: state) 
```
<span id="3-3-1-3 (1c)" label="3-3-1-3 (1c)">\[3-3-1-3 (1c)\]</span> The book **is on the table**.  
```
(h / have-location-91  
	Aspect: state)  
```
<span id="3-3-1-3 (1d)" label="3-3-1-3 (1d)">\[3-3-1-3 (1d)\]</span> She **is an architect**.  
```
(h / have-role-91  
	Aspect: state) 
```
<span id="3-3-1-3 (1e)" label="3-3-1-3 (1e)">\[3-3-1-3 (1e)\]</span> Your glass **is in
the kitchen**.  
```
(h / have-location-91  
	Aspect: state) 
```

Modal verbs, as in [\[3-3-1-3 (2)\]](#3-3-1-3 (2)), and events under the scope of
ability modals, as in [\[3-3-1-3 (3)\]](#3-3-1-3 (3)), are also annotated as
```state```.

<span id="3-3-1-3 (2)" label="3-3-1-3 (2)">\[3-3-1-3 (2)\]</span>

<span id="3-3-1-3 (2a)" label="3-3-1-3 (2a)">\[3-3-1-3 (2a)\]</span> He **wants** to travel to Albuquerque.  
```
(w / want  
	Aspect: state)  
```
<span id="3-3-1-3 (2b)" label="3-3-1-3 (2b)">\[3-3-1-3 (2b)\]</span> The cat **needs** to be fed. 
```
(n / need  
	Aspect: state)  
```
<span id="3-3-1-3 (2c)" label="3-3-1-3 (2c)">\[3-3-1-3 (2c)\]</span> He’s **dreading** their decision.  
```
(d / dread  
	Aspect: state)  
```
<span id="3-3-1-3 (3)" label="3-3-1-3 (3)">\[3-3-1-3 (3)\]</span>

<span id="3-3-1-3 (3a)" label="3-3-1-3 (3a)">\[3-3-1-3 (3a)\]</span> She <u>is able to</u> **sing** that aria.  
```
(s / sing  
	Aspect: state) 
```
<span id="3-3-1-3 (3b)" label="3-3-1-3 (3b)">\[3-3-1-3 (3b)\]</span> This car <u>can</u> **go** up to 150 mph.  
```
(g / go  
	Aspect: state)  
```
In this analysis, ability modals refer to a static state of affairs,
i.e. an entity possesses the relevant ability. For examples like
[\[3-3-1-3 (3a)\]](#3-3-1-3 (3a)), ability modals may look more like event
quantification. That is, there are probably multiple singing events that this example is generalizing over. Examples like [\[3-3-1-3 (3b)\]](#3-3-1-3 (3b)), however, show how ability modals are more like states. It is possible
that the car has never actually gone as fast as 150 mph; the car just
has the parts and (theoretical) ability to do so. Therefore, all types
of ability modals, both [\[3-3-1-3 (3a)\]](#3-3-1-3 (3a)) and [\[3-3-1-3 (3b)\]](#3-3-3 (3b)), are
analyzed as states and annotated as such.

There is a type of event, called “inactive actions” by Croft (2012), which is semantically intermediate between states and processes. In many languages, they can be construed either way. For example, English *lie* can occur in the Progressive (*Bill **is lying** on the bed*) or the Simple Present (*The Sandias **lie** to the east of Albuquerque*). And across languages there is variation as to the default construal of
inactive actions. The most frequent inactive actions are posture verbs
(*sit, stand, lie, hang*), perception verbs (*see/look at, watch,
hear/listen to, feel*), some sensation verbs (*ache*), mental activity
verbs (*think, understand*), and verbs of operation/function (*work* in
*This washing machine **works/is working***). For the UMR annotation,
inactive actions in all constructions are annotated as
```state```. If it is unclear whether an event
refers to a ```state``` or an
```atelic process```, then the
```imperfective``` annotation value is used.

There are different types of states, shown in
[\[3-3-1-3 (4)\]](#3-3-1-3 (4)), which can optionally be distinguished in
the aspect annotation.


<span id="3-3-1-3 (4)" label="3-3-1-3 (4)">\[3-3-1-3 (4)\]</span>

<span id="3-3-1-3 (4a)" label="3-3-1-3 (4a)">\[3-3-1-3 (4a)\]</span> My cat **is black and white**.
```
(h / have-mod-91  
	Aspect: inherent state)  
```
<span id="3-3-1-3 (4b)" label="3-3-1-3 (4b)">\[3-3-1-3 (4b)\]</span> My cat **is hungry**.  
```
(h / have-mod-91  
	Aspect: reversible state)  
```
<span id="3-3-1-3 (4c)" label="3-3-1-3 (4c)">\[3-3-1-3 (4c)\]</span> The wine glass **is shattered**.  
```
(h / have-mod-91  
	Aspect: irreversible state)  
```
<span id="3-3-1-3 (4d)" label="3-3-1-3 (4d)">\[3-3-1-3 (4d)\]</span> It **is 2:30pm**. 
```
(h / have-mod-91  
	Aspect: point state)  
```

Events that are annotated as ```inherent
state```, as in [\[3-3-1-3 (4a)\]](#3-3-1-3 (4a)), refer to states that are
an inherent property of the entity, i.e. they did not ‘start’ at any
particular point in the entity’s history and are not changeable in the
future. Events annotated as ```reversible
state```, as in [\[3-3-1-3 (4b)\]](#3-3-1-3 (4b)), refer to properties of entities
that are not inherent, meaning they have come into existence at some
point during the entity’s history; these states are reversible, meaning
the entity likely will revert back to its base state in the future.
Events annotated as ```irreversible state```,
as in [\[3-3-1-3 (4c)\]](#3-3-1-3 (4c)), refer to properties of entities that are not
inherent, but cannot be reversed in the future; once acquired, these
states are permanent. Finally, events that are annotated as
```point state```, as in [\[3-3-1-3 (4d)\]](#3-3-1-3 (4d)),
refer to states that come into and out of existence over a single point
in time (what is considered a ‘point’ is open to construal); these
states necessarily do not persist into the future.

Events that are not annotated as a type of
```state``` move on to the next step.

##### Part 3-3-1-4. Activity

The ```activity``` label applies to processes
when there is no evidence that the event has come to an end, as in
[\[3-3-1-4 (1)\]](#3-3-1-4 (1)).

<span id="3-3-1-4 (1)" label="3-3-1-4(1)">\[3-3-1-4 (1)\]</span>

<span id="3-3-1-4 (1a)" label="3-3-1-4 (1a)">\[3-3-1-4 (1a)\]</span> He is still **writing** his paper.  
```
(w / write  
	Aspect: activity) 
```
<span id="3-3-1-4 (1b)" label="3-3-1-4 (1b)">\[3-3-1-4 (1b)\]</span> He was
**writing** his paper yesterday.  
```
(w / write  
	Aspect: activity) 
```

This covers cases where it is clear that the process is still ongoing at
document creation time, as in [\[3-3-1-4 (1a)\]](#3-3-1-4 (1a)), but also cases
where it is ambiguous whether or not the process continues, as in
[\[3-3-1-4 (1b)\]](#3-3-1-4 (1b)).

This step is largely dependent on context and real world knowledge,
however there are some grammatical cues that can help. Events in the
present tense, as in [\[3-3-1-4 (2)\]](#3-3-1-4 (2)), are annotated as
```activity```.

<span id="3-3-1-4 (2)" label="3-3-1-4 (2)">\[3-3-1-4 (2)\]</span> He **is playing** the violin.  
```
(p / play  
	Aspect: activity)  
```

Inceptive and continuative aspectual marking, as in [\[3-3-1-4 (3)\]](#3-3-1-4 (3)),
also do not imply that an event has (necessarily) ended.

<span id="3-3-1-4 (3)" label="3-3-1-4 (3)">\[3-3-1-4 (3)\]</span>

<span id="3-3-1-4 (3a)" label="3-3-1-4 (3a)">\[3-3-1-4 (3a)\]</span> He
<u>started</u> **playing** the violin.  
```
(p / play  
	Aspect: activity) 
```
<span id="3-3-1-4 (3b)" label="3-3-1-4 (3b)">\[3-3-1-4 (3b)\]</span> He <u>kept on</u> **playing** the violin.  
```
(p / play  
	Aspect: activity)  
```
If an annotator is unsure about whether the text indicates that an event has ended or not, the ```atelic process```
label can be used.

There are two finer-grained ```activity```
categories which can optionally be distinguished. Certain type of
activities describe directed change, as in
[\[3-3-1-4 (4)\]](#3-3-1-4 (4)), whereas other activities describe
undirected change, as in [\[3-3-1-4 (5)\]](#3-3-1-4 (5));
these are annotated as ```directed activity```
and ```undirected activity``` respectively.


<span id="3-3-1-4 (4)" label="3-3-1-4 (4)">\[3-3-1-4 (4)\]</span>
The soup was **cooling** on the counter.
```
(c / cool  
	Aspect: directed activity)  
```

<span id="3-3-1-4 (5)" label="3-3-1-4 (5)">\[3-3-1-4 (5)\]</span>
The cat was **meowing** outside the door.
```
(m / meow  
	Aspect: undirected activity)  
```

Events annotated as ```directed activity```
refer to change that occurs gradually along a qualitative scale. In
[\[3-3-1-4 (4)\]](#3-3-1-4 (4)), the temperature of the soup
continues to decrease in a linear fashion. Events annotated as
```undirected activity``` refer to change that
does not progress incrementally along a scale; in
[\[3-3-1-4 (5)\]](#3-3-1-4 (5)), there is no scale or gradual
change.

Events that have ended prior to document creation time and have not yet
received an annotation move on to the next step.

##### Part 3-3-1-5. Endeavor and Performance

At this point, only ```perfective``` events are
left: ```endeavor``` and
```performance```. Both the
```endeavor``` and
```performance``` aspectual types entail that
the process has come to an end; they are distinguished by the
boundedness of the event in terms of qualitative state. The
```performance``` value is used when the event
reaches a result state distinct from the base (start) state, that is, a specific “natural” endpoint. The ```endeavor```
value is used when the events ends, but does not reach a distinct result
state. The ```performance``` value can be seen
as the ‘default’ value for events at this step; the
```endeavor``` value is only annotated in the
presence of explicit marking, which may come in several forms detailed
below. If it’s not clear which category an event fits into, it can be
annotated as ```perfective```.

The explicit aspectual markings which suggest an
```endeavor``` annotation are terminative
aspect marking, durative adverbials, and non-result paths. These are
illustrated for English below.

<span id="3-3-1-5 (1)" label="3-3-1-5 (1)">\[3-3-1-5 (1)\]</span>

<span id="3-3-1-5 (1a)" label="3-3-1-5 (1a)">\[3-3-1-5 (1a)\]</span> Mary
<u>stopped</u> **mowing** the lawn.  
```
(m / mow  
	Aspect: endeavor)  
```
<span id="3-3-1-5 (1b)" label="3-3-1-5 (1b)">\[3-3-1-5 (1b)\]</span> Mary **mowed** the lawn <u>for thirty minutes</u>.  
```
(m / mow  
	Aspect: endeavor) 
```
<span id="3-3-1-5 (1c)" label="3-3-1-5 (1c)">\[3-3-1-5 (1c)\]</span> \*Mary
<u>finished</u> **mowing** the lawn <u>for thirty minutes</u>.  

<span id="3-3-1-5 (1d)" label="3-3-1-5 (1d)">\[3-3-1-5 (1d)\]</span> They **walked** <u>along the river</u>.  
```
(w / walk  
	Aspect: endeavor)
```
<span id="3-3-1-5 (1e)" label="3-3-1-5 (1e)">\[3-3-1-5 (1e)\]</span> They
<u>finished</u> **walking** <u>along the river</u>. 
```
(w / walk  
	Aspect: performance) 
```
<span id="3-3-1-5 (1f)" label="3-3-1-5 (1f)">\[3-3-1-5 (1f)\]</span> They
**walked** <u>along the river</u> <u>in 3 hours</u>.  
```
(w / walk  
	Aspect: performance) 
```

Terminative aspectual marking, such as *stop* in English, is the
strongest evidence that an event has ended without reaching a result
state and should therefore be annotated as
```endeavor```. Durative adverbials, such as in
[\[3-3-1-5 (1b)\]](#3-3-1-5 (1b)), are the second strongest evidence for an
```endeavor``` annotation: they indicate that
the event took place for a defined period of time and then ended, likely
without completion. At least in English, durative adverbials cannot
co-occur with completive aspectual marking; see
[\[3-3-1-5 (1c)\]](#3-3-1-5 (1c)). A non-result path is the weakest evidence
for an ```endeavor``` annotation; in the
absence of other aspectual indicators, a non-result path requires an
```endeavor``` annotation, as in
[\[3-3-1-5 (1d)\]](#3-3-1-5 (1d)). But, if there is a completive aspectual marker,
as in [\[3-3-1-5 (1e)\]](#3-3-1-5 (1e)), or a container adverbial, as in
[\[3-3-1-5 (1f)\]](#3-3-1-5 (1f)), both indicators that an event has reached
a distinct result state, then the event is annotated as
```performance```.

In the absence of any of the aspectual indicators listed above, events
that have made it to this point in the decision tree are annotated as
```performance```.

Both ```endeavor``` and
```performance``` have more fine-grained
aspectual distinctions which may optionally be annotated. Endeavors may
be specified with ```undirected endeavor```,
```directed endeavor```, and
```semelfactive```. The
```undirected endeavor``` and
```directed endeavor``` values correspond to
```undirected activity``` and
```directed activity```; they differ in that
the event has come to an end. Semelfactives refer to punctual events
that happen once before reverting back to the base state (these are
similar to ```point state```, but refer to a
process), as in [\[3-3-1-5 (2c)\]](#3-3-1-5 (2c)).

<span id="3-3-1-5 (2)" label="3-3-1-5 (2)">\[3-3-1-5 (2)\]</span>

<span id="3-3-1-5 (2a)" label="3-3-1-5 (2a)">\[3-3-1-5 (2a)\]</span> The cat
**meowed** for two hours until I woke up.
```
(m / meow  
	Aspect: undirected endeavor)  
```
<span id="3-3-1-5 (2b)" label="3-3-1-5 (2b)">\[3-3-1-5 (2b)\]</span> The soup **cooled**
for an hour before we ate it.
```
(c / cool  
	Aspect: directed endeavor) 
```

<span id="3-3-1-5 (2c)" label="3-3-1-5 (2c)">\[3-3-1-5 (2c)\]</span> The
cat **meowed** (once).
```
(m / meow  
	Aspect: semelfactive)  
```

The finer-grained annotations for
```performance``` distinguish between punctual
events (```direct achievement```) and durative
events (```incremental accomplishment```,
```nonincremental accomplishment```), with even
finer-grained categories based on the type of change.

Achievements are punctual events, meaning that are conceptualized as
occurring at a single point in time (like ```point
state``` and ```semelfactive```). Unlike
```point state``` and
```semelfactive```, achievements don’t revert
back to the base state, which is why they’re considered a finer-grained
type of ```performance```. The
```directed achievement``` annotation can be
further specified based on whether the change is reversible or
irreversible. In [\[3-3-1-5 (3a)\]](#3-3-1-5 (3a)), the change that the door
undergoes can be reversed in that the door can be closed; therefore this
is annotated as ```reversible directed
achievement```. In [\[3-3-1-5 (3b)\]](#3-3-1-5 (3b)), the change that the
window undergoes cannot be reversed; therefore this is annotated as
```irreversible directed achievement```.

Accomplishments are durative events that can be categorized based on
whether the change occurs incrementally or nonincrementally; this is
similar to the difference between directed and undirected activities and
endeavors. With ```incremental
accomplishment```, the change occurs incrementally along the
qualitative dimension; in [\[3-3-1-5 (3c)\]](#3-3-1-5 (3c)), the pancake
is eaten piece-by-piece and each subsequent bite brings the event closer
to completion. With ```nonincremental
accomplishment```, the change ends up at a distinct result state (as
with all types of Performances), but it may not get there in a
linear/incremental fashion. In [\[3-3-1-5 (3d)\]](#3-3-1-5 (3d)),
the computer does not necessarily get progressively more repaired with
each action. Harry may try one tactic unsuccessfully to fix the
computer; he may even make the problem worse at some point, but
eventually succeeds in repairing the computer.

<span id="3-3-1-5 (3)" label="3-3-1-5 (3)">\[3-3-1-5 (2)\]</span>

<span id="3-3-1-5 (3a)" label="3-3-1-5 (3a)">\[3-3-1-5 (3a)\]</span> The door **opened**.
```
(o / open  
	Aspect: reversible directed achievement)
```
<span id="3-3-1-5 (3b)" label="3-3-1-5 (3b)">\[3-3-1-5 (3b)\]</span> The window
**shattered**.
```
(s / shatter  
	Aspect: irreversible directed achievement)  
```
<span id="3-3-1-5 (3c)" label="3-3-1-5 (3c)">\[3-3-1-5 (3c)\]</span> I
**ate** an apple pancake.
```
(a / ate  
	Aspect: incremental accomplishment)
```
<span id="3-3-1-5 (3d)" label="3-3-1-5 (3d)">\[3-3-1-5 (3d)\]</span>
Harry **repaired** the computer.
```
(r / repair  
	Aspect: nonincremental accomplishment) 
```
  
#### Part 3-3-2. Mode

UMR adopts the mode attribute for AMR. The four values for the **mode** attribute include
*expressive*, *imperative*, and *interrogative* as in [\[3-3-2 (1)\]](#3-3-2 (1)). 

<span id="3-3-2 (1)" label="3-3-2 (1)">3-3-2 (1)</span>

<span id="3-3-2 (1a)" label="3-3-2 (1a)">3-3-2 (1a)</span>
```
Yup , a couple of hundred dollars is going to save the day !
(s / save-02 
      :mode expressive
      :ARG0 (c / couple
            :op1 (m / monetary-quantity :quant 100
                  :unit (d2 / dollar)))
      :ARG1 (d / day))
```

<span id="3-3-2 (1b)" label="3-3-2 (1b)">3-3-2 (1b)</span>

```
Chalk another good one up to the wife .

(c / chalk-up-02 :mode imperative
      :ARG0 (y / you)
      :ARG1 (o / one
            :mod (a / another)
            :ARG1-of (g / good-02))
      :ARG2 (w / wife))
```


#### Part 3-3-3. Polarity
UMR mainly treats propositional negation at the document-level in the modal dependency annotation. However, the AMR attribute :polarity is also maintained in the UMR sentence-level annotation. It is used to flag any morphosyntactic indicators of negation that are present in the clause, as in [\[3-3-3 (1)\]](#3-3-3 (1)). These do not necessarily signal semantic negation. This is the case, for example, for some instances of derivational negation of adjectives in English. 

<span id="3-3-3 (1)" label="3-3-3 (1)">3-3-3 (1)</span>

<span id="3-3-3 (1a)" label="3-3-3 (1a)">3-3-3 (1a)</span>
```
Most of the time , economic policy and economic theory are not aimed at\
 individuals .

(a / aim-02 
      :polarity -
      :aspect State
      :ARG1 (a2 / and
            :op1 (p / policy-01)
            :op2 (t / theory)
            :mod (e / economy))
      :ARG2 (i / individual)
      :frequency (t2 / time
            :quant (m / most)))
```

<span id="3-3-3 (1b)" label="3-3-3 (1b)">3-3-3 (1b)</span>
```
Unhealthy food.

(t / thing
	:ARG1-of (e/ eat-01)
	:mod (h/ healthy
		:polarity -))
```

#### Part 3-3-4. Quant

<span id="3-3-4 (1)" label="3-3-4 (1)">3-3-4 (1)</span>

```
As of now , five million tickets have been sold on the StubHub website .
(s / sell-01
      :Aspect Performance
      :ARG1 (t / ticket :quant 5000000)
      :location (w / website
            :mod (c / company :wiki "StubHub" :name (n / name :op1 "StubHub")))
      :time (a / as-of
            :op1 (n2 / now)))
```

#### Part 3-3-5. Ref
As opposed to AMR, which uses an English-based lexical treatment of pronominal reference, UMR approaches pronominal reference and person/number marking in a cross-linguistically based way. It annotates person and number through two attributes - :ref-person, for grammatical person information, and :ref-number for grammatical number marking. These attributes can apply to any entity concept. If an explicit nominal is marked for plural or dual number, for instance, the node for this entity concept can take the relevant attribute value label, as in [\[3-3-5 (1)\]](#3-3-5 (1)).

<span id="3-3-5 (1)" label="3-3-5 (1)">3-3-5 (1)</span>

<span id="3-3-5 (1a)" label="3-3-5 (1a)">3-3-5 (1a)</span>
```
Bill saw rare birds today.
(s / see-01
	:ARG0 (p/ person
		:name (n/ name	:op1 "Bill"))
	:ARG1 (b/ bird
		:mod (r/ rare)
		:ref-number Plural))
```

<span id="3-3-5 (1b)" label="3-3-5 (1b)">3-3-5 (1b)</span>
```
áine	ŋara-di-a-ru.
woman	that-3PL-EP-DU
'Those two women'

(w/ woman
	:ref-number Dual
	:mod (a/ ŋara))
```

For arguments expressed only through verbal cross-referencing, or arguments that are implicit, both :ref-person and :ref-number can be used to represent their pronominal features. In such cases where there is no overt nominal expression to attach those values to, UMR "hallucinates" a concept (e.g., person, thing) to attach the attribute labels to in order to facilitate cross-lingual compatibility, as in [\[3-3-5 (2)\]](#3-3-5 (2)). In the context preceding this one-word sentence, the speaker talks about how upon first contact between the Sanapaná and Latinoparaguayans, the Paraguayans gifted the Sanapaná food and clothes. Here, the speaker describes the reaction of his ancestors to these gifts. From the prefixal indexation on the verb (2nd/3rd person masculine + distributive) and the preceding context (talking about the Sanapaná ancestors), we know that the :Actor argument of the eat-verb is third person plural. Therefore, we annotate this argument with a (p/ person) concept, which in turn takes :ref-person and :ref-number attributes with the relevant values. The :Undergoer of this predicate is not explicitly expressed at all, but from previous context we know it is the food that they were offere by the Paraguayans. We therefore annotate it with a (t/ thing) concept which takes a :ref-number Plural attribute. No :ref-number attribute is needed here, since the Thing concept implies third person rather than a speech act participant.

<span id="3-3-5 (2)" label="3-3-5 (2)">3-3-5 (2)</span>
```
m-e-hl-t-om-o=hlta
NEG-2/3M.IRR-DSTR-eat-PST/HAB-SBJ=PHOD
'They did not eat it.'

(e/ entoma-00 'eat'
	:Actor (p/ person
		:ref-person 3rd
		:ref-number Plural)
	:Undergoer (t/ thing
		:ref-number Singular)
	:polarity -)
```

The possible values for the :refer-person attribute are based on Cysouw's (2003) cross-linguistic study of person-marking system in the languages of the world. They are organized in a lattice as seen below. The default level of categories contains the well-known and familiar first, second, and third person values. Some languages have more fine-grained person systems, distinguishing a first person exclusive from a first person inclusive value in non-singular numbers (depending on whether the interlocutor is included in the group that is being referred to). Other languages have more coarse-grained systems, making no distinction between first and second person, or between second and third person (like Sanapaná above).

```
|         | coarse-gr | default | fine-gr   |
|---------|-----------|---------|-----------|
|         |           | 1st     | excl.     |
|         | non-3rd   |         | incl.     |
| pers.   |           | 2nd     |           |
|         | non-1st   |         |           |
|         |           | 3rd     |           |

```

The possible number values for the :refer-number attribute are based on Corbett (2000). The default level here consists simply of singular vs. non-singular. Languages with more fine-grained categories in their system may have Duals, Trials, and Paucals, and Greater Plurals, which fit together as shown in the figure below (add lattice image).

#### Part 3-3-6. Degree
In AMR, markers of degree such as English _very_ (high degree of a scalar quality, as in _very cold_) and _somewhat_ (low degree of a scalar quality, as in _somewhat dirty_) are treated lexically - a :degree relation is added to the property concept that is admodified. However, in many languages, such degree expressions are morphological rather than periphrastic - they form a single word with the property concept word. Such a lexical treatment is hard for these languages. UMR therefore allows annotators to treat :degree as an attribute, with three possible values: _intensifier_, _downtoner_, and _equal_. These values can in this way be attached directly to the whole property concept word without the need for morphological decomposition, as shown in [\[3-3-6 (1)\]](#3-3-6 (1)). For languages with periphrastic degree expressions like English, the lexical entry for words such as _very_ and _somewhat_ can be constructed to include reference to which of the three degree values listed above it expresses. In that way, English annotations would be comparable to annotations in a language like Sanapaná

<span id="3-3-6 (1)" label="3-3-6 (1)">3-3-6 (1)</span>
```
ak-yav-ay'-a=ngkoye	yamet
2/3F-be.large-PST/HAB-NOM=INTNS
'The tree is very large.'

(h / have-mod-91
	:ARG0 (y/ yamet 'tree')
	:ARG1 (e/ enyavay'a-00 'large'
		:degree Intensifier))
(h/ have-mod-91
	:ARG0 (t/ tree)
	:ARG1 (l/ large
		:degree (v/ very)))
Lexicon: Very - _Intensifier_
```

## Part 4. Document-Level Representation
### Part 4-1. Coreference


Anaphorical expressions such as pronouns cannot be properly interpreted without identifying their referents. This is generally done by linking an anaphorical expression to a named entity, a process generally known as *coreference* in the field of NLP. Coreference is an established NLP task, and the goal here is to identify the most relevant types of coreference in the UMR framework.  

For the UMR corereference annotation, we first need to answer two questions. The first is what counts as an anaphorical expression. For UMR annotation, we focus on pronouns. The second question is what types of coreference relations we are considering. The most common type of coreference relations are *identity* relations, and we label such relations as *same*. Identity relations means two expressions have the same referent. In [\[4-1 (1)\]](#4-1 (1)), *he* refers to the same person as the person whose name is "Edmond Pope":

<span id="4-1 (1)" label="4-1 (1)">4-1 (1)</span>

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
      :ARG0 (h / person
               :ref 3s)
      :ARG1 (t / thing
            :ARG1-of (d2 / do-02
                  :ARG0 h
                  :ARG1-of (w / wrong-02))))
  
(s3 / sentence
    :coref((s3h :same-entity s1p)) )
```

Subset relation:

<span id="4-1 (2)" label="4-1 (2)">4-1 (2)</span>
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

#### Part 4-1-2 Event coreference
 
	
 - Event identity

 We use *same-event* to represent cases where two event mentions refer to  the same event, as in [\[4-1-2 (1)\]](#4-1-2 (1)).
 
 <span id="4-1-2 (1)" label="4-1-2 (1)">4-1-2 (1)</span>
 
  <span id="4-1-2 (1a)" label="4-1-2 (1a)">4-1-2 (1a)</span>
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

 <span id="4-1-2 (1b)" label="4-1-2 (1b)">4-1-2 (1b)</span>
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

Event identity also includes cases where the same underlying event is referred to with two very different linguistic expressions. This is the case for **introduced** and **provide** in [\[4-1-2 (2)\]](#4-1-2 (2)).

 <span id="4-1-2 (2)" label="4-1-2 (2)">4-1-2 (2)</span>

<span id="4-1-2 (2a)" label="4-1-2 (2a)">4-1-2 (2a)</span>
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

<span id="4-1-2 (2b)" label="4-1-2 (2b)">4-1-2 (2b)</span>
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

*subset* is also used to annotate the subset relations between two event mentions, with one referring to a subset of another, as is the case in [\[4-1-2 (3)\]](#4-1-2 (3)).

<span id="4-1-2 (3)" label="4-1-2 (3)">4-1-2 (3)</span>

<span id="4-1-2 (3a)" label="4-1-2 (3a)">4-1-2 (3a)</span>
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
<span id="4-1-2 (3b)" label="4-1-2 (3b)">4-1-2 (3b)</span>
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

The temporal annotation in UMR is done at both the sentence level and the document level. For instance, a time expression that serves as the modifier of a predicate is annotated at the sentence level. In [\[4-2 (1)\]](#4-2 (1)), the time expression 
*April 1998* is annotated as a temporal modifier of the predicate *sign*. Likewise, the temporal relation between an event and its document creation time (DCT) is also annotated at the sentence level. In [\[4-2 (1)\]](#4-2 (1)), the temporal relation between *sign* and the DCT is annotated as `:time (b2 /before :op (n/now))`. The temporal relation between an event and a time expression is annotated when a time expression is present in the sentence. The temporal relation between an event and the DCT is annotated when this temporal relation is defined in that context. For example, while the relation between *signed* and the DCT is clearly defined, the temporal relation between *fight* and the DCT is not.


<span id="4-2 (1)" label="4-2 (1)">4-2 (1)</span>
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
annotation of ([\[4-2 (2)\]](#4-2 (2))) below.

<span id="4-2 (2)" label="4-2 (2)">\[4-2 (2)\]</span> *Lerias
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

UMR represents modal strength and polarity as a dependency structure.
The nodes are either events or conceivers (i.e., a source, an entity
whose perspective on an event is modelled in the text). The edges in the dependency structure correspond to modal strength and polarity values (i.e., how certain a specific conceiver is about the occurrence of the event in the real world). Annotators do not have to construct the dependency structure directly, but it can be built up “behind the
scenes” by annotating some modal/polarity information and leveraging
the participant role annotation.

The modal annotation captures the modal strength of events, but not the modal type of the event (i.e., epistemic/evidential, deontic,
permissive, etc.). These modal strengths are annotated based on a
lattice of annotation values that differ in terms of granularity. An
example of the UMR annotation and the underlying modal dependency
structure is shown below in [\[4-3 (1)\]](#4-3 (1)).


<span id="4-3 (1)" label="4-3 (1)">\[4-3 (1)\]</span>

![Modal dependency structure](modal-dependency.png)

Martin **said** that the package has probably already **arrived**.

```
(s / say  
	:actor (M / Martin)
	:theme (a / arrive  
		:theme (p / package)  
		quot: s
		modstr: Prt)
	modstr: Aff)  
```

The saying-event and the arriving-event each get a modal strength value (```modstr```), which can then be represented
in the dependency as shown on the right. The
```quot``` value indicates than an event is
being reported, and the participant role annotation can be used to
automatically select the conceiver for the reported event(s), here,
*Martin*.

The road map stages build on each other to end up at a fully specified
modal dependency structure. This means that Stage 2 annotation involves first doing the Stage 1 modality annotations. (This contrasts with participant roles, where annotators can largely ignore Stage 1 if the annotation language has existing frame files.)

#### Part 4-3-1. Stage 1

There are two types of modal annotations at Stage 1: a
```modstr``` annotation that consists of a
single epistemic strength/polarity value and a dependency annotation
that indicates a relation between two events. There are four dependency
relations, ```mod``` for the link between a
modal event and the event(s) that it modalizes,
```quot``` for the link between a reporting
event and the event(s) that it reports,
```purp``` for the link between a main clause
event and an event in a purpose clause, and
```cond``` for the relation between the
apodasis and protasis in a conditional construction. The
```modstr``` annotation applies to all events,
except for those under the scope of a modal identified as its own event (i.e., events with ```mod``` relations). This
is summarized below.

Events under the scope of modal events: ```mod``` relation  
Events under the scope of reporting events: ```modstr``` annotation;
```quot``` relation  
Events in purpose clauses: ```modstr``` annotation; ```purp``` relation  
Events in conditionals: ```modstr``` annotation; ```cond``` relation  
All other events: ```modstr``` annotation

##### Part 4-3-1-1. ```modstr``` values

The modal strength values correspond to epistemic strength, i.e. the
author or conceiver’s certainty about the occurrence of the event in the real world, or certainty about another conceiver’s mental content. Based on Boye (2012), a typological study of modal systems across languages, and following FactBank (Pustejovsky et al. 2005), the UMR annotation is based around three levels of modal strength: Full, Partial, and Neutral, illustrated in [\[4-3-1-1 (1)\]](#4-3-1-1 (1)).

<span id="4-3-1-1 (1)" label="4-3-1-1 (1)">\[4-3-1-1 (1)\]</span>

<span id="4-3-1-1 (1a)" label="4-3-1-1 (1a)">\[4-3-1-1 (1a)\]</span> Full:  
The cat already **ate** breakfast.

<span id="4-3-1-1 (1b)" label="4-3-1-1 (1b)">\[4-3-1-1 (1b)\]</span>
Partial:  
The cat <u>probably</u> already **ate** breakfast.  

<span id="4-3-1-1 (1c)" label="4-3-1-1 (1c)">\[4-3-1-1 (1c)\]</span>
Neutral:  
The cat <u>might</u> have already **eaten** breakfast.

The Full modal strength value, as in [\[4-3-1-1 (1a)\]](#4-3-1-1 (1a)), corresponds to complete certainty; that is, the conceiver is 100% certain that the event occurs in the real world. The Neutral modal strength value, shown in [\[4-3-1-1 (1c)\]](#4-3-1-1 (1c)), indicates the possibility of the event; essentially, this corresponds to 50/50 certainty that the event occurs in the real world. The Partial modal strength value, as in [\[4-3-1-1 (1b)\]](#4-3-1-1 (1b)), falls between the Full and Neutral values; the conceiver believes that more likely than not, the event occurs in the real world.

But, Full, Partial, and Neutral aren’t the only possible modal strength annotation values. Languages differ in the modal strength distinctions that are conventionalized in their grammar. In order to accommodate these differences, we use a typological lattice of annotation values, constructed based on the structure of the annotation categories across languages (Van Gysel et al. 2019).

One level of granularity in the lattice is designated as the “base
level”: annotators are encouraged to use categories from this level as
the default. These values are selected as the base level because these
distinctions occur the most frequently across languages. The higher and lower levels, respectively, contain equally typologically-motivated coarser-grained and finer-grained categories, which can be used when a language conventionalizes these distinctions in its grammar. Such lattices capture the idea that many semantic categories are structured as hierarchical scales, where the middle values can group together with either end, but the extremes of the scale are highly unlikely to be categorized together in any language. For example, no language has a grammatical form that is used for both Full and Neutral epistemic strength, but not Partial. The typological lattice for epistemic strength is shown below.

![Modal strength lattice](modal-lattice.png)

This lattice is based around the base level of Full vs. Partial vs.
Neutral, but also allows for the annotation of more coarse-grained
values that lump together the distinctions in the base level, and more
fine-grained annotation values. For contexts where it is unclear if the modal strength is Full or Partial, the Non-neutral value can be used; if it is unclear whether the modal strength is Partial or Neutral, then the Non-full value can be used. The most fine-grained modal strength values are generally used with languages that have grammatical forms that encode the relevant distinction.

Also following FactBank (Pustejovsky et al. 2006), the ```modstr```
annotation combines the epistemic strength values with a binary polarity distinction (Affirmative, Negative). This results in six modal strength/polarity values for the default level, shown below.

<div>

| **Label**                              | **Value**                              |
| :------------------------------------- | :------------------------------------- |
| ```Aff```     | full strength, affirmative polarity    |
| ```Prt```     | partial strength, affirmative polarity |
| ```Neut```    | neutral strength, affirmative polarity |
| ```NeutNeg``` | neutral strength, negative polarity    |
| ```PrtNeg```  | partial strength, negative polarity    |
| ```Neg```    | full strength, negative polarity       |

</div>

These values and their interpretation are shown below; the corresponding FactBank values are in parentheses.

```Aff```: full affirmative support; complete certainty that the event occurs (CT+)  
```Prt```: partial affirmative support; there is strong, but not definitive certainty that the event occurs (PR+)  
```Neut```: affirmative neutral support; there is neutral certainty that the event occurs/doesn’t occur; event is expressed positively (PS+)  
```NeutNeg```: negative neutral support; there is neutral certainty that the event occurs/doesn’t occur; negation of event is expressed (PS-)  
```PrtNeg```: partial negative support; there is strong but not definitive certainty that the event does not occur (PR-)  
```Neg```: full negative support; complete certainty that the event does not occur (CT-)

Degree of certainty corresponds most straightforwardly to the degree of confidence of a conceiver (often, the author) in the occurrence of an episodic event, i.e. the epistemic continuum from certainty to
possibility. We use these same values for the evidential continuum from direct evidence to second-hand (reported or inferred) evidence; see [\[evidentialjust\]](#evidentialjust) below. And these values are
interpreted into the domain of future-oriented or deontic modality, as
explained in [\[futureevents\]](#futureevents). The interpretation of
the value - as epistemic, evidential or deontic - is not reflected in
the modal strength annotation.

##### Part 4-3-1-1-1. Non-future events

For non-future (non-deontic) events, the ```modstr``` values correspond to the author’s level of certainty towards the occurrence of the event in the real world. Events presented as fact are annotated with
```Aff```, while events for which the author categorically denies their occurrence are annotated ```Neg```. When the author doesn’t present the
event as fact, but has a higher level of certainty towards the event
either being true or not true, this is annotated as
```Prt``` or, when the polarity is negative, ```PrtNeg```. When the author doesn’t lean either direction towards the event being true in the real world or not, the event is annotated as ```Neut``` or
```NeutNeg```, depending on the polarity of the
linguistic expression. These strength values are exemplified in
([\[4-3-1-1-1 (1)\]](#4-3-1-1-1 (1))).


<span id="4-3-1-1-1 (1)" label="4-3-1-1-1 (1)">\[4-3-1-1-1 (1)\]</span>

<span id="4-3-1-1-1 (1a)" label="4-3-1-1-1 (1a)">\[4-3-1-1-1 (1a)\]</span> The dog **barked**
last night.  
```
(b / bark  
	modstr: Aff)  
```
<span id="4-3-1-1-1 (1b)" label="4-3-1-1-1 (1b)">\[4-3-1-1-1 (1b)\]</span> The dog <u>probably</u> **barked** last night.  
```
(b / bark  
modstr: Prt)  
```
<span id="4-3-1-1-1 (1c)" label="4-3-1-1-1 (1c)">\[4-3-1-1-1 (1c)\]</span> The dog <u>may</u> have **barked** last night.  
```
(b / bark  
	modstr: Neut)  
```
<span id="4-3-1-1-1 (1d)" label="4-3-1-1-1 (1d)">\[4-3-1-1-1 (1d)\]</span> The dog <u>may not</u> have **barked** last night.  
```
(b / bark  
	modstr: NeutNeg)  
```

<span id="4-3-1-1-1 (1e)" label="4-3-1-1-1 (1e)">\[4-3-1-1-1 (1e)\]</span> The dog <u>probably didn’t</u> **bark** last night. 
```
(b / bark  
	modstr: PrtNeg)  
```

<span id="4-3-1-1-1 (1f)" label="4-3-1-1-1 (1f)">\[4-3-1-1-1 (1f)\]</span> The dog <u>didn’t</u> **bark** last night.  
```   
(b / bark  
	modstr: Neg)  
```

##### Part 4-3-1-1-2. Evidential justification

Following Boye (2012) and Saurí and Pustejovsky (2009), we conflate evidential justification with epistemic support. Boye (2012) finds that there is cross-linguistic evidence for lumping epistemic support and evidential justification together into the same relations. Languages may encode direct evidential justification (sensory perception) with the same forms as full epistemic support; indirect justification (hearsay, inferential) may be encoded by the same forms as partial epistemic support.

Example [\[4-3-1-1-2 (1)\]](#4-3-1-1-2 (1)) shows how direct and indirect justification correspond to epistemic support.

<span id="4-3-1-1-2 (1)" label="4-3-1-1-2 (1)">\[4-3-1-1-2 (1)\]</span>

<span id="4-3-1-1-2 (1a)" label="4-3-1-1-2 (1a)">\[4-3-1-1-2 (1a)\]</span> (I **saw**) Mary <span class="smallcaps">feed</span> the cat.
```
(f / feed  
	modstr: Aff)
```
<span id="4-3-1-1-2 (1b)" label="4-3-1-1-2 (1b)">\[4-3-1-1-2 (1b)\]</span> Mary **must** have <span class="smallcaps">fed</span> the cat.
```
(f / feed  
	modstr: Prt) 
```

In [\[4-3-1-1-2 (1a)\]](#4-3-1-1-2 (1a)), the author has direct knowledge of the feeding event, by way of witnessing it. Therefore, *feed* is annotated with ```Aff``` modal strength. In
[\[4-3-1-1-2 (1b)\]](#4-3-1-1-2 (1b)), however, *must* signals that the author is inferring that the feeding event occurred without direct, perceptual knowledge. Therefore, *fed* in [\[4-3-1-1-2 (1b)\]](#4-3-1-1-2 (1b)) is annotated with ```Prt``` modal strength.

##### Part 4-3-1-1-3. Future events and deontic modality

For events presented as (potentially) happening in the future,
```modstr``` refers to the predictability of
the occurrence of the event in the future, as presented by the author.
Predictive future has full strength (```Aff```
or ```Neg```); intentions and commands
correspond to partial strength (```Prt``` or
```NegPrt```); and desire and permission
correspond to neutral (```Neut``` or
```NeutNeg```) strength. Keep in mind that events under the scope of modals identified as their own event don't receive any ```modstr``` value at all. This section refers to deontic meanings indicated by grammaticalized modals that don't fit the criteria to be identified as events.

This is illustrated in ([\[4-3-1-1-3 (1)\]](#4-3-1-1-3 (1))).

<span id="4-3-1-1-3 (1)" label="4-3-1-1-3 (1)">\[4-3-1-1-3 (1)\]</span>

<span id="4-3-1-1-3 (1a)" label="4-3-1-1-3 (1a)">\[4-3-1-1-3 (1a)\]</span> I <u>will</u> **go** to Santa Fe. 
```
(g / go  
	modstr: Aff) 
```

<span id="4-3-1-1-3 (1b)" label="4-3-1-1-3 (1b)">\[4-3-1-1-3 (1b)\]</span> You <u>must</u> **go** to Santa Fe.  
```
(g / go  
	modstr: Prt)  
```

<span id="4-3-1-1-3 (1c)" label="4-3-1-1-3 (1c)">\[4-3-1-1-3 (1c)\]</span> You can go to Santa Fe.  
```
(g / go  
	modstr: Neut)  
```
 
The predictive future, as in [\[4-3-1-1-3 (1a)\]](#4-3-1-1-3 (1a)), is annotated with
full modal strength because it presents the future event as a certainty
(i.e., it is as certain as is possible for future events). Commands, as
in [\[4-3-1-1-3 (1b)\]](#4-3-1-1-3 (1b)), are annotated with partial modal strength
because they present the future event as less likely than the predictive
future, but more likely to happen than the neutral strength deontics.
Finally, permission, as in [\[4-3-1-1-3 (1c)\]](#4-3-1-1-3 (1c)), is annotated as
neutral strength.

##### Part 4-3-1-2. ```mod``` relation

Events under the scope of a modal identified as its own event are only
annotated with a ```mod``` relation to the
relevant modal. This is shown below in [\[4-3-1-2 (1)\]](#4-3-1-2 (1)).

<span id="4-3-1-2 (1)" label="4-3-1-2 (1)">\[4-3-1-2 (1)\]</span>

<span id="4-3-1-2 (1a)" label="4-3-1-2 (1a)">\[4-3-1-2 (1a)\]</span> Mary <u>**wants**</u> to
**visit** France.
```
(w / want  
	(v / visit  
		mod: w)  
	modstr: Aff)  
```

<span id="4-3-1-2 (1b)" label="4-3-1-2 (1b)">\[4-3-1-2 (1b)\]</span> Rob <u>**thinks**</u>
the dog **escaped** through the fence.
```
(t / think  
	(e / escape  
		mod: t)  
	modstr: Aff)
```

<span id="4-3-1-2 (1c)" label="4-3-1-2 (1c)">\[4-3-1-2 (1c)\]</span> They <u>probably</u>
<u>**decided**</u> to **leave** on Monday.
```
(d / decide  
	(l / leave  
		mod: d)  
	modstr: Prt)  
```

<span id="4-3-1-2 (1d)" label="4-3-1-2 (1d)">\[4-3-1-2 (1d)\]</span> His parents
<u>**forbid**</u> him from **smoking**.
```
(f / forbid  
	(s / smoke  
		mod: f)  
	modstr: Aff)
```

Note that the modal itself is annotated with a
```modstr``` value (if it is not under the
scope of another modal). The actual modal value imparted by the modal
event is not annotated at Stage 1.

##### Part 4-3-1-3. ```quot``` relation

Events under the scope of a reporting predicate or a speech predicate
are annotated with a ```quot``` relation to the
reporting or speech predicate. Unlike events under the scope of modals,
these events are also annotated with a
```modstr``` value.


<span id="4-3-1-3 (1)" label="4-3-1-3 (1)">\[4-3-1-3 (1)\]</span>

<span id="4-3-1-3 (1)" label="4-3-1-3 (1)">\[4-3-1-3 (1)\]</span> Mary <u>**said**</u>
that she **went** to Santa Fe.
```
(s / say  
	(g / go  
		quot: s  
		modstr: Aff)  
	modstr: Aff)  
```

<span id="4-3-1-3 (1a)" label="4-3-1-3 (1a)">\[4-3-1-3 (1a)\]</span> The New York Times
<u>**reported**</u> that Congress **voted** on the bill this afternoon.
```
(r / report  
	(v / vote  
		quot: r  
		modstr: Aff)  
	modstr: Aff) 
```

<span id="4-3-1-3 (1b)" label="4-3-1-3 (1b)">\[4-3-1-3 (1b)\]</span> Mary <u>might</u>
have <u>**said**</u> that she **went** to Santa Fe.
```
(s / say  
	(g / go  
		quot: s  
		modstr: Aff)  
	modstr: Neut)  
```

<span id="4-3-1-3 (1c)" label="4-3-1-3 (1c)">\[4-3-1-3 (1c)\]</span> Mary <u>didn’t</u>
<u>**say**</u> that she **went** to Santa Fe.
```
(s / say  
	(g / go  
		quot: s  
		modstr: Aff)  
	modstr: Neg)
```

<span id="4-3-1-3 (1d)" label="4-3-1-3 (1d)">\[4-3-1-3 (1d)\]</span> Mary
<u>**said**</u> that John <u>might</u> have **gone** to Santa Fe.
```
(s / say  
	(g / go  
		quot: s  
		modstr: Neut)  
	modstr: Aff) 
```

<span id="4-3-1-3 (1e)" label="4-3-1-3 (1e)">\[4-3-1-3 (1e)\]</span> Mary <u>**said**</u>
that John <u>probably didn’t</u> **go** to Santa Fe.
```
(s / say  
	(g / go  
		quot: s  
		modstr: PrtNeg)  
	modstr: Aff)  
```

As can be seen above, both the reporting predicate and the reported
events are annotated with a ```modstr``` value.
The ```modstr``` value of the reporting
predicate corresponds to the author’s certainty that the reporting event
happened. The ```modstr``` value associated
with the reported events corresponds to the certainty with which the
sayer/reporter reports the events. For example, in
[\[4-3-1-3 (1d)\]](#4-3-1-3 (1d)), the author is certain about the saying event,
so it is annotated with ```Aff```; but Mary is
unsure about the reality of the going event, and therefore it is
annotated with ```Neut``` modal strength.

##### Part 4-3-1-4. ```purp``` relation

Events in purpose clauses are annotated with both a
```modstr``` value and ```purp``` relation to the main clause event.


<span id="4-3-1-4 (1)" label="4-3-1-4 (1)">\[4-3-1-4 (1)\]</span>
They **dropped** water <u>in order to</u> **fight** the fire.
```
(d / drop  
	(f / fight  
		purp: d  
		modstr: Aff)  
	modstr: Aff) 
```

<span id="4-3-1-4 (2)" label="4-3-1-4 (2)">\[4-3-1-4 (2)\]</span>
He **walked** quickly <u>in order to</u> not **arrive** late.
```
(w / walked  
	(a / arrive  
		purp: w  
		modstr: Neg)  
	modstr: Aff)  
```

The ```modstr``` value represents any modals or
negation that are present within the purpose clause. That is, this value
doesn’t capture the fact that the purpose clause itself imparts a
non-full epistemic stance on its events; that is captured by the
```purp``` relation.

##### Part 4-3-1-5. ```cond``` relation

The ```cond``` relation indicates the relationship between events in conditional constructions. These events
also receive a ```modstr``` annotation. As can
be seen in [\[4-3-1-5 (1)\]](#4-3-1-5 (1)), the event in the apodasis is annotated with a ```cond``` relation to the event in the
protasis.

<span id="4-3-1-5 (1)" label="4-3-1-5 (1)">\[4-3-1-5 (1)\]</span>

<span id="4-3-1-5 (1a)" label="4-3-1-5 (1a)">\[4-3-1-5 (1a)\]</span> If she’s **hungry**, I’ll **feed** her dinner.
```
(h / have-mod-91  
	modstr: Aff)  
(f / feed  
	modstr: Aff  
	:cond h)
```

<span id="4-3-1-5 (1b)" label="4-3-1-5 (1b)">\[4-3-1-5 (1b)\]</span> If she’s **hungry**, maybe I’ll **cook** pasta.
```
(h / have-mod-91  
	modstr: Aff)  
(f / feed  
	modstr: Prt  
	:cond h)
```

<span id="4-3-1-5 (1c)" label="4-3-1-5 (1c)">\[4-3-1-5 (1c)\]</span> If she **isn’t hungry**, we’ll just **watch** a movie.
```
(h / have-mod-91  
	modstr: Neg)  
(f / feed  
	modstr: Aff 
	:cond h)  
```

As with purpose clauses, the ```modstr``` value
doesn’t capture the uncertainty imparted by the conditional construction
itself; it corresponds to any negation or modals which are expressed
inside of the conditional construction. The modal value of the
conditional construction is captured by the
```cond``` value.

##### Part 4-3-1-6. Modal dependency structure

At Stage 1, there are some pieces of the modal dependency structure that
are unspecified. The modal strength that a modal verb imparts on its
complement is one of these pieces. As the modal annotation progresses,
this information is added to the frame files for modal verbs. For
example, the complements of English *want* have a
```Neut``` ```modstr``` value; this will be indicated
in the frame file as shown below.

```
Predicate: want.01 
	Roles:  
	Arg0: wanter  
	Arg1: thing wanted  
	Arg2: beneficiary  
	Arg3: in-exchange-for  
	Arg4: from 

modstr of complement: Neut  
```

For the complements of modals, the ```modstr```
values work largely the same way that they do for other events; however,
they reflect the beliefs of the
```experiencer``` participant of the modal
event, who is often not the author. For example, in
[\[4-3-1-6 (1)\]](#4-3-1-6 (1)), Mary believes that the visit event may take
place in the future (```Neut``` strength), but
the author disagrees.

<span id="4-3-1-6 (1)" label="4-3-1-6 (1)">\[4-3-1-6 (1)\]</span> Mary wants
to visit France next month, but I don’t think that’s possible.

The value associated with the modal event in its frame file corresponds
to Mary’s beliefs, as the ```experiencer``` of
the wanting event.

Some predicates impart full, positive
(```Aff```) strength on their complements,
often called factive predicates (e.g., *manage to*). Strong epistemic
modals (e.g., *expect that, deduce*) and strong deontic modals,
including intention modals (e.g., *plan to, decide to*) and obligation
modals (e.g., *need, demand*), impart ```Prt```
strength on their complements. Weak deontic modals, including desire
(e.g., *want*) and permission (e.g., *allow*), impart
```Neut``` strength on their complements.
Certain modals may also lexicalize negation, such as *doubt*, *forbid*,
or *wish*. These are annotated with the
```NeutNeg```,
```PrtNeg```, and
```Neg``` values, respectively.

#### 4.3.2 English modals

This list gives the modal strength value associated with common English
modal constructions (this is certaintly not an exhaustive list). For
modal predicates that are identified as their own event (e.g.,
deontic predicates), the modal strength value characterizes the dependency link between the modal predicate node and its child event. For example, *want* is in the ```Neut``` list, which indicates that there
is a ```Neut``` link between the ```want``` node and its
complement event node in the full dependency structure.   

```Aff``` (full affirmative)

  - Simple assertions: declarative sentences

  - Certainty: *certainly, be sure, definitely, necessarily*

  - Predictive future: *will,* non-intentional *be going to*

  - Factual predicates: *manage to, finished*

```Prt``` (partial affirmative)

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

```Neut``` (neutral affirmative)

  - Weak epistemic modals: *may, might/might have, could have*

  - Weak epistemic adverbs/adjectives: *maybe, possibly/be possible
    that*

  - Conditionals

  - Hope/Fear: *hope, fear, worry, dread*

  - Weak deontic modals
    
      - Desire: *want, prefer, would like to*
    
      - Permission: *let, permit, allow*

```NeutNeg``` (neutral negative)

  - Doubt: *doubt, call into question, be dubious that, be skeptical
    that*

  - Combination of (some) <span>Neut</span> lexical items with negation

```PrtNeg``` (partial negative)

  - Strong negative deontics: *forbid, ban, disallow*

  - Negative imperatives

  - Combination of (some) <span>Prt</span> lexical items with negation

```Neg``` (full negative)

  - Negation: *not, never, no* + noun phrase

  - Negative complement taking predicates that entail that the event
    didn’t happen: *deny, prevent, prohibit, block, cease, it is
    impossible that, avoid*

  - Counterfactuals

  - Wishes: *wish*
  
  
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


