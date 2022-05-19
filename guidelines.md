# Uniform Meaning Representation (UMR) 0.8 Specification
=======================================================

**April 17, 2021**

-AUTHORS-

**<span id="toc" label="toc">Table of Contents</span>**  

* Part 1. [Introduction: What is UMR and what does UMR annotation look like?](#part-1-introduction-what-is-UMR-and-what-does-UMR-annotation-look-like)
* Part 2. [From AMR to UMR](#part-2-from-amr-to-umr)
    * Part 2-1. [Introduction](#part-2-1-introduction)
    * Part 2-2. [Introduction for field linguists](#part-2-2-introduction-for-field-linguists)
      * Part 2-2-1. [Predicate-argument relations](#part-2-2-1-predicate-argument-relations)
      * Part 2-2-2. [Multi-word expressions](#part-2-2-2-multi-word-expressions)
      * Part 2-2-3. [Abstract concepts](#part-2-2-3-abstract-concepts)
      * Part 2-2-4. [Non-participant role relations](#part-2-2-4-non-participant-role-relations)
      * Part 2-2-5. [Attributes](#part-2-2-5-attributes)
* Part 3. [Sentence-Level Representation](#part-3-sentence-level-representation)
    * Part 3-1. [UMR Concepts](#part-3-1-umr-concepts)
      * Part 3-1-1. [Eventive concepts](#part-3-1-1-eventive-concepts)
      	* Part 3-1-1-1. [Processes in predication](#part-3-1-1-1-processes-in-predication)
      	* Part 3-1-1-2. [Processes in modification and reference](#part-3-1-1-2-processes-in-modification-and-reference)
      	* Part 3-1-1-3. [States and entities](#part-3-1-1-3-states-and-entities)
      	* Part 3-1-1-4. [Implicit events](#part-3-1-1-4-implicit-events) 	
      * Part 3-1-2. [Named entities](#part-3-1-2-named-entities)  
      * Part 3-1-3. [Concept-word mismatches](#part-3-1-3-concept-word-mismatches) 
         * Part 3-1-3-1. [Predicate and argument as one word](#part-3-1-3-1-predicate-and-argument-as-one-word)
         * Part 3-1-3-2. [Valency-changing operations](#part-3-1-3-2-Valency-changing-operations)
         * Part 3-1-3-3. [TAM categories](#Part-3-1-3-3-TAM-categories)
         * Part 3-1-3-4. [Associated motion](#Part-3-1-3-4-Associated-Motion)
         * Part 3-1-3-5. [Non-verbal clauses](#Part-3-1-3-5-Non-verbal-clauses)
         * Part 3-1-3-6. [Multi-word concepts](#part-3-1-3-6-multi-word-concepts)
      * Part 3-1-4. [Word senses](#part-3-1-4-word-senses)
      * Part 3-1-5. [Scope for quantification and negation](#part-3-1-5-scope-for-quantification-and-negation)
      * Part 3-1-6. [Discourse relations](#part-3-1-6-discourse-relations)
    * Part 3-2. [UMR relations](#part-3-2-umr-relations) 
      * Part 3-2-1. [Participant roles](#part-3-2-1-participant-roles)
      	* Part 3-2-1-1. [Stage 0](#part-3-2-1-1-stage-0) 
      		* Part 3-2-1-1-1. [Nonverbal clauses](#part-3-2-1-1-1-nonverbal-clauses)
      		* Part 3-2-1-1-2. [Valency alternations](#part-3-2-1-1-2-valency-alternations)
      	* Part 3-2-1-2. [Stage 1](#part-3-2-1-2-stage-1)
      		* Part 3-2-1-2-1. [Valency alternations](#part-3-2-1-2-1-valency-alternations)
      	* Part 3-2-1-3. [Inverse participant roles](#part-3-2-1-3-inverse-participant-roles)
      	* Part 3-2-1-4. [Table of verb meanings](#part-3-2-1-4-table-of-verb-meanings)
      * Part 3-2-2. [Non-participant role UMR relations](#part-3-2-2-Non-participant-role-UMR-relations)
      	* Part 3-2-2-1. [Temporal relations](#part-3-2-2-1-temporal-relations)
     	* Part 3-2-2-2. [Modifiers](#part-3-2-2-2-modifiers)
     	* Part 3-2-2-3. [Circumstantial temporals and locatives](#part-3-2-2-3-circumstantial-temporals-and-locatives)
     	* Part 3-2-2-4. [Named entities](#part-3-2-2-4-named-entities)
     	* Part 3-2-2-5. [Quantification](#part-3-2-2-5-quantification)
     	* Part 3-2-2-6. [Other relations](#part-3-2-2-6-other-relations)
    * Part 3-3. [UMR attributes](#part-3-3-UMR-attributes) 
      * Part 3-3-1. [Aspect](#part-3-3-1-Aspect) 
      	* Part 3-3-1-1. [Event nominals](#part-3-3-1-1-event-nominals)
      	* Part 3-3-1-2. [Habitual](#part-3-3-1-2-habitual)
      	* Part 3-3-1-3. [State](#part-3-3-1-3-state)
      	* Part 3-3-1-4. [Activity](#part-3-3-1-4-activity)
      	* Part 3-3-1-5. [Endeavor and Performance](#part-3-3-1-5-endeavor-and-performance) 
      * Part 3-3-2. [Mode](#part-3-3-2-mode)
      * Part 3-3-3. [Polarity](#part-3-3-3-polarity)
      * Part 3-3-4. [Quant](#part-3-3-4-quant)
      * Part 3-3-5. [Ref](#part-3-3-5-ref)
      * Part 3-3-6. [Degree](#part-3-3-6-degree)    
* Part 4. [Document-Level Representation](#part-4-document-level-representation)
    * Part 4-1. [Coreference](#part-4-1-coreference)
    	* Part 4-1-1. [Entity coreference](#part-4-1-1-entity-coreference)
    	* Part 4-1-2.  [Event coreference](#part-4-1-2-event-coreference)
    * Part 4-2. [Temporal dependency](#part-4-2-temporal-dependency)
    	* Part 4-2-1. [Temporal superstructure](#part-4-2-1-temporal-superstructure)
    		* Part 4-2-1-1. [Pre-defined metanodes](#part-4-2-1-1-pre-defined-metanodes)
    		* Part 4-2-1-2. [Time expressions](#part-4-2-1-2-time-expressions)
    		* Part 4-2-1-3. [Key events](#part-4-2-1-3-key-events)
    	* Part 4-2-2. [Temporal relations](#part-4-2-2-temporal-relations)
    		* Part 4-2-2-1. [Choosing the right temporal relation](#part-4-2-2-1-choosing-the-right-temporal-relation)
    		* Part 4-2-2-2. [Contained or Overlap](#part-4-2-2-2-contained-or-overlap)
    		* Part 4-2-2-3. [Causally-related events](#part-4-2-2-3-causally-related-events)
    		* Part 4-2-2-4. [Deontic modal events](#part-4-2-2-4-deontic-modal-events)  
    * Part 4-3. [Modal dependency](#part-4-3-modal-dependency) 
    	* Part 4-3-1. [Stage 0](#part-4-3-1-stage-0) 
    		* Part 4-3-1-1. [modstr values](#part-4-3-1-1-modstr-values)
    			* Part 4-3-1-1-1. [Non-future events](#part-4-3-1-1-1-non-future-events)
    			* Part 4-3-1-1-2. [Evidential justification](#part-4-3-1-1-2-evidential-justification)
    			* Part 4-3-1-1-3. [Future events and deontic modality](#part-4-3-1-1-3-future-events-and-deontic-modality)
    		* Part 4-3-1-2. [modpred relation](#part-4-3-1-2-modpred-relation)
    		* Part 4-3-1-3. [quot relation](#part-4-3-1-3-quot-relation)
    		* Part 4-3-1-4. [purpose relation](#part-4-3-1-4-purpose-relation)
    		* Part 4-3-1-5. [condition relation](#part-4-3-1-5-condition-relation)
    		* Part 4-3-1-6. [Modal dependency structure](#part-4-3-1-6-modal-dependency-structure)
    	* Part 4-3-2. [English modals](#part-4-3-2-english-modals)  

* Part 5. [Annotation Cheat Sheet](#part-5-annotation-cheat-sheet)
    
* Part 6. [Integrated examples](#part-6-integrated-examples)

* Part 7. [Alphabetical Index of UMR Annotation Categories](#part-7-alphabetical-index-of-UMR-annotation-categories)


##  Part 1. Introduction: What is UMR and what does UMR annotation look like?

The **Uniform Meaning Representation** (UMR) project aims to design a meaning representation that facilitates
the computational interpretation of a text. UMR combines a **sentence-level** representation that is adapted 
from **Abstract Meaning Representation** (AMR), which focuses on **predicate-argument structures**, **word senses**, **named entities**, **multi-word expressions**, **aspect**, and **quantification**, and a document-level representation that focuses on **coreference**, **temporal** and **modal** relations. We illustrate this representation with a short English document as in [\[1 (1)\]](#1 (1)) - [\[1 (9)\]](#1 (9)), and then describe in more detail each component of UMR in the next few sections. UMR is intended to be a cross-lingual annotation framework with a shared set of **abstract** concepts and relations. 

Operationally, for both sentence-level and document-level annotation, we assume an annotation procedure in which a document is processed sentence by sentence. The sentence-level representation is annotated first, so that the document-level annotation can make reference to the concepts in the sentence-level representation.

<span id="1 (1)" label="1 (1)">\[1 (1)\]</span>
```
Snt1: Edmund Pope tasted freedom today for the first time in more than eight months.

(t/ taste-01
  :ARG0 (p/ person :wiki "Edmond_Pope"
         :name (n/ name :op1 "Edmund" :op2 "Pope"))
  :ARG1 (f/ free-04
         :ARG1 p)
  :temporal (t2/ today)
  :ord (o/ ordinal-entity :value 1
        :range (m/ more-than
                :op1 (t3/ temporal-quantity :quant 8
                    :unit (m2/ month))))
  :aspect Performance
  :modstr FullAff)
                    
(s1/ sentence
    :temporal((DCT :depends-on s1t2)
	      (s1t2 :contained s1t))
    :modal(AUTH :FullAff s1t))
        
```
The document-level representation includes a list of **temporal and modal dependencies**, as well as a list of **coreference relations**. In this first sentence, the first temporal relation is between *DCT*, a constant that refers to the time when the document is created, and *today*, a concept that can only be correctly interpreted if we know the DCT of the document. In this sense, we say that *today* depends on DCT, hence the relation between them is *:depends-on*. We will define the set of temporal relations used in UMR in [Part 4-2-2](#part-4-2-2-temporal-relations).  The second temporal relation is between *today* and *taste-01*, and we say here *taste-01* happened sometime *today* and therefore is _:contained_ in *today*.

The document-level representation also includes a list of modal dependencies. There is only one modal relation in this sentence, and it is between *taste-01* and *AUTH*. Like DCT, AUTH is also a constant - it refers to the author of this text as a *conceiver*, or in other words, as the *source* of the modal judgment of certainty about the *taste-01* event, which is indicated by the *:FullAff* label.

<span id="1 (2)" label="1 (2)">\[1 (2)\]</span>
```
Snt2: Pope is the American businessman who was convicted last week on spying charges and sentenced to 20 years in a Russian prison.

(i/ identity-91
     :ARG0 (p/ person :wiki "Edmond_Pope"
     	:name (n/ name "op1 "Pope))
     :ARG1 (b/ businessman
	:mod (n2/ nationality :wiki "United_States"
	   :name (n3/ name :op1 "America")))
	:ARG1-of (c/ convict-01
	   :ARG2 (c2/ charge-05
	      :ARG1 b
	      :ARG2 (s/ spy-02
	         :ARG0 b
		 :modpred c2))
	   :temporal (w/ week
	      :mod (l/ last))
	   :aspect Performance
	   :modstr FullAff)
	:ARG1-of (s2/ sentence-01
	   :ARG2 (p2/ prison
	      :mod (c3/ country :wiki "Russia"
	         :name (n4/ name :op1 "Russia))
	      :duration (t/ temporal-quantity
	         :quant 20
		 :unit (y/ year)))
	   :ARG3 s
	   :aspect Performance
	   :modstr FullAff)
     :aspect State
     :modstr FullAff)
 
(s2/ sentence
    :temporal((DCT :depends-on s2w)
    	      (s2w :contained s2c)
	      (s2w :contained s2s2)
	      (s2c :after s2s))
    :modal((AUTH :FullAff s2i)
      	   (AUTH :FullAff s2c)
	   (AUTH :FullAff NULL_CHARGER)
	   (NULL_CHARGER :FullAff s2c)
	   (s2c :Unsp s2s)
    :coref(s1p :same-entity s2p))
```
<!-- should annotate coreference for nominals? if so we need to annotate "the american businessman"-->

For this sentence, the temporal relations represent the fact that the *conviction* event and the *sentence* event both
happened *last week*, which itself depends on the DCT for its temporal interpretation, and that the *sentence* event happened after the *conviction*. The modal dependencies indicate that from the author's perspective, the *conviction* event and the
*sentence* event definitely happened, and that *Pope* is certainly *the American businessman*. It introduces a *NULL_CHARGER* conceiver to indicate that the authority that charged Pope (which is not explicit in the text) presents the *spying* event as a certainty. The coreference annotation specifies that *Pope* in sentence 2 and *Edmund Pope* in sentence 1 are the same entity.

<span id="1 (3)" label="1 (3)">\[1 (3)\]</span>
```
Snt3: He denied any wrongdoing.
(d/ deny-01 
      :ARG0 (p/person
         :ref-person 3rd
	 :ref-number Singular)
      :ARG1 (t/ thing
            :ARG1-of (d2/ do-02
                  :ARG0 p
                  :ARG1-of (w/ wrong-02)
		  :modpred d))
      :aspect Performance
      :modstr FullAff)
  
(s3/ sentence
    :temporal((DCT :before s3d)
              (s3d :before s3d2))
    :modal((AUTH :FullAff s3p)
    	   (s3p :FullAff s3d)
	   (s3d :Unsp s3d2))
    :coref(s2p :same-entity s3p))

```

For this sentence, the coreference annotation indicates that *he* is the same person as *Pope* mentioned in [\[1 (2)\]](#1 (2)). Because there is no strict event coreference or subevent relation between *wrongdoing* and, for example, *spying* in [\[1 (2)\]](#1 (2)), this relation is left unannotated.

The temporal annotation indicates that Pope's denial took place before document creation time, and that any *wrongdoing* would have happened before this denial. When annotating temporal relations, we always need to pick a *reference time* with respect to which the temporal relation between the reference time and the event can be determined. In this case, it is not clear whether the *deny* event happened before or after the *conviction* and *sentence* events, so the reference time is determined to be the document creation time.

The modal relations indicate that the *deny* event definitely happened according to the author. The author presents themselves as having certainty about Pope's mental state at the time of the denial (annotated as a :FullAff relation from AUTH to *Pope*), and the :FullNeg relation indicates that *wrongdoing* did not happen according to Edmund Pope, based on the author's account.

<span id="1 (4)" label="1 (4)">\[1 (4)\]</span>
```
Snt4: Russian President Vladimir Putin pardoned him for health reasons.
(p/ pardon-01
      :ARG0 (p2/ person :wiki "Vladimir_Putin"
            :name (n/ name :op1 "Vladimir" :op2 "Putin")
            :ARG0-of (h/ have-org-role-91
                  :ARG1 (c/ country :wiki "Russia"
                        :name (n2/ name :op1 "Russia"))
                  :ARG2 (p3/ president)))
      :ARG1 (p4/ person
      	    :ref-person 3rd
	    :ref-number Singular)
      :ARG1-of (c2/ cause-01
            :ARG0 (r/ reason
                  :mod (h2/ health)))
      :aspect Performance
      :modstr FullAff)

(s4/ sentence
    :temporal(s2s2 :after s4p)
    :modal (AUTH :FullAff s4p)
    :coref(s3p :same-entity s4p4))
```

In the document-level representation for this sentence, the person that is pardoned by Putin is marked as coreferential with *he* in sentence 3 (and therefore *Edmund Pope*). In the temporal annotation, the *sentence-01* event is designated as the reference time of *pardon-01* - the latter happens after the former. In the modal annotation, *pardon-01* is annotated as certain from the point of view of the author.

<span id="1 (5)" label="1 (5)">\[1 (5)\]</span>
```
Snt5: Pope was flown to the U.S. military base at Ramstein, Germany.
 
(f/ fly-01
      :ARG1 (p/ person :wiki "Edmond_Pope"
            :name (n/ name :op1 "Pope"))
      :goal (b/ base
            :mod (m/ military
            :mod (c/ country :wiki "United_States"
                  :name (n2/ name :op1 "U.S.")))
            :place (c2/ city :wiki "Ramstein_Air_Base"
                  :name (n3/ name :op1 "Ramstein")
                  :place (c3/ country :wiki "Germany"
                        :name (n4/ name :op1 "Germany"))))
      :aspect Performance
      :modstr FullAff)

(s5/ sentence
    :temporal(s4p :after s5f)
    :modal(AUTH :FullAff s5f)
    :coref(s4p4 :same-entity s5p))
```
In the document-level annotation of this sentence, *pardon-01* from [\[1 (4)\]](#1 (4)) is chosen as the
reference time of the *fly-01* event, and it happened before the *fly-01* event. The author is certain that the *fly-01* 
event happened, and *Pope* in this sentence is the same person as *him* in the previous one.

<span id="1 (6)" label="1 (6)">\[1 (6)\]</span>
```
Snt6: He will spend the next several days at the medical center there before he returns home with his wife Sherry

(s/ spend-02
      :ARG0 (p/ person
         :ref-person 3rd
	 :ref-number Singular)
      :ARG1 (t/ temporal-quantity
         :quant (s2/ several)
	 :unit (d/ day
	 	:mod (n/ next)))
      :temporal (b/ before
         :op2 (r/ return-01
	    :ARG1 p
	    :ARG4 (h/ home)
	    :companion (p2/ person :wiki -
	       :name (n2/ name :op1 "Sherry")
	       :ARG0-of (h2/ have-role-91
	          :ARG1 p
		  :ARG2 (w/ wife)))
	    :aspect Performance
	    :modstr FullAff))
      :place (c/ center
          :mod (m/ medical)
	  :place (t2/ there))
      :aspect State
      :modstr FullAff)

(s6/ sentence
  :temporal((DCT :after s6s)
            (s6s :after s6r))
  :modal((AUTH :FullAff s6s)
         (AUTH :FullAff s6r))
  :coref((s5p :same-entity s6p)
         (s5b :same-entity s6t2))
```
In the temporal annotation of this sentence, the DCT is chosen as the reference time for *spend-02*, which is in turn the reference time for *return-01* - *spending time at the medical center* will happen after the DCT, and *returning home* will happen later still. In the modality annotation, both *spend-02* and and *return-01* are presented by the author as certainly happening - or at least as certain as one can be about future events. In the coreference annotation, *he* is considered to be the same as the *person* whose name is Pope in [\[1 (5)\]](#1 (5)), and *there* is the same location as the town of *Ramstein, Germany* in the preceding sentence. 

<span id="1 (7)" label="1 (7)">\[1 (7)\]</span>
 ```
Snt7: Pope was in remission from a rare form of bone cancer when he was arrested in Russia.

(h/ have-mod-91
       :ARG1 (p/ person :wiki "Edmond_Pope"
             :name (n/ name :op1 "Pope"))
       :ARG2 (r/ remission-02
             :ARG1 (d/ disease :wiki -
                   :name (n2/ name :op1 "bone" :op2 "cancer")
                   :ARG1-of (r2/ rare-02))
             :temporal (a/ arrest-01
                   :ARG1 p
                   :place (c/ country :wiki "Russia"
                         :name (n3/ name :op1 "Russia")))
		   :aspect Performance
		   :modstr FullAff)
	:aspect State
	:modstr FullAff)

(s7/ sentence
  :temporal((s2c :before s7a)
            (s7a :overlap s7h))
  :modal ((AUTH :FullAff s7h)
         (AUTH :FullAff s7a))
  :coref (s6p :same-entity s7p))
```
For [\[1 (7)\]](#1 (7)), the state of being in *remission-02* held simultaneously with the *arrest-01* event, and the *arrest-01* event happended before the *convict-01* event from sentence 2. According to the author, both *arrest-01* and *be in remission* happened. Once again, *Pope* is the same entity as *he* in the previous sentence.

<span id="1 (8)" label="1 (8)">\[1 (8)\]</span>
```
Snt8: Doctors will examine him for signs that the cancer may have come back while he was awaiting trial in a Russian jail.

 (e/ examine-01
       :ARG0 (d/ doctor
          :ref-number Plural)
       :ARG1 (p/ person
          :ref-person 3rd
	  :ref-number Singular)
       :ARG2 (s/ signal-07
          :ARG1 (c/ come-01
	     :ARG1 (d2/ disease :wiki "Cancer"
	        :name (n/ name :op1 "cancer))
	     :direction (b/ back)
	     :temporal (a/ await-01
	        :ARG1 p
		:ARG2 (t/ try-02
		   :ARG1 p
		   :aspect Process)
		:place (j/ jail
		   :mod (c2/ country :wiki "Russia
		      :name (n2/ name :op1 "Russia")))
		:aspect State
		:modstr FullAff)
	     :aspect Performance
	     :modstr NeutAff)
	  :ARG2 d)
	:aspect Endeavor
	:modstr FullAff)
  
(s8/ sentence
  :temporal((DCT :after s8e)
  	    (s2c :before s8a)
	    (s8a :overlap s8c))
  :modal ((AUTH :FullAff s8e)
          (AUTH :NeutAff s8c)
          (AUTH :FullAff s8a))
  :coref(s7p :same-entity s8p)) 
```

The *examine-01* event will happen after the DCT. The *await-01* event happened before the *conviction* event mentioned earlier in the text, and the potential return of the cancer temporally overlaps with this *await-01* event. According to the author, the *examine-01* event will certainly happen, and the *await-01* event certainly happened as well. The author is uncertain about whether the cancer has come back, indicated with a *NeutAff* epistemic strength link. *He* is annotated as being the same person as Edmund Pope.

<span id="1 (9)" label="1 (9)">\[1 (9)\]</span>
```
Snt9:  A spokeswoman said that Pope was suffering from malnutrition and high blood pressure.
(s/ say-01
      :ARG0 (p/ person
            :ARG0-of (h/ have-org-role-91
                  :ARG2 (s2/ spokeswoman))
	    :ref-number Singular)
      :ARG1 (s3/ suffer-01
            :ARG0 (p2/ person :wiki "Edmond_Pope"
	          :name (n/ name :op1 "Pope"))
            :ARG1 (a/ and
                  :op1 (m/ malnourished-01
                        :ARG1 p2)
                  :op2 (p3/ pressure-01
                        :ARG1 (b/ blood
			   :part-of p2)
                        :ARG1-of (h2/ high-02)))
	    :aspect State
	    :modstr FullAff)
      :aspect Performance
      :modstr FullAff)
      
(s9/ sentence
 :temporal ((DCT :before s9s)
            (s9s :overlap s9s3))
 :modal ((AUTH :AFF s9s)
         (AUTH :AFF s9p)
	 (s9p :AFF s9s3))
 :coref (s8p :same-entity s9p2))
 ```
The document-level representation indicates the *say-01* event happened before Document Creation Time, and that the *suffer-01* event overlaps temporally with the *say-01* event. The modality annotation indicates that from the author's perspective, the *say-01* event definitely happened, and the author indicates that the *suffer-01* event happened according to the spokesperson. Once again, coreference is indicated between different mentions of *Pope*.  

[Back to Table of Contents](#toc)

##  Part 2. From AMR to UMR

### Part 2-1. Introduction

UMR inherits the sentence-level representation of AMR, with modifications. Like AMR, the sentence-level representation of UMR is a single-rooted, directed, node- and edge-labeled graph, as in [\[2 (1)\]](#2 (1)). The nodes of this graph are UMR concepts, while edges represent UMR relations. 

<span id="2 (1)" label="2 (1)">\[2 (1)\]</span>
```
Snt1: Edmund Pope tasted freedom today for the first time in more than eight months.

(t/ taste-01
  :ARG0 (p/ person :wiki "Edmond_Pope"
         :name (n/ name :op1 "Edmund" :op2 "Pope"))
  :ARG1 (f/ free-04
         :ARG1 p)
  :temporal (t2/ today)
  :ord (o/ ordinal-entity :value 1
        :range (m/ more-than
                :op1 (t3/ temporal-quantity :quant 8
                    :unit (m2/ month))))
  :aspect Performance
  :modstr FullAff)
```

**UMR concepts:** There are a number of ways that UMR concepts are created based on the input sentence:

* Lemmas: Some UMR concepts are simply lemmas. For example, `today` in the example above is a lemma, which happens to have the same form as the word token itself.
* Word senses: When definitions of word senses are available for a language in the form of a lexicon, a concept can also be a sense-disambiguated word. For instance, `taste-01` in the example above refers to the first sense of the word *taste* in the English PropBank.
* Concepts formed out of multi-word expressions: `more-than` is a concept that is formed by concatenating multiple words in a sentence. Exactly when multi-word concepts should be formed will be determined on a language-by-language basis.
* Named entity types. Named entities in a sentence are annotated with a named entity type concept (e.g., `person`) and a `name` concept. The actual names are annotated as a constant (`Edmund` and `Pope`).
* Abstract concepts. In some cases a concept can be inferred from the context. In this case, the concept does not correspond to any particular word in the sentence, hence it is an *abstract* concept (e.g. `ordinal-entity`).

**UMR relations:** There are also a number of ways relations between concepts are created:

* Participant roles: The participant roles characterize the role that a participant plays with respect to the predicate. They can be predicate-specific if a set of *frame files* are defined for a language, where a set of core participant roles are defined for each (sense of the) predicate. For example, `:ARG0` and `:ARG1` are participant roles defined for `taste-01`. For languages that do not have *frame files*, the participant roles are generic (e.g., `Actor`, `Experiencer`), and they are described in [Part 3-2-1](#part-3-2-1-participant-roles).
* Semantic relations: Other UMR relations include `:temporal`, `:ord`, `:range` etc. that are not normally characterized as participant roles. A complete list of such relations can be found in [Part 3-2-2](#part-3-2-2-Non-participant-role-UMR-relations).

**UMR attributes:** UMR currently has seven attribute types:

* Aspect: Aspect is annotated for eventive concepts only (see
[Part 3-1-1](#part-3-1-1-eventive-concepts) on event identification). Possible Aspect values at the default level of granularity include `Activity`, `Habitual`, `State`, `Endeavor`, `Performance`. A complete list of aspect values with explanations and examples can be found in [Part 3-3-1](#part-3-3-1-aspect). 
* Polarity: Polarity is only annotated for negative polarity as indicated by a negation marker or an affix indicating negation (see [Part 3-3-3](#part-3-3-3-polarity)).
* Mode: The mode attribute is typically for the main predicate of a sentence. Its values include `imperative`, `expressive`, and `interrogative` (see [Part 3-3-2](#part-3-3-2-mode)).
* Quantity: The value of a `:quant` attribute is a numerical number (see [Part 3-3-4](#part-3-3-4-quant)).
* Value: The value of a `:value` attribute is a numerical number (see [Part 3-2-2](#part-3-2-2-Non-participant-role-UMR-relations)).
* Degree: The value of a `:degree` attribute is either `intensifier`, `downtoner`, or `equal` (see [Part 3-3-6](#part-3-3-6-degree)).
* Reference: The value of a `:ref-person` or `:ref-number` attribute is a either a person feature (e.g. `1st`, `2nd`, `3rd`) or a number feature (e.g. `Singular`, `Dual`, `Paucal`, `Plural`) used to represent reference. These features are used to represent pronouns, verbal cross-referencing, implicit arguments, and overt nominal number (see [Part 3-3-5](#part-3-3-5-ref)).

**UMR modal values:** UMR currently has three modal relations that are annotated at the sentence level, even though the final modal dependency structure functions at the document level:

* Modstr: Indicates the epistemic strength relation (degree of confidence/certainty) between a conceiver and an event or between a conceiver and an embedded conceiver.
* Modpred: Indicates the relation between a modal complement-taking predicate and its complement
* Quot: Indicates the relation between a speech predicate and its complement

**Differences between AMR and UMR**

UMR differs from AMR in a number of ways:

* UMR has a document-level representation that represents *coreference*, *temporal dependencies*, and *modal dependencies*.

* As a result, some sentence-level AMR concepts  are now represented at the document level. This applies to concepts for modality (e.g., `possible-01`, `obligate-01`) - see the AMR and the UMR for *The boy can go* in [\[2 (2a)\]](#2 (2a)) and [\[2 (2b)\]](#2 (2b)), respectively.

<span id="2 (2a)" label="2 (2a)">\[2 (2a)\]</span>

```
(p/ possible-01
   :ARG0 (g/ go-01  
            :ARG0 (b/ boy
	       :ref-number Singular)))
```
<span id="2 (2b)" label="2 (2b)">\[2 (2b)\]</span>
```
(g/ go-01  
    :ARG0 (b/ boy
    	:ref-number Singular)
    :aspect State
    :modstr NeutAff)

(s0/sentence
  :modal (AUTH :NEUT s0g))
  
```

* UMR adds a *scope* concept to represent the relative scope of quantifiers and negations. See [Part-3-1-5](#part-3-1-5-scope-for-quantification-and-negation) for details.
* UMR allows the use of non-predicate-specific participant roles for languages that do not have *frame files* with lexicalized argument structure information. See [Part 3-2-1](#part-3-2-1-participant-roles) for details. To further accomodate languages with less advanced grammatical description or resource availability, other annotation domains are structured as *lattices*.
* UMR adds *aspect* and *ref* attributes to the representation. See [Part 3-3-1](#part-3-3-1-aspect) and [Part 3-3-5](#part-3-3-5-ref) for details.

[Back to Table of Contents](#toc)

### Part 2-2. Introduction for field linguists

The annotation scheme detailed in these guidelines, Uniform Meaning
Representation (UMR), intends to allow for annotation of temporal,
aspectual, modal, and quantification semantics, as well as semantic
argument structure, in a cross-linguistically motivated and portable
way. Some semantic domains, specifically coreference, temporal
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
roles and a range of different modification relations, amongst others.

[Back to Table of Contents](#toc)

#### Part 2-2-1. Predicate-argument relations

The annotation of predicate-argument structure is the main domain in
which AMR annotation conventions are inherited. First and foremost,
predicated events are represented in the graph as nodes, as are
predicated states, events that are being referred to or used as
modifiers, and various other kinds of "non-verbal predicates" (see
[Part 3-1-1](#part-3-1-1-eventive-concepts) on event identification). For annotation of English texts,
sense-disambiguated predicates from PropBank, such as the one presented below for English _taste_ are used to label predicate
nodes. Since for most languages, no equivalent of PropBank is available, the UMR annotation tool contains a lexicon-building functionality where annotators can either upload a lexicon created in FLEx to support them in their annotation effort, or they can start a lexicon with argument structure information from scratch and essentially build PropBank-style frame files on the fly.

```
Roleset id: taste.01, use one's tastebuds, active perception of flavor.
Roles:
	ARG0: taster
	ARG1: food
	
Roleset id: taste.02, possess a flavor.
Roles
	ARG1: thing with flavor
	ARG2: description of flavor
```

The semantic arguments of such predicate nodes are represented in the
graph as daughter nodes of the relevant predicate. The edge that connects parent and daughter
nodes in these structures carries a participant role label. For English,
these participant role labels are predicate-specific, numbered argument
roles drawn once again from PropBank. For languages without comparable
lexical databases, we use an inventory of general argument roles such as
`:actor`, `:undergoer`, and `:theme`. In the long run, annotations can be used to
create language-specific and predicate-specific frame files detailing
argument structure of individual predicates, and the predicate-specific
argument roles can be linked to predicate-general participant roles for
commensurability (see [Part 3-2-1](#part-3-2-1-participant-roles) on argument structure annotation).
This AMR-based predicate-argument annotation is shown in its most basic
form in [\[2-2-1 (1)\]](#2-2-1 (1)) from Sanapaná (Enlhet-Enenlhet) below.

<span id="2-2-1 (1)" label="2-2-1 (1)">\[2-2-1 (1)\]</span>
```
ap-hle-am-ke'		nenhlet
2/3M-travel-TI-DECL	person
'A man travelled.'

(e/ enhleama-00 'travel'
	:actor (n/ nenhlet 'person'
		:ref-number Singular)
	:aspect Endeavor
	:modstr FullAff)
(t/ travel-01
	:ARG0 (m/ man
		:ref-number Singular)
	:aspect Endeavor
	:modstr FullAff)
```

The basic, AMR-inspired graph structures for simple sentences in
languages like English and Sanapaná then look very similar, as shown
above: they both have a predicate corresponding to the main event of the
sentence as the top of the graph - the English one has a reference to a
numbered PropBank frame file for the predicate *travel*, the Sanapaná
one just has the citation form of the *travel*-verb with a `-00` suffix.
In both cases, the semantic argument 'person/man' is a daughter of this
predicate, linked with a participant role edge. In English, this is a
numbered participant role taken from this same PropBank frame file,
while in Sanapaná it is a predicate-general participant role. In both languages, the participant has a :ref-number Singular attribute.

AMR and UMR concepts are underspecified for morphosyntactic
representation: the same concept (for example, `travel-01`) can be used
to annotate a verb (as seen above), a noun (e.g. *his travels* in [\[2-2-1 (2)\]](#2-2-1 (2))), or any other relevant part of speech conveying the same semantics. [Part 3-1-1](#part-3-1-1-eventive-concepts) discusses how AMR and UMR deal with the
information-packaging differences which are conveyed by packaging such
content in different parts of speech.

<span id="2-2-1 (2)" label="2-2-1 (2)">\[2-2-1 (2)\]</span>
```
I heard about his travels.
(h/ hear-01
	:ARG0 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:ARG1 (t/ travel-01
		:ARG0 (p2/ person
			:ref-person 3rd
			:ref-number Singular)
		:aspect Process
		:modstr FullAff)
	:aspect State
	:modstr FullAff)
```
[Back to Table of Contents](#toc)

#### Part 2-2-2. Multi-word expressions

UMR inherits annotation conventions from AMR in domains other than
predicate-argument structure. With regard to concepts, UMR treats
multi-word expressions in essentially the same way as AMR. Specifically,
it allows annotators to select multiple words in a sentence and annotate
them as a single concept. This is necessary, for example, to annotate
idiomatic expressions which cannot be semantically decomposed
felicitously. In [\[2-2-2 (1)\]](#2-2-2 (1)) from Sanapaná, for instance,
*elvongkeskama tayep* is a multi-word expression which literally and
compositionally means 'cause (someone) to be just across', but its
idiomatic meaning is 'rescue'. The two words are therefore annotated
together as a multi-word expression with a single meaning. Some further
specifications are made in UMR with regards to the annotation of
multi-word expressions such as serial verb constructions and
periphrastic TAM constructions. More information about the annotation of
multi-word expressions is given throughout [Part 3-1-3](#part-3-1-3-concept-word-mismatches), and
specifically in section [Part 3-1-3-6](#part-3-1-3-6-multi-word-concepts).

<span id="2-2-2 (1)" label="2-2-2 (1)">\[2-2-2 (1)\]</span>
```
apk-el-vongk-es-akp-e'		tayep	ayko<'o>k
2/3M-DSTR-be.just-CAUS-PAS-DECL	across	child<PL>
'The children were rescued.'
(e/ elvongkeskama-tayep-00 'rescue'
	:Undergoer (a/ ayko'ok 'child'
		:ref-number Plural)
	:aspect Performance
	:modstr FullAff)
```
[Back to Table of Contents](#toc)

#### Part 2-2-3. Abstract concepts

AMR conventions are also largely inherited with regards to the use of
abstract concepts. Abstract concepts are concepts that are identified
and annotated even though they do not (consistently) correspond to any
overt word in the sentence. There are typically two main reasons for
which AMR and UMR use abstract concepts. Firstly, there are concepts
where AMR and UMR use abstract concepts rather than language-specific
concepts corresponding to specific words with the goal of making
annotations cross-linguistically comparable. For example, even though
the Sanapaná thetic possession construction in [\[2-2-3 (1)\]](#2-2-3 (1)) makes use of a verb
that literally means *exist*, an abstract concept predicate node
`have-91` is introduced rather than a language specific `enyetnema-00`
concept. This way, possessive constructions across the world's languages
can be annotated in consistent and comparable ways regardless of the
morphosyntactic strategies they use (see [Part 3-1-3-5](#Part-3-1-3-5-Non-verbal-clauses) for more
information on such "non-verbal clauses").

<span id="2-2-3 (1)" label="2-2-3 (1)">\[2-2-3 (1)\]</span>
```
an-yetn-eye'		ko'o	vakka-hak	ah-angkok
2/3F-exist-DECL		1SG:PRO	cow-old		1SG-POS
'I have a book.' lit. 'My book exists.'
(h/ have-91
	:ARG0 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:ARG1 (v/ vakkahak 'book')
	:aspect State
	:modstr FullAff)
```

Secondly, abstract concept conventions are inherited from AMR in a
variety of domains where information expressed in natural language text
needs to be standardized for computational tractability. This applies
to, for example, the annotation of different types of quantities (which
use abstract concepts such as `distance-quantity`,
`temporal-quantity` and `monetary-quantity`, as
illustrated in [\[2-2-3 (2a)\]](#2-2-3 (2a))-[\[2-2-3 (2b)\]](#2-2-3 (2b))), and the annotation of dates and times (which use abstract concepts such as `date-entity`, as illustrated in [\[2-2-3 (2c)\]](#2-2-3 (2c)), all from Sanapaná). More information on abstract concepts can be found throughout this document in the sections dedicated to the specific semantic phenomena for which they are needed.

<span id="2-2-3 (2)" label="2-2-3 (2)">\[2-2-3 (2)\]</span>

<span id="2-2-3 (2a)" label="2-2-3 (2a)">\[2-2-3 (2a)\]</span>
```
cinco,	seis	meses	apk-ehl-ta'mehl-kes-kam-a
five	six	months	2/3M-DSTR-be.good-CAUS-TI-NOM
'They would preserve it for five or six months.'
(e/ enta'mehlkeskama-00 'preserve'
	:actor (p/ person
		:ref-person 3rd
		:ref-number Plural)
	:undergoer (t/ thing)
	:duration (o/ or
		:op1 (t2/ temporal-quantity
			:quant 5
			:unit (m/ mes 'month'))
		:op2 (t3/ temporal-quantity
			:quant 6
			:unit (m/ mes 'month')))
	:aspect Habitual
	:modstr FullAff)
```
<span id="2-2-3 (2b)" label="2-2-3 (2b)">\[2-2-3 (2b)\]</span>
```
escuela	agrícola	seis	millón	cada	año	on-yanmong-kes-ek
school	agricultural	six	million	each	year	1PL.IRR-exchange-CAUS-FUT
'For the agricultural school, we would pay six million (guaranies) per year.'
(e/ enyanmongkeskama-00 'pay'
	:actor (p/ person
		:ref-person 1st
		:ref-number Plural)
	:recipient (e2/ escuela 'school'
		:mod (a/ agrícola 'agricultural'))
	:theme (m/ monetary-quantity
		:quant 6,000,000
		:unit (g/ guaraní
			:mod (c/ country
				:wiki "Paraguay"
				:name (n/ name :op1 "Paraguay"))))
	:frequency (r/ rate-entity
		:ARG1 1
		:ARG2 (t/ temporal-quantity
			:quant 1
			:unit (a2/ año 'year)))
	:aspect Habitual
	:modstr FullAff)
```
<span id="2-2-3 (2c)" label="2-2-3 (2c)">\[2-2-3 (2c)\]</span>
```
apk-el-v-ayk-akh-a'		Venancio	el-eyv-om-akha'		mil		novecientos	sesenta	y	seis=anehla
2/3M-DSTR-arrive-TI-DUPL-NOM	Venancio	1PL-live-TI-NOM.LOC	thousand	nine-hundred	sixty	and	six=DUB
'Venancio and his companions arrived where we lived in ninteen sixty-six, maybe.'
(e/ elvay'a-00 'arrive'
	:actor (p/ person
		:name (n/ name :op1 "Venancio")
	:companion (p2/ person))
	:goal (p3/ place
		:place-of (e2/ eleyvoma-00 'live'
			:actor (p4/ person
				:ref-person 1st
				:ref-number Plural)))
	:temporal (d/ date-entity
		:year 1966)
	:aspect Performance
	:modstr NeutAff)
```
[Back to Table of Contents](#toc)

#### Part 2-2-4. Non-participant role relations

Another domain in which AMR conventions are inherited by UMR is the
annotation of non-participant role relations. Such relations are used to
annotate a wide range of meanings. Many of them, such as `:medium`,
`:topic`, and `:mod` (the latter of which is illustrated in [\[2-2-3 (2b)\]](#2-2-3 (2b))) are used to
annotate modifiers of referring expressions. Other relations are used
with specific abstract concepts: whenever a `date-entity`
concept is present, one of the temporal relations `:month`, `:year`, `:day`
etc. will be used, for example. The use of these relations is treated
more in detail in [Part 3-2-2](#part-3-2-2-Non-participant-role-UMR-relations) of this document.

Even though many of these relations are straightforwardly inherited by
UMR, some changes are made to their use for the sake of cross-linguistic
comparability. Firstly, UMR adjusts the use of the `:mod` relation to
cover all *typifying* modifiers - i.e. modifiers which subcategorize the
reference of a referring expression rather than narrowing it down to a
specific entity (e.g. *women* in *women's magazine*). In AMR, this
semantic domain was shared between the `:mod` relation and a number of
other relations such as `:medium`, `:topic`, and `:consist-of`. In UMR, these
other relations still exist, but they are treated as more fine-grained
values on a lattice underneath the more general `:mod` relation. Whereas
AMR used the `:frequency` and `:duration` relations as the main ways of
annotating aspect, UMR does this through a dedicated `:aspect` attribute.
However, UMR maintains the `:duration` and `:frequency` relations so that
annotators can use them to indicate more fine-grained aspectual
information beyond the aspect categories offered in the corresponding
attribute, as in [\[2-2-3 (2b)\]](#2-2-3 (2b)). UMR also adds a new non-participant role relation: the `:other` relation, which annotators can use when encountering meanings that UMR currently does not provide a straightforward annotation procedure for.

[Back to Table of Contents](#toc)

#### Part 2-2-5. Attributes

The last area in which AMR conventions are inherited by UMR is that of
*attribute* annotations. Attributes are relations which attach one of a
closed, pre-defined list of values to a concept node: for example, the
`:aspect` attribute allows annotators to hang a `State`, `Habitual`,
`Activity`, `Endeavor`, or `Performance` value off
of a predicate node.

Attributes inherited from AMR are `:polarity`, `:mode`,
`:quant`, and `:value` ([Part 3-2-2](#part-3-2-2-Non-participant-role-UMR-relations), [Part 3-3](#part-3-3-UMR-attributes)). The use
of the `:quant` relation was changed in that a more fine-grained
annotation scheme for quantification is now available (see [Part 3-1-5](#part-3-1-5-scope-for-quantification-and-negation), [Part 3-3-4](#part-3-3-4-quant)). The `:quant` relation is mainly what annotators with
less training or for languages with less available linguistic analysis
will use to flag concepts that are of interest with regards to
quantification. More confident annotators
and annotators for well-documented languages will apply the full
fine-grained quantification and scope scheme. One
specific change is that, whereas in mensural constructions (e.g. *three
cups of milk*), AMR varies between having the substance or the mensural
term as the head depending on morphosyntactic expression, UMR always
annotates the substance as the head for greater cross-linguistic
comparability. This means that even less conventionalized measure terms,
like English *cup* or *bag*, are annotated as modifiers, even though
they look like morphosyntactic heads. This is illustrated in [\[2-2-5 (1)\]](#2-2-5 (1)). The use of the `:polarity` value is constrained to the sentence level.
Propositional negation is annotated in the modal section of the document
level annotation and through :modstr relations. The `:polarity` value is used to indicate any overt
morphosyntactic exponents of negation at the sentence level, flagging
such concepts as interesting for the modal or scope negation. This
includes e.g. morphologically negated adjectives like _unhappy_, even though in the
document-level modal annotation, these will not be annotated as negated.

<span id="2-2-5 (1)" label="2-2-5 (1)">\[2-2-5 (1)\]</span>
```
Three bottles of water
(w/ water
	:quant 3
	:unit (b/ bottle))
```

UMR introduces four new attributes: `:aspect` (see [Part 3-3-1](#part-3-3-1-Aspect)), `:degree` (see [Part 3-3-6](#part-3-3-6-degree)), and
`:ref-person` and `:ref-number` (see [Part 3-3-5](#part-3-3-5-ref)).

[Back to Table of Contents](#toc)

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
predication. Croft (to appear)  defines them as:

**reference**: what the speaker is talking about  
**modification**: additional information provided about the referent  
**predication**: what the speaker is asserting about the referents in a particular utterance

The three semantic types can occur with any of the three fundamental
information packaging functions, as shown in Table
1 from Croft (in preparation).


<div id="tab:information_packaging">

|           |              Reference               |           Modification           |         Predication         |
| :-------: | :----------------------------------: | :------------------------------: | :-------------------------: |
| Entities  |         the sharp **thorns**         |      the **bush’s** thorns       |     It **is a thorn.**      |
|  States   |            **sharpness**             |       the **sharp** thorns       | Those thorns **are sharp.** |
|     Processes      |     I said \[**that** the thorns **scratched** me\]. / <br />      the \[**scratching** of the thorns\]    |       the thorns **that** \[**scratched** me\] / <br /> the thorns \[**scratching** me\]        |      The sharp thorns **scratched** me.      |

Table 1: Semantic types expressed in different information packaging constructions
</div>

Cross-linguistically, certain types of morphosyntactic constructions
tend to express specific combinations of semantic type and information
packaging; these are shown in Table 2,
modified from Croft (2001). Prototypical combinations of semantic type and
information packaging are indicated with caps. These correspond to
well-known part-of-speech classes across languages: entities in
reference correspond to nouns, states in modification to adjectives, and
processes in predication to verbs.

<div id="tab:eventive_concepts">
	
|               |                   Reference                   |                    Modification                    |                  **Predication**                  |
| :-----------: | :-------------------------------------------: | :------------------------------------------------: | :-----------------------------------------------: |
|   Entities    | UNMARKED NOUNS |                 relative clauses, PPs on nouns                  |              **predicate nominals,** **complements**             |
|    States     |              deadjectival nouns               | UNMARKED ADJECTIVES |             **predicate adjectives,** **complements**           |
| **Processes** |       **event nominals, complements,** **infinitives, gerunds**        |         **participles, relative clauses**          | **UNMARKED VERBS** |

Table 2: Constructions identified as events
</div>

The most prototypical expression for an event is a process in
predication, therefore we identify a word/phrase as an event if it has
either the semantic type of the prototype (process) or the prototypical
information packaging (predication). The categories which are identified
as events in UMR are shown in bold in Table 2.

[Back to Table of Contents](#toc)

##### Part 3-1-1-1. Processes in predication

Predicated processes are the most prototypical subcategory of events,
corresponding cross-linguistically to unmarked verbs. They will
therefore always be identified as events. This is shown in
[\[3-1-1-1 (1)\]](#3-1-1-1 (1)) below. (Throughout this section, words
that are identified as events will be shown in bold; the relevant
phenomenon under discussion will be italicized.)

<span id="3-1-1-1 (1)" label="3-1-1-1 (1)">\[3-1-1-1 (1)\]</span>

<span id="3-1-1-1 (1a)" label="3-1-1-1 (1a)">\[3-1-1-1 (1a)\]</span> She
<u>**_repaired_**</u> her bike.  
<span id="3-1-1-1 (1b)" label="3-1-1-1 (1b)">\[3-1-1-1 (1b)\]</span> Before
she <u>**_went_**</u> to school, she **repaired** my bike.  

Regardless of whether they are in an independent clause, like *repaired*
in [\[3-1-1-1 (1a)\]](#3-1-1-1 (1a)), or a dependent clause, like *went* in
[\[3-1-1-1 (1b)\]](#3-1-1-1 (1b)), predicated processes are always
identified as events.

[Back to Table of Contents](#toc)

##### Part 3-1-1-2. Processes in modification and reference

Processes packaged as modifiers or referents should also be identified
as events. Cross-linguistically, these may take a variety of
morphosyntactic forms, such as event nominals (as in
[\[3-1-1-2 (1a)\]](#3-1-1-2 (1a))), non-finite complements (as in
[\[3-1-1-2 (1b)\]](#3-1-1-2 (1b))), participles (as in
[\[3-1-1-2 (1c)\]](#3-1-1-2 (1c))), or relative clauses (as in
[\[3-1-1-2 (1d)\]](#3-1-1-2 (1d))).

<span id="3-1-1-2 (1)" label="3-1-1-2 (1)">\[3-1-1-2 (1)\]</span>

<span id="3-1-1-2 (1a)" label="3-1-1-2 (1a)">\[3-1-1-2 (1a)\]</span> The
**<u>_storm_</u> damaged** the roads.

<span id="3-1-1-2 (1b)" label="3-1-1-2 (1b)">\[3-1-1-2 (1b)\]</span> She
**wanted <u>_to go_</u>** to school.

<span id="3-1-1-2 (1c)" label="3-1-1-2 (1c)">\[3-1-1-2 (1c)\]</span> The
student **<u>_playing_</u>** the violin **likes** Bach.

<span id="3-1-1-2 (1d)" label="3-1-1-2 (1d)">\[3-1-1-2 (1d)\]</span> The student,
who is **<u>_playing_</u>** the violin, **likes** Bach.

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
**planning** a **<u>_ceremony_</u>** for Saturday.

<span id="3-1-1-2 (2b)" label="3-1-1-2 (2b)">\[3-1-1-2 (2b)\]</span>
The bus <u>_driver_</u> **turned** the corner too sharply.

Even the same lexical item may or may not refer to a process, depending
on context as in ([\[3-1-1-2 (3)\]](#3-1-1-2 (3))) below.

<span id="3-1-1-2 (3)" label="3-1-1-2 (3)">\[3-1-1-2 (3)\]</span>

<span id="3-1-1-2 (3a)" label="3-1-1-2 (3a)">\[3-1-1-2 (3a)\]</span>

The <u>**_final exam_**</u> began at 8:00.

<span id="3-1-1-2 (3b)" label="3-1-1-2 (3b)">\[3-1-1-2 (3b)\]</span>

One student **threw** their <u>_final exam_</u> in the trash.

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

[Back to Table of Contents](#toc)

##### Part 3-1-1-3. States and entities

As mentioned above, anything that is predicated is identified as an
event, even if it is not a process. Two-place statives, such as *love*
in [\[3-1-1-3 (1)\]](#3-1-1-3 (1)), are annotated in the same way as predicated
processes, i.e. an event is identified and labelled with the predicate
in the language.

<span id="3-1-1-3 (1)" label="3-1-1-3 (1)">\[3-1-1-3 (1)\]</span>

My cat <u>**_loves_**</u> wet food.

Other types of predicated states and entities require different
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

Table 3: Non-verbal clause types
</div>

There are four semantic types of nonverbal clauses: possession,
location, property, and object. All of these occur with predicational
information-packaging: the possessive relationship, location, property,
or object category are predicated of the possession or theme. Possession and location are, in addition, used in a context in which the entire information is presented as ‘thetic’ or ‘all-new’ in the terms of
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
with a special abstract UMR predicate that indicates the relevant combination of
semantics and information-packaging. These are shown below in Table 4. Note that some of these (e.g. `have-91`, `belong-91`) look very similar to existing English PropBank predicates (`have-03` and `belong-01`, respectively). However, they are cross-linguistic abstract concepts meant to annotate the crosslinguistically stable meanings of thetic possession and predicative possession, respectively. For the labelling of participants with these
nonverbal clause predicates, see [Part 3-2-1-1-1](#part-3-2-1-1-1-nonverbal-clauses).

<div id="tab:nonverbalpreds">

| **Clause type**                  | **UMR Predicate** |
| :------------------------------- | :---------------- |
| thetic/presentational possession | have-91           |
| predicative possession           | belong-91         |
| thetic/presentational location   | exist-91          |
| predicative location             | have-location-91  |
| property predication             | have-mod-91       |
| object predication               | have-role-91      |
| 			           | (subtypes: kinship-91; have-org-role-91) |
| equational                       | identity-91       |

Table 4: Non-verbal clause predicates
</div>

States in modification, as in [\[3-1-1-3 (2a)\]](#3-1-1-3 (2a)) and
[\[3-1-1-3 (2b)\]](#3-1-1-3 (2b)), and states in reference, as in
[\[3-1-1-3 (2c)\]](#3-1-1-3 (2c)), are not identified as events.

<span id="3-1-1-3 (2)" label="3-1-1-3 (2)">\[3-1-1-3 (2)\]</span>

<span id="3-1-1-3 (2a)" label="3-1-1-3 (2a)">\[3-1-1-3 (2a)\]</span> The
<u>_tall_</u> man...

<span id="3-1-1-3 (2b)" label="3-1-1-3 (2b)">\[3-1-1-3 (2b)\]</span> The man,
<u>_who is tall_</u>...

<span id="3-1-1-3 (2c)" label="3-1-1-3 (2c)">\[3-1-1-3 (2c)\]</span> His
<u>_happiness_</u>...

Similarly, entities in modification, as in [\[3-1-1-3 (3a)\]](#3-1-1-3 (3a)),
and entities in reference, as in [\[3-1-1-3 (3b)\]](#3-1-1-3 (3b)), are not
identified as events.

<span id="3-1-1-3 (3)" label="3-1-1-3 (3)">\[3-1-1-3 (3)\]</span>

<span id="3-1-1-3 (3a)" label="3-1-1-3 (3a)">\[3-1-1-3 (3a)\]</span> The man,
<u>_who is a doctor_</u>...

<span id="3-1-1-3 (3b)" label="3-1-1-3 (3b)">\[3-1-1-3 (3b)\]</span> The
<u>_doctor_</u>

Causal relationships follow the same rules as states and entities. They
are identified as events when they are predicated, as in
[\[3-1-1-3 (4a)\]](#3-1-1-3 (4a)), but they are not identified as events
otherwise, like in [\[3-1-1-3 (4b)\]](#3-1-1-3 (4b)).

<span id="3-1-1-3 (4)" label="3-1-1-3 (4)">\[3-1-1-3 (4)\]</span>

<span id="3-1-1-3 (4a)" label="3-1-1-3 (4a)">\[3-1-1-3 (4a)\]</span> The
**explosion <u>_caused_</u>** the house **to collapse**.

<span id="3-1-1-3 (4b)" label="3-1-1-3 (4b)">\[3-1-1-3 (4b)\]</span> The house
**collapsed** <u>_because_</u> of the **explosion**.

[Back to Table of Contents](#toc)

##### Part 3-1-1-4. Implicit events

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
**\[_smoking_\]**</u>.

<span id="3-1-1-4 (1b)" label="3-1-1-4 (1b)">\[3-1-1-4 (1b)\]</span> They **told** me “a card
was **left** on Tuesday” (no it wasn’t <u>**\[_left_\]**</u> of
course)...

In [\[3-1-1-4 (1a)\]](#3-1-1-4 (1a)), there is an implicit second *smoking* event and
in [\[3-1-1-4 (1b)\]](#3-1-1-4 (1b)), there is an implicit second *leave* event. These
implicit events should be annotated as coreferential with the event
mentioned earlier in the text (see [Part 4-1](#part-4-1-coreference)).

In [\[3-1-1-4 (2)\]](#3-1-1-4 (2)), however, the implicit events don’t
have a relationship with an event previously mentioned in the text;
instead, they refer to generic events which can be filled in from
context.

<span id="3-1-1-4 (2)" label="3-1-1-4 (2)">\[3-1-1-4 (2)\]</span>

<span id="3-1-1-4 (2a)" label="3-1-1-4 (2a)">\[3-1-1-4 (2a)\]</span> **Phoned** Amtrak on
Wednesday, <u>**\[_they said_\]**</u> “We **need** a consignment
number”.

<span id="3-1-1-4 (2b)" label="3-1-1-4 (2b)">\[3-1-1-4 (2b)\]</span> “I have **ordered** the Coast
Guard and our entire naval force in the (Central Philippines) region
<u>**\[_to go_\]**</u> to the area,” she **said**.

In [\[3-1-1-4 (2a)\]](#3-1-1-4 (2a)), the quotation marks make it clear that there is an
implicit *say* event. In [\[3-1-1-4 (2b)\]](#3-1-1-4 (2b)), we can identify a very general
*go* event, since *ordered...to the area* implies a motion event. For
these types of implicit events, the most abstract, least specific event
should be identified. For example in [\[3-1-1-4 (2b)\]](#3-1-1-4 (2b)), we could make an
assumption based on context clues (e.g., *Coast Guard, naval force*),
that the type of motion event is *sail*. But, that assumption may not be
accurate (and may not be shared amongst annotators); therefore, the most
general event possible should be identified.


[Back to Table of Contents](#toc)

 #### Part 3-1-2. Named entities
 
Following AMR, each named entity in a text is annotated with a type. However, the vocabuary of the named entity types are adapted from AMR so that they reflect the characterization of additional languages and thus made uniform across languages. Example [\[3-1-2 (1)\]](#[3-1-2 (1)) has a `nationality` entity and a `person` entity. 

<span id="3-1-2 (1)" label="3-1-2 (1)">\[3-1-2 (1)\]</span> Edmond Pope is an American businessman.
```
(h/ have-role-91
      :ARG0 (p/ person :wiki "Edmond_Pope"
            :name (n/ name :op1 "Edmund" :op2 "Pope"))
      :ARG2 (b/ businessman
      	    :mod (n2/ nationality :wiki "United_States"
	          :name (n3/ name :op1 "America")))
      :aspect State
      :modstr FullAff)         
```        
The total set of entity types are hierarchically organized, as listed in Table 5 below.



<!--organization, company, government-organization, military, criminal-organization, political-party, market-sector, school, university, research-institute, team, league-->
<!--location, city, city-district, county, state, province, territory, country, local-region, country-region, world-region, continent; ocean, sea, lake, river, gulf, bay, strait, canal; peninsula, mountain, volcano, valley, canyon, island, desert, forest moon, planet, star, constellation, (landforms and water forms?)-->


<div id="tab:named_entity_types">
	
| Class            |Type                |Subtype           |
|------------------|--------------------|------------------|
| animal           |                    |                  |
| plant            |                    |                  |
| language         |                    |                  |
| nationality      |                    |                  |
| individual_person |                    |                  |
| social_group      | family              |                  | 
|                  | ethnic-group        |                  |
|                  | regional-group      |                  |
|                  | religious-group     |                  |
|                  | clan              	|                  |
|                  | organization        | international_organization, business, company, government_organization, political_organization, criminal_organization,  armed_organization, academic_organization, association, sports_organization, religious_organization |
| geographic_entity | ocean, sea, lake, river, gulf, bay, strait, canal, peninsula, mountain, volcano, valley,  canyon, island, desert, forest |  |
|  celestial-body   | moon, planet, star, constellation |   |
| region           | local-region, country-region, world-region |   |
|  geo-political-entity             |city, city-district, county, state, province, territory, country|  |
| facility         | airport, station, port, tunnel, bridge, road, railway-line, canal, building, theater, museum, palace, hotel, worship-place, market, sports-facility, park, zoo, amusement-park |  |
| vehicle          |  ship, aircraft, aircraft-type, spaceship, car-make | |
| cultural-artifact | work-of-art |
|                    |picture      |
|                    |music        | 
|                    |literature   |
|                    |dance        |
|                    | show        |
|                    | broadcast-program |
|                    |publication  |book, newspaper, magazine, journal |
|cultural-activity   |             |       |
| event              | incident,  natural-disaster, earthquake, war, conference, game, festival, ceremony | |
| law                | court-decision, treaty | | 
| award              |  |   |
| food-dish          |  |   |
|notational-system   |writing-script, music-key, musical-note |
| variable           |   |  |
| computer-program   |   |   |
| biomedical-entity | molecular-physical-entity, small-molecule, protein, protein-family, protein-segment, amino-acid, macro-molecular-complex, enzyme, nucleic-acid, pathway, gene, dna-sequence, cell, cell-line, species, taxon, disease, medical-condition| |

</div>

<!-- 
<div id="tab:named_entity_types">

|Type   |  Subtype (AMR NE Type) |
|-------|------------------------|
| person  |person, family, animal, language, nationality, ethnic-group, regional-group, religious-group, political-movement|
|*Organization* | commerical_org (company), political_org (political-party), government_org (government_organization), military_org (military), criminal_org (criminal-organization), academic_org (school, university, research-institute), sports_org (team, league), market-sector|
| *Geographic-entity*   | ocean, sea, lake, river, gulf, bay, strait, canal, peninsula, mountain, volcano, valley, canyon, island, desert, forest|
|  *Celestial-body*     |moon, planet, star, constellation|
| *region*              | local-region, country-region, world-region|
|  *GPE*     |city, city-district, county, state, province, territory, country| 
|  *facility*| airport, station, port, tunnel, bridge, road, railway-line, canal, building, theater, museum, palace, hotel, worship-place, market, sports-facility, park, zoo, amusement-park|
|  *event*   |  incident, natural-disaster, earthquake, war, conference, game, festival|
|  *product* |vehicle, ship, aircraft, aircraft-type, spaceship, car-make, work-of-art, picture, music, show, broadcast-program|
|   *publication*    |book, newspaper, magazine, journal|
|  *Natural-object*| |
|  *Artifact*      |award, law, court-decision, treaty, music-key, musical-note, food-dish, writing-script, variable, program|
|   *Biomedical-entity*| molecular-physical-entity, small-molecule, protein, protein-family, protein-segment, amino-acid, macro-molecular-complex, enzyme, nucleic-acid, pathway, gene, dna-sequence, cell, cell-line, species, taxon, disease, medical-condition|

Table 5: Named entity types
</div>
-->

[Back to Table of Contents](#toc)

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

[Back to Table of Contents](#toc)

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
So, this single word expresses the predicate, and the actor, undergoer,
theme, and instrument arguments of this state of affairs.

<span id="3-1-3-1 (1)" label="3-1-3-1 (1)">\[3-1-3-1 (1)\]</span>
```
nih-teb-e'ei-s-o'
PST-break/remove.stick.like-head-by.blade.CAUS-1SG/3SG
'I cut his head off with a knife.'
(t/ teb-e'ei-s ‘break/remove.stick.like’
    :actor (p/ person
    	:ref-person 1st
	:ref-number Singular)
    :undergoer (p2/ person
    	:ref-person 3rd
	:ref-number Singular)
    :theme (t2/ thing
    	:ref-person Obviative)
    :aspect Performance
    :modstr FullAff)
```

When languages use verbal affixes to index arguments, these arguments
then may or may not be expressed through independent NPs elsewhere in
the clause. UMR treats such indexed arguments in the same way as it does
free pronouns - they are identified as arguments of the verb. So, even
though there is no overt word in the sentence above referring to a first
person actor or a third person undergoer, these arguments are
nevertheless identified and annotated (using a named-entity concept, in
this case `person` or `thing`), as they are clearly identifiable to
native speakers of the language.

Noun incorporation constructions come in different types across
languages (Mithun 1984). Some constructions, such as the one illustrated by *-e'ei*
'head' above, are not very grammaticalized. Here, the incorporated noun
functions as an argument of the verb, meaning that no overt NP can be
present in the clause to fill this semantic role. So, while UMR treats
the whole stem *teb-e'ei-s* as the predicate, it also identifies a
separate concept for 'head', which has the `:theme` participant role as
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
with the `:instrument` role is only identified if it is expressed as an
overt NP in the clause.

This treatment of noun incorporation means that a certain amount of
linguistic analysis must be done prior to UMR annotation. If the
language at hand has one or more noun incorporation constructions,
annotators need to know for any individual construction whether or not
it allows the expression of the incorporated participant as an
independent overt NP. Of course, grammaticalization is a continuous
process, and therefore noun incorporation constructions are likely to be
found on a continuum between these two end points. However, we map this
continuum onto a discrete choice for annotators by taking the ability of
an incorporated noun to co-occur with an independent NP as criterial. This treatment of single words containing predicates and arguments is summarized in table 6 below.

<div id="tab:noun_incorporation">

| **Construction type** | **Construction definition/diagnostic** | **UMR Treatment** |
| :------------------------------- | :----------------------------------------------------------------------------------------------------- |:------------------------------------------------------------------------------------------|
| Pronominal affixes | Verbal affixes expressing person/number values of arguments | If coreferential with overtly expressed nominal argument: don't annotate |
| | | If no overt nominal is present: annotate as argument with relevant named-entity concept |
| Incorporated nouns | No nominal expression coreferential with the incorporated noun can occur in the clause | Annotate separate concept for incorporated noun as argument |
| Verbal classifier | Nominal expression specifying type of object denoted by incorporated noun can occur in the clause | Do not annotate separate concept for incorporated noun |

Table 6: Treatment of pronominal affixes and noun incorporation
</div>

[Back to Table of Contents](#toc)

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

<span id="3-1-3-2 (1a)" label="3-1-3-2 (1a)">\[3-1-3-2 (1a)\]</span> Grandmother made the kid drink the water.
```
(d/ drink
    :cause (m/ make
    	:actor (p/ person
	    :ARG0-of (k/ kinship-91
		 :ARG2 (g/ grandmother))
	    :ref-number Singular)
    	:aspect Performance
	:modstr FullAff)
    :actor (k2/ kid
    	:ref-number Singular)
    :undergoer (w/ water)
    :aspect Performance
    :modstr FullAff)
```
<span id="3-1-3-2 (1b)" label="3-1-3-2 (1b)">\[3-1-3-2 (1b)\]</span> Grandmother did not make the kid drink the water.
```
(d/ drink
    :cause (m/ make
    	:actor (p/ person
	    :ARG0-of (k/ kinship-91
		 :ARG2 (g/ grandmother))
	    :ref-number Singular)
    	:aspect Performance
	:modstr FullNeg)
    :actor (k2/ kid
    	:ref-number Singular)
    :undergoer (w/ water)
    :aspect Performance
    :modstr NeutAff)
```

<span id="3-1-3-2 (1c)" label="3-1-3-2 (1c)">\[3-1-3-2 (1c)\]</span> Grandmother made the kid not drink the water.
```
(d/ drink
    :cause (m/ make
    	:actor (p/ person
	    :ARG0-of (k/ kinship-91
		 :ARG2 (g/ grandmother))
	    :ref-number Singular)
    	:aspect Performance
	:modstr FullAff)
    :actor (k2/ kid
    	:ref-number Singular)
    :undergoer (w/ water)
    :aspect Performance
    :modstr FullNeg)
```

Kukama (Tupían), on the other hand, has a morphological causative, as in
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
    :causer (p/ person
    	:ARG0-of (k2/ kinship-91
		:ARG2 (n/ nai 'grandmother'))
	:ref-number Singular)
    :actor (c/ churan 'kid')
    :undergoer (u/ uni 'water')
    :aspect Performance
    :modstr FullAff)
```

This criterion will be used for all valency change concepts: if the
"lexical" concept expressed by the verb root and the valency change
concept can be negated independently, two events are identified, whereas
if they cannot be negated independently, only one event is identified
corresponding to the derived verb stem (see table 7). The semantics and valency of
such derived forms will be inferred from the participant role annotation
associated with the verb. Which valency changes lead to which argument
structures is detailed in [Part 3-2-1-2-1](#part-3-2-1-2-1-valency-alternations).

<div id="tab:valency_changes">
	
| **IF** | **THEN** |
| :---------------------------------------------------------------------- |:------------------------------------------------|
| Event and valency-changing category can be negated independently | Identify and annotate them as separate events |
| Event and valency-changing category cannot be negated independently | Identify a single event |

Table 7: Treatment of valency-changing categories
</div>

[Back to Table of Contents](#toc)

##### Part 3-1-3-3. TAM categories

Third, some semantic categories such as (phasal) aspect, temporal
relations, and modal relations, can be expressed cross-linguistically
either through bound morphology or through separate words (often called
"auxiliaries").

Phasal aspectual meanings such as inchoative, completive, and
continuative, firstly, are never identified as separate events, even if
they are expressed through independent words. Instead, they will simply
inform the aspect attribute label of the event they modify ([Part 3-3-1](#part-3-3-1-Aspect)). This principle is illustrated in example
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
    :ARG1 (c/ ce 'paper')			    :ARG1 (p/ paper)
    	:mod (s/ əsi 'this')			        :mod (t/ this)
    :ARG2 (m/ mu 'black')			    :ARG2 (b/ black)
    :aspect Performance)			    :aspect Performance)
```

Similarly, modal and temporal auxiliaries will not be identified
independently as events, but will instead inform the modal and temporal
dependency annotation: in English, for example, modal auxiliaries such
as *might* and *should* in *He **might/should** go to school* are not
identified as independent events, and neither are temporal auxiliaries
such as *have* and *be* in *She **has gone/is going** to school*. How
such meanings exactly inform the temporal and modal annotation is
detailed in [Part 4-2](#part-4-2-temporal-dependency) and [Part 4-3](#part-4-3-modal-dependency).

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
    :ARG0 (p/ person
    	:ref-person 3rd
	:ref-number Singular)
    :ARG1 (g/ go-01
    	:ARG1 p
        :ARG4 (s/ school)
        :aspect Performance
	:modpred w)
    :aspect State
    :modstr FullAff)
```
<span id="3-1-3-3 (2b)" label="3-1-3-3 (2b)">\[3-1-3-3 (2b)\]</span> She may want to go to school.
```
(w/ want-01
    :ARG0 (p/ person
    	:ref-person 3rd
	:ref-number Singular)
    :ARG1 (g/ go-01
    	:ARG1 p
        :ARG4 (s/ school)
        :aspect Performance
	:modpred w)
    :aspect State
    :modstr NeutAff)
```

However, if in a language the desire-event cannot be modalized
independently from the desired event, no separate event is identified
for the desire-semantics. Instead, the desiderative is taken into
account in the modal annotation, as detailed in [Part 4-3](#part-4-3-modal-dependency). For three
other semi-modal concepts, the same guidelines as to concept-word
mismatches are used as for desideratives: this is the case for conatives
('try to'), optatives ('wish that'), and frustratives ('fail to').

[Back to Table of Contents](#toc)

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
1PL-DSTR-sleep-TI-VNT-NOM	La	Esperanza
'We slept in La Esperanza while coming here'
(e/ enna'tenekanta' 'sleep while coming'		(s/ sleep-01
    :undergoer (p/ person				    :ARG0 (p/ person
    	:ref-person 1st						:ref-person 1st
	:ref-number Plural)					:ref-number Plural)	    
    :place (c/ city					    :place (c/ city
    	:name (n/ name					        :name (n/ name
            :op1 "La"						    :op1 "La"
            :op2 "Esperanza"))				    	    :op2 "Esperanza"))
    :aspect State					    :temporal (c2/ come-01
    :modstr FullAff)					        :ARG1 p
    								:ARG4 (h/ here)
                                                        	:aspect Activity
                                                        	:modstr FullAff)
                                                    	    :aspect State
                                                   	    :modstr FullAff)
```

The English "venitive" construction in the translational equivalent of
[\[3-1-3-4 (1)\]](#3-1-3-4 (1)), however, can co-occur with an NP which is clearly an argument of the "come"-event: one could say, for instance *We slept in La Esperanza
while coming here **from Puerto Casado***. Therefore, the motion event
and the "sleep"-event are construed in English as two independent
events, and are annotated in UMR as two separate predicates.

[Back to Table of Contents](#toc)

##### Part 3-1-3-5. Non-verbal clauses

Many types of "non-verbal clauses", such as predicate nominals and
predication of properties, possession, and location (see [Part 3-1-1-3](#part-3-1-1-3-states-and-entities) for the predicates UMR predicates that are used to annotate these meanings), show different
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
for the annotation of predicate-argument structure, since there is no
separate material that can be identified as a predicate.

<span id="3-1-3-5 (1)" label="3-1-3-5 (1)">\[3-1-3-5 (1)\]</span> 
```
ajan	kunumi		tsumi
this	young.man	shaman
'This young man is a shaman.'

(h/ have-role-91						(h/ have-role-91
    :ARG0 (k/ kunumi 'young man'				    :ARG0 (m/ man
    	:mod (a/ ajan 'this')						:mod (y/ young)
	:ref-number Singular)						:mod (t/ this)						
    :ARG2 (t/ tsumi 'shaman')						:ref-number Singular)	
    :aspect State						    :ARG2 (s/ shaman)
    :modstr FullAff)						    :aspect State
    								    :modstr Aff)
```

<span id="3-1-3-5 (2)" label="3-1-3-5 (2)">\[3-1-3-5 (2)\]</span> 
```
Mijiri-tin	ɨara-yara
Miguel-CER	canoe-owner
'Miguel does have a canoe.' lit. 'Miguel is a canoe-owner.'

(h/ have-91							(h/ have-91
    :ARG0 (p/ person						    :ARG0 (p/ person
    	:name (n/ name :op1 "Mijiri")					:name (n/ name :op1 "Miguel")
	:ref-number Singular)					    	:ref-number Singular)
    :ARG1 (a/ ɨarayara 'canoe')					    :ARG1 (c/ canoe)
    :aspect State						    :aspect State
    :modstr FullAff)						    :modstr FullAff)
```

We propose a set of seven abstract concept predicates each corresponding
to a discrete "non-verbal clause" function, listed in the table below. When there is no overt predicate-word, as
in [\[3-1-3-5 (1)\]](#3-1-3-5 (1)), we assume that annotators will be able
to recognize the type of non-verbal clause function they are dealing
with. They should use such an abstract predicate concept as predicative core of the graph, and use the appropriate numbered argument roles as specified in
the table (see also [Part 3-2-1-1-1](#part-3-2-1-1-1-nonverbal-clauses) for more in-depth treatment of the argument structure annotation with these predicates).

In constructions with predicativized arguments, such as
[\[3-1-3-5 (2)\]](#3-1-3-5 (2)), once again annotators are expected to recognize the type of non-verbal clause function at hand and select the appropriate predicate. An argument concept will be identified and linked to the predicativized participant word in the sentence - the possessum *ɨara-yara* in the case of [\[3-1-3-5 (2)\]](#3-1-3-5 (2)). As can be seen in the example UMRs
above, the resulting graphs have similar structures regardless of
whether a language uses an overt-predicate strategy, a zero-predicate
(juxtaposition) strategy, or a predicativized argument strategy for such
"non-verbal clause" meanings.

<div id="tab:nonverbal_arguments">
	
| **Clause Type**        | **Predicate**    | **ARG0**  | **ARG1**         | **ARG2**         |
| :--------------------- | :--------------- | :-------- | :--------------- | :--------------- |
| Thetic Possession      | have-91          | possessor | possessum        | ---              |
| Predicative Possession | belong-91        | possessum | possessor        | ---              |
| Thetic Location        | exist-91         | location  | theme            | ---              |
| Predicative Location   | have-location-91 | theme     | location         | ---              |
| Property Predication   | have-mod-91      | ---       | theme            | property         |
| Object Predication     | have-role-91     | theme     | reference point  | object category  |
|                        | have-org-role-91 | theme     | organization     | role             |
|                        | kinship-91       | theme     | family member    | kinship rel.     |
| Equational             | identity-91      | theme     | equated referent | ---              |

Table 8: Argument structure of non-verbal clause predicates
</div>

##### Part 3-1-3-6. Multi-word concepts

In languages with simpler morphology, the opposite situation, *multi-word concepts* may arise. Multi-word concepts can simply be handled by
concatenating the lemmatized words, as in [\[3-1-3-6 (1)\]](#3-1-3-6 (1)).

<span id="3-1-3-6 (1)" label="3-1-3-6 (1)">\[3-1-3-6 (1)\]</span>

<span id="3-1-3-6 (1a)" label="3-1-3-6 (1a)">\[3-1-3-6 (1a)\]</span> So I normally steep it in hot water , then take it out and stir - fry it.
```
(c/ cause-01
      :ARG1 (a/ and
            :op1 (s/ steep-01
                  :ARG0 (p/ person
		        :ref-person 1st
			:ref-number Singular)
                  :ARG1 (t/ thing
		        :ref-number Singular)
                  :ARG2 (w/ water
                        :ARG1-of (h/ hot-05))
		  :aspect Habitual
		  :modstr FullAff)
            :op2 (a2/ and
                  :op1 (t2/ take-out-11
                        :ARG0 p
                        :ARG1 t
			:aspect Habitual
			:modstr FullAff)
                  :op2 (s2/ stir-01
                        :ARG0 p
                        :ARG1 t
			:aspect Habitual
			:modstr FullAff)
                  :op3 (f/ fry-01
                        :ARG0 p
                        :ARG1 t
			:aspect Habitual
			:modstr FullAff)
                  :temporal (t3/ then)))
      :ARG1-of (n/ normal-02))
```

<span id="3-1-3-6 (1b)" label="3-1-3-6 (1b)">\[3-1-3-6 (1b)\]</span> The moral aspects of the movement intrigued him as well
```
(i/ intrigue-01
      :ARG0 (a/ aspect
            :ARG1-of (m/ moral-02)
            :poss (m2/ movement-07)
	    :ref-number Plural)
      :ARG1 (p/ person
            :ref-person 3rd
	    :ref-number Singular)
      :mod (a2/ as-well)
      :aspect State
      :modstr FullAff)
```

[Back to Table of Contents](#toc)
#### Part 3-1-4. Word senses
 
 UMR allows concepts to be word senses. In order to annotate word senses, it is necessary to first have a sense inventory for all words that need to be sense-disambiguated. For languages that do not have a sense inventory, concepts can simply be represented by lemmas. For predicate concepts which the annotator wants to flag for later inclusion in a lexicon, the suffix -00 can be added to such lemmas. It is also possible that a language only has a sense inventory for a subset of the words. This is the case with English [\[3-1-4 (1)\]](#3-1-4 (1)) and Chinese [\[3-1-4 (2)\]](#3-1-4 (2)), where word senses are defined for predicates together with their arguments in *frame files*.

<span id="3-1-4 (1)" label="3-1-4 (1)">\[3-1-4 (1)\]</span> The school has approximately 570 pupils.
``` 
(h/ have-91
      :ARG0 (s/ school)
      :ARG1 (p/ pupil
            :quant (a/ approximately :op1 570))
      :aspect State
      :modstr FullAff)
```

<span id="3-1-4 (2)" label="3-1-4 (2)">\[3-1-4 (2)\]</span>
 ```
 并且 还 有 很多 高层 的 人物 哦 ！
There will even be many VIPs!
(x/ and
      :op2 (e/ exist-91
            :mod (x2/ 还)
            :ARG1 (x3/ 人物
                   :mod (x4/ 高层)
                   :quant (x5/ 很多))
            :mode Expressive
	    :aspect State
	    :modstr FullAff))
```
 


 [Back to Table of Contents](#toc)
 #### Part 3-1-5. Scope for Quantification and negation

To facilitate the translation of UMR into first-order expressions to support logical inference,
we add a **scope** concept to represent the relative order of the predicate, quantified concept and negated concept.
In most cases, the order of these elements are interpreted in textual order, and do not need an over scope annotation.
The scope annotation is only needed when these elements are interpreted "out-of-order", as in [\[3-1-5 (1)\]](#3-1-5 (1)).

<span id="3-1-5 (1)" label="3-1-5 (1)">\[3-1-5 (1)\]</span>
```
Someone didn't answer all the questions
(a/ answer-01
   :ARG0 (p/ person)
   :ARG1 (q/ question
              :quant A
              :polarity -)
   :Pred-of (s/ scope
                :ARG0 p
                :ARG1 q))
```

Related to scope is the issue of distributive vs. collective interpretations of events. Ambiguities in this realm may arise in a great number of different contexts. They may be triggered by, amongst others, explicit quantifiers or numerals, or events with plural arguments. For example, in [\[3-1-5 (2)\]](#3-1-5 (2)) below, is there a single woman which every man loves, or does every man love a different woman? The latter interpretation is distributive, the former is usually interpreted as collective.

<span id="3-1-5 (2)" label="3-1-5 (2)">\[3-1-5 (2)\]</span>

<span id="3-1-5 (2a)" label="3-1-5 (2a)">\[3-1-5 (2a)\]</span> Each man loves a woman.

However, many cases that are technically ambiguous nevertheless have a strong default reading stemming from the lexical semantics of the predicate and its arguments. For example, in [\[3-1-5 (3a)\]](#3-1-5 (3a)), there is a strong default interpretation that every single student ran 5 kilometers rather than that they ran a total of 5 kilometers between them - _run_ is typically an individual activity, so its lexical semantics trigger a default distributive reading. However, in [\[3-1-5 (3b)\]](#3-1-5 (3b)), the equally strong default interpretation is that the students carried a single piano together and there was only a single carrying-event - our world knowledge specifies that things as heavy as a piano must typically be carried by multiple people, so the lexical semantics of the predicate-argument combination here trigger a default collective reading. In yet another set of cases, our "default" feeling is that it does not really matter in what configurations the participants participate in the denoted events. In [\[3-1-5 (3c)\]](#3-1-5 (3c)), all that typically matters is that 6 states were hit by at least one hurricane each, and that there was a total of 10 hurricanes. We can't really know how many hurricanes hit each state, and we don't really care - all we know is that 6 states and 10 hurricanes were involved. This kind of default interpretation is called a summation reading.
					
<span id="3-1-5 (3)" label="3-1-5 (3)">\[3-1-5 (3)\]</span>

<span id="3-1-5 (3a)" label="3-1-5 (3a)">\[3-1-5 (3a)\]</span> The linguistics students ran 5 kilometers to raise money for charity.

<span id="3-1-5 (3b)" label="3-1-5 (3b)">\[3-1-5 (3b)\]</span> The linguistics students carried a piano into the theater.

<span id="3-1-5 (3c)" label="3-1-5 (3c)">\[3-1-5 (3c)\]</span> Ten hurricanes hit six states over the weekend.

Scope will not be annotated for summation readings (as we cannot reliably know it from the text alone), nor is it annotated where a distributive or collective reading can be predictably derived from the lexical semantics. In other words, whenever _run_ is interpreted distributively or _carry a piano_ is interpreted collectively, no scope annotation is needed. The scope annotation only comes into play when some overt linguistic element forces an interpretation that diverges from the lexical default. For example, in [\[3-1-5 (4a)\]](#3-1-5 (4a)), _together_ forces a collective interpretation of _run_, in [\[3-1-5 (4b)\]](#3-1-5 (4b)), _each_ forces a distributive interpretation of _carry a piano_, and in [\[3-1-5 (4c)\]](#3-1-5 (4c)), _each_ similarly forces a distributive interpretation of _hit_. In all these cases, a (s / scope) predicate would appear to clarify the non-canonical scopal relations.

<span id="3-1-5 (4)" label="3-1-5 (4)">\[3-1-5 (4)\]</span>

<span id="3-1-5 (4a)" label="3-1-5 (4a)">\[3-1-5 (4a)\]</span> The linguistics students together ran 200 kilometers to raise money for charity.

<span id="3-1-5 (4b)" label="3-1-5 (4b)">\[3-1-5 (4b)\]</span> The bodybuilders each carried a piano into the theater.

<span id="3-1-5 (4c)" label="3-1-5 (4c)">\[3-1-5 (4c)\]</span> Ten hurricanes each hit six states over the weekend.

[Back to Table of Contents](#toc)

#### Part 3-1-6. Discourse-relations

When multiple events are expressed in a complex sentence, a variety of semantic relations can hold between them. UMR provides annotators with a lattice of category values to annotate such discourse-level event-event relations. This lattice is based partly on existing typological research (Malchukov 2004; Thompson & Longacre 1985), and partly on patterns of expression through adverbial subordination or coordination in English. This lattice covers event-event relations that are typically overtly and obligatorily expressed in languages through either (coordinating or subordinating) conjunctions or dedicated (“deranked”) verb forms. In other words, it does not cover relations typically expressed through optional “discourse adverbs”.

![Discourse Lattice_2022](https://github.com/umr4nlp/umr-guidelines/blob/master/Guidelines_figures/Discourse%20Lattice_2022.png)

Annotators may choose annotation values from more fine-grained levels of the lattice when they are confident in doing so, or from more course-grained levels when they are in doubt. Generally, (adverbial) subordination constructions express overtly more fine-grained values. Many of these are already treated in other parts of UMR (particularly through participant roles), in which case cross-references will lead annotators to the relevant sections of this document. Coordination constructions tend to be more polysemous – they subsume various more fine-grained values and may be ambiguous between them, and they might therefore require the use of higher-level categories. This description already hints at the observation that many of the event-event relations on this lattice can be expressed through either coordination or subordination. We follow Talmy (1978), Reinhart (1984), and Wierzbicka (1980) in taking this difference not to be a semantic one, but rather an information-structural one between a “complex figure” construal (both events are equally “prominent”) and a “figure-ground” construal (one event is “foregrounded” and another is “backgrounded”). We therefore do not require annotators to annotate the same meaning differently when expressed through coordination as opposed to subordination (although, as mentioned before, subordination constructions may allow for the identification of more fine-grained meanings). In the examples below, both options are illustrated wherever possible.

Each discourse relation on the lattice is defined below, based on Croft (to appear, ch. 15, ch. 17).

```Disjunctive```: Construes two (or more) events as being alternatives of each other in some way. Roughly corresponds to the range of meanings expressed by English _(either) or_. UMR expresses this meaning through an abstract concept ```or``` which takes numbered ```:opX``` arguments for the construed alternatives as in [\[3-1-6 (1)\]](#3-1-6 (1)).

<span id="3-1-6 (1)" label="3-1-6 (1)">\[3-1-6 (1)\]</span>
```
I will go for a walk or play some soccer.
(o/ or
   :op1 (w/ walk-01
   	:ARG0 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:aspect Process
	:modstr FullAff)
   :op2 (p2/ play-01
   	:ARG0 p
	:ARG1 (s/ soccer)
	:aspect Process
	:modstr FullAff))
```

There are two more fine-grained subtypes of disjunctive relations:

```Inclusive Disjunctive```: also known as “non-exhaustive disjunction”. Indicates that either any of the construed alternatives can be “chosen” individually, or any combination of the construed alternatives. This is illustrated in [\[3-1-6 (2a)\]](#3-1-6 (2a)) from Hua (Haiman 1978:7-8). Here, _-ve_ indicates that bashing pandanus, husking and eating corn, and planting bananas are not mutually exclusive alternatives. Performing any or all of these actions equally violates a sexual taboo. UMR uses an abstract concept ```inclusive-disj``` to annotate this meaning, with numbered ```:opX``` roles for the construed alternatives.

```Exclusive Disjunctive```: also known as “exhaustive disjunction”. Indicates that the construed alternatives are presented as mutually exclusive options. This is illustrated in [\[3-1-6 (2b)\]](#3-1-6 (2b)) from Hua (Haiman 1980:271). Here, _ito_ indicates that his being here and his not being here are mutually exclusive alternatives. UMR uses an abstract concept ```exclusive-disj``` to annotate this meaning, with numbered ```:opX``` roles for the construed alternatives.

<span id="3-1-6 (2)" label="3-1-6 (2)">\[3-1-6 (2)\]</span>

<span id="3-1-6 (2a)" label="3-1-6 (2a)">\[3-1-6 (2a)\]</span>
```
mnu'bo		hatai-supi'ba-ve	kire'bo	kro-de-supi'ba-ve	egemo	bre-supi'ba-ve		degi	kiko-pi'	rmi-supamo	a-ki'		a'-vo-g-une
pandanus	bash-PURP.1PL-NONEX	corn	husk-eat-PURP.1PL-NONEX	banana	plant-PURP.1PL-NONEX	crazy	place-in	go_down-if.1PL	woman-with	not-sleep-fut-1PL.IND
'If we go down to a 'crazy place' to bash pandanus, husk and eat corn, or plant bananas, we don't sleep with women.'
(h/ have-condition-91
   :ARG1 (a/ a'vogune-00 'sleep'
   	:actor (p/ person
		:ref-person 1st
		:ref-number Plural)
	:companion (a2/ aki' 'woman')
	:aspect Habitual
	:modstr FullNeg)
   :ARG2 (r/ rmisupamo-00 'go down'
   	:actor p
	:goal (k/ kikopi' 'place'
		:mod (d/ degi 'crazy'))
	:Purpose (i/ inclusive-disj
		:op1 (h2/ hataisupi'bave-00 'bash'
			:actor p
			:undergoer (m/ mnu'bo 'pandanus')
			:aspect Performance
			:modstr FullAff)
		:op2 (k2/ krodesupi'bave-00 'husk and eat'
			:actor p
			:undergoer (k3/ kire'bo 'corn')
			:aspect Performance
			:modstr FullAff)
		:op3 (b/ bresupi'bave-00 'plant'
			:actor p
			:undergoer (e / egemo 'banana')
			:aspect Performance
			:modstr FullAff)
	:aspect Performance
	:modstr FullAff
   :aspect State)
	
```

<span id="3-1-6 (2b)" label="3-1-6 (2b)">\[3-1-6 (2b)\]</span>
```
bai-ve		ito	'a'-bai-e
be.3SG-INTERR	EX	NEG-be.3SG-IND
'Is he here or isn't he?'
(e/ exclusive-disj
   :op1 (h/ have-location-91
   	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Singular)
	:ARG1 (p2/ place)
	:aspect State
	:modstr NeutAff
	:mode Interrogative)
   :op2 (h2/ have-location-91
   	:ARG0 p 
	:ARG1 p2
	:aspect State
	:modstr NeutNeg
	:polarity -
	:mode Interrogative))
```

The exclusive disjunction relation has one further, more specific subtype:

```Apprehensive```: expresses that two events are mutually exclusive alternatives, but more specifically, that one event is carried out with the intention of preventing the other event from happening. It is in a way a negated counterpart of the `purpose` relation discussed below. In [\[3-1-6 (3)\]](#3-1-6 (3)), the implication is that if the addressee of the imperative grabs a stick, they will not be attacked - the grab-event and the attack-event are mutually exclusive alternatives. As illustrated in [\[3-1-6 (3)\]](#3-1-6 (3)), English has a dedicated subordinator to express apprehensive relations, but may also draw on its polysemous disjunctive coordinator, which has apprehensive as one of its functions. In the latter case, annotators may either use the higher-level category (the ```or``` abstract concept) in the lattice, or if they are confident, the lower-level category (using the ```:apprehensive``` relation. The same holds for many of the other fine-grained meanings discussed below - illustrative annotations will not be provided for all of them.

<span id="3-1-6 (3)" label="3-1-6 (3)">\[3-1-6 (3)\]</span>

<span id="3-1-6 (3a)" label="3-1-6 (3a)">\[3-1-6 (3a)\]</span>
```
Grab a stick lest he attack you!
(g/ grab-01
     :ARG0 (p/ person
          :ref-person 2nd
	  :ref-number Singular)
     :ARG1 (s/ stick
          :ref-number Singular)
     :apprehensive (a/ attack-01
          :ARG0 (p2/ person
	       :ref-person 3rd
	       :ref-number Singular)
	  :ARG1 p
	  :aspect Performance
	  :modstr FullAff)
     :mode Imperative
     :aspect Performance
     :modstr PrtAff)
```

<span id="3-1-6 (3b)" label="3-1-6 (3b)">\[3-1-6 (3b)\]</span>
```
Grab a stick or he will he attack you!
(g/ grab-01					Or	(o/ or
     :ARG0 (p/ person						:op1 (g/ grab-01
          :ref-person 2nd						:ARG0 (p/ person
	  :ref-number Singular)							:ref-person 2nd
     :ARG1 (s/ stick								:ref-number Singular)
          :ref-number Singular)						:ARG1 (s/ stick
     :apprehensive (a/ attack-01						:ref-number Singular)
          :ARG0 (p2/ person						:mode Imperative
	       :ref-person 3rd						:aspect Performance
	       :ref-number Singular)					:modstr PrtAff)
	  :ARG1 p						:op2 (a/ attack-01
	  :aspect Performance						:ARG0 (p2/ person
	  :modstr FullAff)							:ref-person 3rd
     :mode Imperative								:ref-number Singular)
     :aspect Performance						:ARG1 p
     :modstr PrtAff)							:aspect Performance
                            						:modstr FullAff))
```

```Additive```: expresses the addition of one “figure” (foregrounded participant or event) to another one in order to form a complex figure. This is represented in UMR through an ```additive``` abstract concept with numbered ```:opX``` roles. The additive function has a number of more fine-grained subfunctions:

```Simultaneous```: expresses full or partial temporal overlap of the events that together form a complex figure. This is illustrated in [\[3-1-6 (4a)\]](#3-1-6 (4a)) - the reading-event and the listening-event take place, at least in part, at the same time. This function is annotated at the sentence level using the ```:temporal``` participant role relation (see [Part 3-2-1-1](#part-3-2-1-1-stage-0)), and at the document level through the :overlap temporal relation (see [Part 4-2-2](#part-4-2-2-temporal-relations)).

```(pure) Addition```: expresses no temporal specification of the sequencing of events, but rather that the two events that form a complex figure cannot occur separately from each other in the context of the utterance. In [\[3-1-6 (4b)\]](#3-1-6 (4b)), having either your hand stamped or showing your ticket stub alone is not sufficient to get into the concert - both are necessary. UMR uses a ```:pure-addition``` relation to connect two events semantically related in this way.

```Substitution```: expresses that one of the events that together form a complex figure is offered as an “alternative” or “replacement” for the other – this is typically expressed through the negation of one of the two coordinands, as in [\[3-1-6 (4c)\]](#3-1-6 (4c)). The acceptability of both _and_ and _but_ here illustrates that the substitutive function is intermediate between the conjunctive and adversative higher-level categories (see below). Substitutive meanings are annotated with the abstract `substitute-01` predicate. The rejected alternative is annotated as :ARG2, while the replacement is annotated as :ARG1

<span id="3-1-6 (4)" label="3-1-6 (4)">\[3-1-6 (4)\]</span>

<span id="3-1-6 (4a)" label="3-1-6 (4a)">\[3-1-6 (4a)\]</span>
```
I read a book while I listened to music. / I read a book while listening to music. / I read a book and listened to music.
(r/ read-01				Or		(a/ and
   :ARG0 (p/ person						:op1 (r/ read-01
   	:ref-person 1st							:ARG0 (p/ person
	:ref-number Singular)							:ref-person 1st
   :ARG1 (b/ book								:ref-number Singular)
   	:ref-number Singular)						:ARG1 (b/ book
   :temporal (listen-01								:ref-number Singular)
   	:ARG0 p								:aspect Performance
	:ARG1 (m/ music)						:modstr FullAff)
	:aspect State						:op2 (l/ listen-01
	:modstr FullAff)						:ARG0 p
   :aspect Performance							:ARG1 (m/ music)
   :modstr FullAff)							:aspect State
   									:modstr FullAff))
```

<span id="3-1-6 (4b)" label="3-1-6 (4b)">\[3-1-6 (4b)\]</span>
```
In addition to having your hand stamped, you have to show your ticket to get into the concert. / You have to have your hand stamped and show your ticket stub to get into the concert.
(a/ and							Or	(h/ have-04
   :op1 (h/ have-04							:ARG0 (p/ person
   	:ARG0 (p/ person							:ref-person 2nd
		:ref-person 2nd							:ref-number Singular)
		:ref-number Singular)					:ARG1 (s/ stamp-01
	:ARG1 (s/ stamp-01							:ARG0 (p2/ person)
		:ARG0 (p2/ person)						:ARG1 (h/ hand
		:ARG1 (h2/ hand								:part-of p)
			:part-of p)						:aspect Performance
		:aspect Performance						:modstr PrtAff)
		:modstr PrtAff)						:aspect Performance
	:aspect Performance						:modstr PrtAff
	:modstr PrtAff)							:pure-addition (s2/ show
   :op2 (s2/ show-01								:ARG0 p
   	:ARG0 p									:ARG1 (t/ ticket
	:ARG1 (t/ ticket								:poss p
		:poss p									:ref-number Singular)
		:ref-number Singular)						:ARG2 (p3/ person)
	:ARG2 (p3/ person)							:aspect Performance
   	:aspect Performance							:modstr PrtAff)
	:modstr PrtAff)							:purpose (g/ get-05
   :purpose (g/ get-05								:ARG0 p
   	:ARG0 p									:ARG2 (c/ concert
	:ARG2 (c/ concert								:ref-number Singular)
		:ref-number Singular)						:aspect Performance
	:aspect Performance							:modstr FullAff))
	:modstr FullAff)
```

<span id="3-1-6 (4c)" label="3-1-6 (4c)">\[3-1-6 (4c)\]</span>
```
Instead of going out to eat, we barbecued chicken at home. / We didn’t go out to eat and/but barbecued chicken at home.
(s/ substitute-01				Or		(a/ and
   :ARG1 (b/ barbecue-01						:op1 (g/ go_out-17
   	:ARG0 (p/ person							:ARG0 (p/ person
		:ref-person 1st								:ref-person 1st
		:ref-number Plural)							:ref-number Plural)
	:ARG1 (c/ chicken)							:purpose (e/ eat-01
	:location (h/ home)								:ARG0 p
	:aspect Performance								:aspect Endeavor
	:modstr FullAff)								:Modstr FullAff)
   :ARG2 (g/ go_out-17								:aspect Performance
   	:ARG0 p									:modstr FullNeg)				
	:purpose (e/ eat-01						:op2 (b/ barbecue-01
		:ARG0 p								:ARG0 p
		:aspect Endeavor						:ARG1 (c/ chicken)
		:modstr FullAff)						:location (h/ home)
	:aspect Performance							:aspect Performance
	:modstr FullNeg))							:modstr FullAff))
```

```Consecutive```: expresses two or more events as a complex figure, with additional information on their temporal and/or logical sequencing. Just like the ```Additive``` meaning, this is represented in UMR through a ```consecutive``` abstract concept with numbered ```:opX``` relations. The temporal relations holding between the events can then be further specified in the document-level temporal annotation. More fine-grained sub-functions of the consecutive function are the following:

```Purpose```: expresses the intention on the part of the agent of one event towards bringing about another event, as in [\[3-1-6 (5a)\]](#3-1-6 (5a)). This relation is annotated using the `:purpose` participant role relation (see [Part 3-2-1-1](#part-3-2-1-1-stage-0)).

```Means```: expresses a relation where one event accompanies another and characterizes more specifically what happened (or didn't happen) in another event, as in [\[3-1-6 (5b)\]](#3-1-6 (5b)). This relation has also been called “positive circumstantial”. This relation is annotated using the `:manner` participant role relation (see [Part 3-2-1-1](#part-3-2-1-1-stage-0)).

```Causal```: expresses a relation between a causing event and a resulting event, where the former explicitly brings about the latter, as in [\[3-1-6 (5c)\]](#3-1-6 (5c)). This relation is annotated using the `cause-01` predicate or the `:cause` participant role relation (see [Part 3-2-1-1](#part-3-2-1-1-stage-0)).

```Conditional```: expresses a relation where one event is contingent upon the occurrence of another event, as in [\[3-1-6 (5d)\]](#3-1-6 (5d)). This relation is annotated using the `have-condition-91` predicate or the `:condition` participant role relation (see [Part 3-2-1-1](#part-3-2-1-1-stage-0), [Part 4-3-1-5](#part-4-3-1-5-condition-relation)).

```Anterior```: expresses that one event takes place before another. This can either be expressed through an adverbial construction with the earlier event in the main clause and the later event in a subordinate clause, or through iconicity of tense in coordinated clauses with the earlier event in the sequentially prior clause, all exemplified in [\[3-1-6 (5e)\]](#3-1-6 (5e)). This relation is annotated at the sentence level, using the `:temporal` participant role relation (see [Part 3-2-1-1](#part-3-2-1-1-stage-0)), and at the document level (see [Part 4-2-2](#part-4-2-2-temporal-relations)).

```Posterior```: expresses that one event takes place following another. This can either be expressed through an adverbial construction with the later event in the main clause and the earlier event in a subordinate clause, or through iconicity of tense in coordinated clauses with the later event in the sequentially later clause, all exemplified in [\[3-1-6 (5f)\]](#3-1-6 (5f)). This relation is annotated at the sentence level, using the `:temporal` participant role relation (see [Part 3-2-1-1](#part-3-2-1-1-stage-0)), and at the document level (see [Part 4-2-2](#part-4-2-2-temporal-relations)).

<span id="3-1-6 (5a)" label="3-1-6 (5a)">\[3-1-6 (5a)\]</span>
```
I grabbed a stick **in order to** defend myself. / I grabbed a stick **and** defended myself.
(g/ grab-01
	:ARG0 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:ARG1 (s/ stick
		:ref-number Singular)
	:purpose (d/ defend
		:ARG0 p
		:ARG1 p
		:aspect Performance
		:modstr FullAff)
	:Aspect Performance
	:modstr FullAff)
```

<span id="3-1-6 (5b)" label="3-1-6 (5b)">\[3-1-6 (5b)\]</span>
```
He got into the army **by** lying about his age. / He lied about his age **and** got into the army.
(g/ get-5
	:ARG1 (p/ person
		:ref-person 3rd
		:ref-number Singular)
	:ARG2 (a/ army)
	:manner (l/ lie-01
		:ARG0 p
		:ARG1 (t/ thing
			:ARG2-of (a2/ age-01
				:ARG1 p))
		:aspect Performance
		:modstr FullAff)
	:Aspect Performance
	:modstr FullAff)
```

<span id="3-1-6 (5c)" label="3-1-6 (5c)">\[3-1-6 (5c)\]</span>
```
Sarah moved back to California **because** she couldn't find a job in Washington. / Sarah couldn't find a job in Washington **and (so)** she moved back to California.
(m/ move-01
	:ARG0 (p/ person
		:name (n/ name :op1 "Sarah))
	:ARG2 (s/ state :wiki "California"
		:name (n2/ name :op1 "California))
	:mod (b/ back)
	:cause (f/ find-01
		:ARG0 p
		:ARG1 (j/ job)
		:place (s/ state :wiki "Washington"
			:name (n3/ name :op1 "Washington"))
		:aspect Performance
		:modstr FullNeg)
	:aspect Performance
	:modstr FullAff)
```

<span id="3-1-6 (5d)" label="3-1-6 (5d)">\[3-1-6 (5d)\]</span>
```
**If** you touch it, it might explode. / Touch it, **and** it might explode.
(e/ explode-01
	:ARG1 (t/ thing
		:ref-number Singular)
	:condition (t2/ touch-01
		:ARG0 (p/ person)
		:ARG1 t
		:aspect Performance
		:modstr FullAff)
	:aspect Performance
	:modstr NeutAff)
```

<span id="3-1-6 (5e)" label="3-1-6 (5e)">\[3-1-6 (5e)\]</span>
```
I went home **before** paying the check. / I went home **and** paid the check.
(g/ go-01
	:ARG1 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:ARG4 (h/ home)
	:temporal (b/ before
		:op1 (p2/ pay-01
			:ARG0 p
			:ARG3 (c/ check)
			:aspect Performance
			:modstr FullAff)
	:aspect Performance
	:modstr FullAff)
```

<span id="3-1-6 (5f)" label="3-1-6 (5f)">\[3-1-6 (5f)\]</span>
```
I went home **after** paying the check. / I paid the check **and** went home.
(g/ go-01
	:ARG1 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:ARG4 (h/ home)
	:temporal (a/ after
		:op1 (p2/ pay-01
			:ARG0 p
			:ARG3 (c/ check)
			:aspect Performance
			:modstr FullAff)
	:aspect Performance
	:modstr FullAff)
```

Together, the additive and consecutive functions and all their subfunctions can be subsumed under the higher-level, more coarse-grained conjunctive function, marked in UMR with the ```and``` abstract concept and numbered ```:opX``` roles. That these functions are all semantically related and that their conjoining under the higher-level function is appropriate is illustrated by _and_ being the English coordinator used to express all these functions when a complex-figure construal is chosen.

```(pure) Contrast```: expresses a relation of contrast in some way between events, without an element of unexpectedness. In [3-1-6 (6a)\]](#3-1-6 (6a)), properties attributed to Peter are contrasted with properties attributed to Vanja. Unlike with the “unexpected co-occurrence” relation below, there is no expectation that whenever two people are discussed and one of them is diligent, the other must be lazy. This meaning is annotated using the ```contrast-01``` abstract predicate and its numbered argument roles.

```Unexpected co-occurrence```: expresses a relation of juxtaposition between two events where the second event is unexpected in case the first occurs. For example, in [3-1-6 (6b)\]](#3-1-6 (6b)) from Russian (Malchukov 2004:180), it is unexpected that Vanja went to school given that she had a cold - the sentence implies, in other words, that people who have a cold usually do not go to school. UMR uses a ``unexpected-co-occurrence``` abstract concept with numbered ```:opX``` roles to represent this meaning.

<span id="3-1-6 (6)" label="3-1-6 (6)">\[3-1-6 (6)\]</span>

<span id="3-1-6 (6a)" label="3-1-6 (6a)">\[3-1-6 (6a)\]</span>
```
Petja	staratel'nyi,	a	Vanja	lenivyj
Peter	diligent	CONJ	Vanja	lazy
'Peter is diligent, but [contrast] Vanja is lazy.'
(c/ contrast-01
   :ARG1 (h/ have-mod-91
   	:ARG1 (p/ person
		:name (n/ name :op1 "Peter"))
	:ARG2 (s/ staratel'nyi 'diligent')
	:aspect State
	:modstr FullAff)
   :ARG2 (h2/ have-mod-91
   	:ARG1 (p2/ person
		:name (n2/ name :op1 "Vanja"))
	:ARG2 (l/ lenivyj 'lazy')
	:aspect State
	:modstr FullAff))
```

<span id="3-1-6 (6b)" label="3-1-6 (6b)">\[3-1-6 (6b)\]</span>
```
Vanja	prostudilsja,	no	poshël	v	shkolu
Vanja	caught_cold	CONJ	went	to	school
'Vanja caught a cold, but [unexpected] went to school.'
(u/ unexpected-co-occurrence
   :op1 (p/ prostudilsja-00 'catch a cold'
   	:experiencer (p2/ person
		:name (n/ name :op1 "Vanja"))
	:aspect Performance
	:modstr FullAff)
   :op2 (p3/ poshël-00 'go'
   	:actor p2
	:goal (s/ shkolu 'school)
	:aspect Performance
	:modstr FullAff))
```

There are three subtypes of unexpected co-occurrence relations that confident annotators, or annotators for languages which have overt grammatical mechanisms of disambiguating them, may distinguish:

```Negative circumstantial```: expresses that the lack of occurrence of one event is a specific characterization of the other event, in the same way that the `means` relation discussed above expresses that the occurrence of one event is a specific characterization of another event. This meaning is classified as a subtype of “unexpected cooccurrence” because typically, the “more specific”, “characterizing” event that did not happen is only expressed overtly if the general expectation is that it _would_ happen. Compare the difference in naturalness between [3-1-6 (7a)\]](#3-1-6 (7a)) and [3-1-6 (7b)\]](#3-1-6 (7b)): the former sounds natural because we assume that, when carrying a bowl of punch, spills are a fairly common occurrence. The latter is not ungrammatical, but it implies that Sarah usually does a somersault whenever she carries bowls of punch. This relation is annotated using the `:manner` participant role relation (see [Part 3-2-1-1](#part-3-2-1-1-stage-0)), and a negative polarity attribute (see [Part 3-3-3](#part-3-3-3-polarity)).

```Concessive```: expresses a relation between two events towards which the speaker has a positive epistemic stance (i.e. the speaker believes they both occurred/will occur), but specifies that this co-occurrence is unexpected. Concessives have also been treated as negative causal relations (Comrie 1986). For instance, in [3-1-6 (7c)\]](#3-1-6 (7c)), the speaker asserts that both the state of being broke and the guitar-buying event occurred in the real world. The concessive _even though_ specifies that typically being broke causes one to not buy new guitars. This relation is annotated using the ```have-concession-91``` predicate or the shortcut ```:concession``` relation (see [Part 3-2-1-1](#part-3-2-1-1-stage-0), [Part 4-3](#part-4-3-modal-dependency)).

```Concessive conditional```: expresses that the state of affairs described in the apodosis will be true under the entire range of conditions described in the protasis. Concessive conditionals are different from regular conditionals in that they imply an expectation that the event expressed in the protasis may not lead to the event expressed in the apodosis happening. For instance, in [3-1-6 (7d)\]](#3-1-6 (7d)), there is an expectation that a mere five minutes of tardiness is not likely to cause one to be fired, and the concessive conditional contradicts this expectation: in the entire range of possible tardiness events, the event in the apodosis (being fired) will take place. This relation is annotated using the ```concessive-condition``` relation.

<span id="3-1-6 (7a)" label="3-1-6 (7a)">\[3-1-6 (7a)\]</span>
```
Sarah carried the bowl of punch into the living room **without** doing a somersault. / Sarah carried the bowl of punch into the living room **and/but** didn't do a somersault.
(c/ carry-01
	:ARG0 (p/ person
		:name (n/ name :op1 "Sarah"))
	:ARG1 (p2/ punch
		:unit (b/ bowl))
	:goal (r/ room
		:mod (l/ living))
	:manner (s/ somersault
		:ARG0 p
		:aspect Performance
		:polarity -
		:modstr FullNeg)
	:aspect Performance
	:modstr FullAff)
```

<span id="3-1-6 (7b)" label="3-1-6 (7b)">\[3-1-6 (7b)\]</span> 
```
Sarah carried the bowl of punch into the living room **without** spilling a drop. / Sarah carried the bowl of punch into the living room **and/but** didn't spill a drop.
(c/ carry-01
	:ARG0 (p/ person
		:name (n/ name :op1 "Sarah"))
	:ARG1 (p2/ punch
		:unit (b/ bowl))
	:goal (r/ room
		:mod (l/ living))
	:manner (s/ spill
		:ARG0 p
		:ARG1 p2
			:unit (d/ drop)
		:aspect Performance
		:polarity -
		:modstr FullNeg)
	:aspect Performance
	:modstr FullAff)
```

<span id="3-1-6 (7c)" label="3-1-6 (7c)">\[3-1-6 (7c)\]</span>
```
**Even though** he was broke, he bought a new guitar. / He was broke, **but (still)** bought a new guitar.
(b/ buy-01
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Singular)
	:ARG1 (g/ guitar
		:mod (n/ new)
		:ref-number Singular)
	:concession (h/ have-mod-91
		:ARG1 p
		:ARG2 (b2/ broke)
		:aspect State
		:modstr FullAff)
	:aspect Performance
	:modstr FullAff)
```

<span id="3-1-6 (7d)" label="3-1-6 (7d)">\[3-1-6 (7d)\]</span>
```
**Even if** you arrive only five minutes late, you will be fired.
(f/ fire-02
	:ARG1 (p/ person
		:ref-person 2nd
		:ref-number Singular)
	:aspect Performance
	:modstr FullAff
	:concessive-condition (a/ arrive-01
		:ARG1 p
		:temporal (l/ late
			:extent (t/ temporal-quantity
				:quant 5
				:unit (m/ minute)))
		:aspect Performance
		:modstr FullAff))
```

Some languages co-express the “(pure) contrast” and the “unexpected co-occurrence” meanings, using the same form to express both. These two meanings are therefore subsumed under the `adversative` category on the lattice, annotated in UMR using the ```but``` abstract concept and numbered ```:opX``` argument roles. However, both the “(pure) contrast” and the “unexpected co-occurrence meaning” may also be co-expressed with conjunctive meanings. Therefore, these categories combine into a number of higher-level, more coarse-grained categories on the UMR lattice above:

```And + unexpected```: abstract concept that may be used if a language does not formally distinguish conjuctive relations from unexpected co-occurrence relations. The language may still have a distinct form to express pure contrast. This abstract concept takes numbered ```:opX``` roles.

```And + contrast```: abstract concept that may be used if a language does not formally distinguish conjunctive relations from pure contrast relations. The language may still have a distinct form for expressing unexpected cooccurrence. This abstract concept takes numbered ```:opX``` roles.

```And + but```: abstract concept that may be used if a language does not formally distinguish between conjunctive relations and adversative relations at all. This abstract concept takes numbered ```:opX``` roles.

[Back to Table of Contents](#toc)

### Part 3-2. UMR relations 

   #### Part 3-2-1. Participant roles 
   
Every entity and event identified as a participant is related to an
event (the event that it is dependent on) and annotated with a
participant role label. The participant role annotation is organized as a road map with different stages. The factor which
determines where a language begins on the road map is whether there is
an existing PropBank-style lexicon (frame files) for the language which defines predicate-specific roles. An English PropBank
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
PropBank-style frame files. This is considered the ‘Stage 1’ participant
role annotation (see [Part 3-2-1-2](#part-3-2-1-2-stage-1)). The 'Stage 0' annotation involves
using a set of general participant roles, while building a lexicon of
PropBank-style frame files in order to move towards Stage 1 annotation.

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
```
ta-di=lo	daki-a		tioni	arimi 		ta 	besu  
PFV-3PL.S=go	find-3SG.O	man	feel.sorry	3SG.PFV	be.hungry
‘When they found him, the poor many was hungry.’
```

<span id="3-2-1 (2b)" label="3-2-1 (2b)">\[3-2-1 (2b)\]</span>
```
ta-di=lama 	ari 	da-daki 	uua=i
PFV-3PL.S-TAM	REC	RDP-find	in.that.direction=LOC
‘They had found each other.’
```

The event described in [\[3-2-1 (2a)\]](#3-2-1 (2a)) is different than the
event described in [\[3-2-1 (2b)\]](#3-2-1 (2b)) - in the former, the finder and findee are different, while in the latter they are the same. This is in contrast to
valency alternations which reflect a pragmatic difference between the
basic and non-basic construction. With pragmatic alternations, both
constructions refer to the same “real-world” event, but they package
that information differently, often in terms of the topicality (or,
discourse salience) of participants. Passive constructions are an
example of a pragmatic valency alternation, as seen in
[\[3-2-1 (3)\]](#3-2-1 (3)) from Balinese (Shibatani and Artawa 2013).

<span id="3-2-1 (3)" label="3-2-1 (3)">\[3-2-1 (3)\]</span>
```
anak=e 		muani	cenik	ento 	ngajeng buah=e 		ento 
person=DEF	male	small	that	eat	fruit=DEF	that
‘The boy ate the fruit.’
```
<span id="3-2-1 (3b)" label="3-2-1 (3b)">\[3-2-1 (3b)\]</span>
```
buah=e 		ento 	ajeng=a 	teken 	anak=e 		muani 	cenik	ento
fruit=DEF	that	eat=PASS	by	person=DEF	male	small	that
‘The fruit was eaten by the boy.’
```
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
of the road map, which will be detailed in [Part 3-2-1-1-2](#part-3-2-1-1-2-valency-alternations) and [Part 3-2-1-2-1](#part-3-2-1-2-1-valency-alternations).

[Back to Table of Contents](#toc)

##### Part 3-2-1-1. Stage 0

At Stage 0, a set of general (i.e., non-lexicalized) semantic roles are
used. These certainly will not map exactly to the grammatical marking of
argument phrases in any language, but this set of roles was selected
based on cross-linguistic patterns of argument marking. The set of
participant role labels, a brief description for each label, and
examples are shown below in Table 9.

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

Table 9: UMR non-lexicalized roles
</div>

These general semantic roles can be categorized based on the types of
events with which they occur, shown in Table 10. Some
participant roles (those found in the first column of the table) express the external cause of an event. These can
occur with many semantic classes of events. Similarly, the
“circumstantial” type semantic roles in the last column of the table can occur with a wide range of
semantic event classes. Note that UMR uses `:temporal` to annotate temporal circumstantials of events, while `:time` is only used as a daughter of `date-entity` concepts to annotate hours and minutes on the clock.

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

Table 10: Categorization of UMR non-lexicalized roles
</div>

For the roles that characterize the central participant(s) in the event,
the best way to decide which participant role label a given participant
should receive is to consider the semantic class of the event as specified in the middle column of table 10. The
```:undergoer``` role only occurs with
change-of-state events, construed broadly to include creation and
contact events as well. The ```:undergoer```
role is used for the entity that undergoes the change-of-state, is the
endpoint of force in a contact event, or is created in a creation event,
as seen in [\[3-2-1-1 (1)\]](#3-2-1-1 (1)). The ```:material```
role only occurs with creation events, as in
[\[3-2-1-1 (1c)\]](#3-2-1-1 (1c)), and is used for the raw materials
that are transformed into the created object.

<span id="3-2-1-1 (1)" label="3-2-1-1 (1)">\[3-2-1-1 (1)\]</span>

<span id="3-2-1-1 (1a)" label="3-2-1-1 (1a)">\[3-2-1-1 (1a)\]</span>
```
The ice cube melted.  
(m/ melt-01  
	:undergoer (c / cube
		:consist-of (i/ ice)
		:ref-number Singular)
	:aspect Performance
	:modstr FullAff)
```
<span id="3-2-1-1 (1b)" label="3-2-1-1 (1b)">\[3-2-1-1 (1b)\]</span> 
```
The enemy sank the ship. 
(s/ sink-01  
	:actor (e/ enemy) 
	:undergoer (s2/ ship
		:ref-number Singular)
	:aspect Performance
	:modstr FullAff)

```
<span id="#3-2-1-1 (1c)" label="#3-2-1-1 (1c)">\[#3-2-1-1 (1c)\]</span> 
```
She built a house out of wood. 
(b/ build-01  
	:actor (p/ person
		:ref-person 3rd
		:ref-number Singular)  
	:undergoer (h/ house
		:ref-number Singular) 
	:material (w/ wood)
	:aspect Performance
	:modstr FullAff)
```
<span id="#3-2-1-1 (1d)" label="#3-2-1-1 (1d)">\[#3-2-1-1 (1d)\]</span> 
```
He hit the stick against the fence.  
(h / hit-01
	:actor (p/ person
		:ref-person 3rd
		:ref-number Singular)  
	:instrument (s/ stick
		:ref-number Singular)  
	:undergoer (f / fence
		:ref-number Singular)
	:aspect Endeavor
	:modstr FullAff) 
```
The `:experiencer` and
`:stimulus` roles always occur with
experiential events, as seen in [\[3-2-1-1 (4)\]](#3-2-1-1 (4)). The
`:experiencer` role is used for the
mental-level entity which attends to, reacts to, or passively
experiences the `:stimulus` role.

<span id="3-2-1-1 (4)" label="3-2-1-1 (4)">\[3-2-1-1 (4)\]</span>

<span id="3-2-1-1 (4a)" label="3-2-1-1 (4a)">\[3-2-1-1 (4a)\]</span>
```
The audience listened to the concerto.  
(l/ listen-01
	:experiencer (a/ audience) 
	:stimulus (c / concerto
		:ref-number Singular)
	:aspect State
	:modstr FullAff)
```
<span id="3-2-1-1 (4b)" label="3-2-1-1 (4b)">\[3-2-1-1 (4b)\]</span>
```
The cat startled me.
(s/ startle-01  
	:experiencer (p/ person
		:ref-person 1st
		:ref-number Singular)
	:stimulus (c / cat
		:ref-number Singular)
	:aspect Performance
	:modstr FullAff) 
```
The `:start, :goal`, and
`:source` roles only occur with motion
events; `:place` has two different uses, one
with Motion/Location events and one with other event classes.
`:start`,
`:goal`, and
`:place` are used for locations –
`:start` is the location from which motion
originates, as in [\[3-2-1-1 (5a)\]](#[3-2-1-1 (5a)),
`:goal` is the location in which motion
ends, as in [\[[3-2-1-1 (5b)\]](#3-2-1-1 (5b)) and [\[3-2-1-1 (5c)\]](#3-2-1-1 (5c)),
and `:place` is used for static locations,
as in [\[3-2-1-1 (5d)\]](#3-2-1-1 (5d)). The
`:source` role is in the removal subclass of
motion events; it is used for the entity from which the
`:theme` is removed, as in
[\[3-2-1-1 (5e)\]](#3-2-1-1 (5e)). With motion events, the
`:theme` role is used for the entity that
moves (unless the motion is volitional), as in
[\[3-2-1-1 (5a)\]](#3-2-1-1 (5a)).

<span id="3-2-1-1 (5)" label="3-2-1-1 (5)">\[3-2-1-1 (5)\]</span>

<span id="[3-2-1-1 (5a)" label="[3-2-1-1 (5a)">\[[3-2-1-1 (5a)\]</span> 
```
She walked home from the store.
(w/ walk-01 
	:actor (p/ person
		:ref-person 3rd
		ref-number Singular)  
	:goal (h/ home)
	:start (s/ store)
	:aspect Performance
	:modstr FullAff)  
```
<span id="3-2-1-1 (5b)" label="3-2-1-1 (5b)">\[3-2-1-1 (5b)\]</span> 
```
The leaf fell to the ground.
(f/ fall-01 
	:theme (l/ leaf
		:ref-number Singular) 
	:goal (g/ ground)
	:aspect Performance
	:modstr FullAff)  
```
<span id="3-2-1-1 (5c)" label="3-2-1-1 (5c)">\[3-2-1-1 (5c)\]</span> 
```
He put the books in a box.
(p/ put-01  
	:actor (p/ person
		:ref-person 3rd
		:ref-number Singular)  
	:theme (b / book
		:ref-number Plural)  
	:goal (b2 / box
		:ref-number Singular)
	:aspect: Performance
	:modstr FullAff)  

```
<span id="3-2-1-1 (5d)" label="3-2-1-1 (5d)">\[3-2-1-1 (5d)\]</span> 
```
She is sitting on the couch.
(s/ sit-01  
	:actor (p/ person
		:ref-person 3rd
		:ref-number Singular)  
	:place (c/ couch
		:ref-number Singular)
	:aspect State
	:modstr FullAff)  
```
<span id="3-2-1-1 (5e)" label="3-2-1-1 (5e)">\[3-2-1-1 (5e)\]</span> 
```
He picked some berries from the bush.
(p/ pick-01
	:actor (p2/ person
		:ref-person 3rd
		:ref-number Singular) 
	:theme (b/ berry
		:ref-number Paucal)  
	:source (b2/ bush
		:ref-number Singular)
	:aspect Performance
	:modstr FullAff) 
```
The `:recipient` role only occurs with
transfer events, or metaphorical transfer events like communication.
With these events, the initiator of the transfer is an
`:actor`, the entity that is transferred is
the `:theme` and the entity that the
`:theme` is transferred to is labelled as
the `:recipient`. For transfer of possession
events that express the original possessor of the
`:theme`, the original possessor is
annotated as `:affectee`, as in
[\[3-2-1-1 (6d)\]](#3-2-1-1 (6d)).

<span id="3-2-1-1 (6)" label="3-2-1-1 (6)">\[3-2-1-1 (6)\]</span>

<span id="3-2-1-1 (6a)" label="3-2-1-1 (6a)">\[3-2-1-1 (6a)\]</span> 
```
He gave the cat some wet food.
(g/ give-01  
	:actor (p/ person
		:ref-person 3rd
		:ref-number Singular)  
	:theme (f/ food
		:mod (w/ wet)
		:quant (s/ some))  
	:recipient (c/ cat
		:ref-number Singular)
	:aspect Performance
	:modstr FullAff)
```

<span id="3-2-1-1 (6b)" label="3-2-1-1 (6b)">\[3-2-1-1 (6b)\]</span> 
```
I showed the pictures to her.
(s/ show-01  
	:actor (p/ person
		:ref-person 1st
		:ref-number Singular)  
	:theme (p2/ picture
		:ref-number Plural)
	:recipient (p3/ person
		:ref-person 3rd
		:ref-number Singular)
	:aspect Performance
	:modstr FullAff) 
```

<span id="3-2-1-1 (6c)" label="3-2-1-1 (6c)">\[3-2-1-1 (6c)\]</span> 
```
She told me that they they’re attending.
(t/ tell-01  
	:actor (p/ person
		:ref-person 3rd
		:ref-number Singular)    
	:theme (a/ attend-01  
		:actor (p2/ person
			:ref-person 3rd
			:ref-number Plural)
		:aspect Activity
		:quot t
		:modstr FullAff)
	:aspect Performance
	:modstr FullAff) 
```

<span id="3-2-1-1 (6d)" label="3-2-1-1 (6d)">\[3-2-1-1 (6d)\]</span> 
```
She stole the information from a competitor.
(s/ steal-01
	:actor (p/ person
		:ref-person 3rd
		:ref-number Singular)
	:theme (i/ information) 
	:source (c/ competitor
		:ref-number Singular)
	:aspect Performance
	:modstr FullAff) 
```

The other participant roles can occur pretty much freely with any semantic class of event. The external cause roles are used to annotate entities that bring about the central event. The
`:actor` role is used for “active”
single-participant events, in which the single participant acts
volitionally to bring about the event, as in
[\[3-2-1-1 (7a)\]](#3-2-1-1 (7a)). This contrasts with “inactive”
single-participant events, in which the single participant undergoes a
change outside of its control, as in [\[3-2-1-1 (1a)\]](#3-2-1-1 (1a))
above. See Appendix [8](#ap:verbspr) for examples of single-participant
verbs and their participant role annotation. The
`:actor` role is also used for animate
entities that initiate an action, as in [\[3-2-1-1 (1b)\]](#3-2-1-1 (1b))
above.

The `:companion` role is used for the entity
that helps the `:actor` bring about the
action, as in [\[3-2-1-1 (7b)\]](#3-2-1-1 (7b)). Note that this role is only annotated when the `:companion`
participant is expressed separately from the
`:actor`. Plural participants and conjoined
participants, as in [\[3-2-1-1 (7c)\]](#3-2-1-1 (7c)) and
[\[3-2-1-1 (7d)\]](#3-2-1-1 (7d)), are annotated with a single
`:actor` role. In some languages, a marker
may be ambiguous between a comitative marker and a conjunction. When the two participants are expressed separately in the clause, they should be treated as separate participants, annotated with `:actor` and `:companion`. When they are expressed
together, they are treated as a single
`:actor` participant.

The `:instrument` role is used for an entity
that is manipulated by one of the other external cause roles, often an `:actor`, in order to initiate the action.
The entity which manipulates the
`:instrument` may or may not be present in
the clause; see [\[3-2-1-1 (7e)\]](#3-2-1-1 (7e)) and
[\[3-2-1-1 (7f)\]](#3-2-1-1 (7f)).

The `:force` role is used for inanimate physical
entities which initiate an action, or cause another entity to undergo a
change, as in [\[3-2-1-1 (7g)\]](#3-2-1-1 (7g)). Finally, the
`:causer` role is used for the external
initiator in some causative constructions, see [4.1.2](#pr0:alts).


<span id="3-2-1-1 (7)" label="3-2-1-1 (7)">\[3-2-1-1 (7)\]</span>

<span id="3-2-1-1 (7a)" label="3-2-1-1 (7a)">\[3-2-1-1 (7a)\]</span>
```
He winked.
(w/ wink-01
	:actor (p/ person
		:ref-person 3rd
		:ref-number Singular)
	:aspect Endeavor
	:modstr FullAff)
```
<span id="3-2-1-1 (7b)" label="3-2-1-1 (7b)">\[3-2-1-1 (7b)\]</span> 
```
Jane wrote the paper with Chris.
(w/ write-01 
	:actor (p/ person
		:name (n/ name :op1 "Jane"))  
	:companion (p2/ person
		:name (n2/ name :op2 "Chris"))  
	:undergoer (p3 / paper
		:ref-number Singular)
	:aspect Performance
	:modstr FullAff) 
```

<span id="3-2-1-1 (7c)" label="3-2-1-1 (7c)">\[3-2-1-1 (7c)\]</span> 
```
They wrote the paper.
(w/ write-01  
	:actor (p/ person
		:ref-number Plural)
	:undergoer (p2/ paper
		:ref-number Singular)
	:aspect Performance
	:modstr FullAff)
```
<span id="3-2-1-1 (7d)" label="3-2-1-1 (7d)">\[3-2-1-1 (7d)\]</span> 
```
Jane and Chris wrote the paper.
(w/ write-01
	:actor (a/ and
		:op1 (p/ person
			:name (n/ name :op1 "Jane"))
		:op2 (p2/ person
			:name (n2/ name :op1 "Chris)))
	:undergoer (p3/ paper
		:ref-number Singular)
	:aspect Performance
	:modstr FullAff)  
```
<span id="3-2-1-1 (7e)" label="3-2-1-1 (7e)">\[3-2-1-1 (7e)\]</span> 
```
She sliced the bread with a knife.
(s/ slice-01
	:actor (p/ person
		:ref-person 3rd
		:ref-number Singular) 
	:instrument (k/ knife
		:ref-number Singular) 
	:undergoer (b/ bread
		:ref-number Singular)
	:aspect Performance
	:modstr FullAff)
```
<span id="3-2-1-1 (7f)" label="3-2-1-1 (7f)">\[3-2-1-1 (7f)\]</span>
```
The knife sliced through the bread.
(s/ slice-01 
	:instrument (k/ knife
		:ref-number Singular)  
	:undergoer (b/ bread
		:ref-number Singular)
	:aspect Performance
	:modstr FullAff) 
```
<span id="3-2-1-1 (7g)" label="3-2-1-1 (7g)">\[3-2-1-1 (7g)\]</span> 
```
The storm damaged the power lines.
(d/ damage-01 
	:force (s/ storm
		:ref-number Singular)  
	:undergoer (l/ line
		:purpose (p/ power)
		:ref-number Plural)
	:aspect Performance
	:modstr FullAff)
```
See Table 9 above for examples of the circumstantial
roles. In addition, there is an `:other`
placeholder role that can be used when annotators are unsure of which participant role annotation is accurate for a particular participant. Also see Appendix [8](#ap:verbspr) for a list of verbs and how their microroles are annotated.

At Stage 0, participant roles that aren’t explicitly expressed in the clause do not have to be annotated, even if they are implied by the context. If the annotator is certain about them, however, they can be annotated. For example, in [\[3-2-1-1 (8)\]](#3-2-1-1 (8)), the
`:goal` is left implicit on the left-hand side but annotated on the right-hand side; at Stage 0, this
role may be left out of the annotation.

<span id="3-2-1-1 (8)" label="3-2-1-1 (8)">\[3-2-1-1 (8)\]</span> 
```
They loaded the boxes.
(l/ load-01  					Or		(l/ load-01
	:actor (p/ person						:actor (p/ person
		:ref-person 3rd							:ref-person 3rd
		:ref-number Plural)  						:ref-number Plural)
	:theme (b/ box							:theme (b/ box
		:ref-number Plural)						:ref-number Plural)
	:aspect Performance						:goal (t/ thing)
	:modstr FullAff)						:aspect Performance
									:modstr FullAff)
```

[Back to Table of Contents](#toc)

###### Part 3-2-1-1-1. Nonverbal clauses

There is a small set of predicates that use lexicalized roles at all stages of the road map; therefore, frame files for these predicates are created at Stage 0 annotation. These are the nonverbal clause predicates shown in Table 11 (see also [Part 3-1-1-3](#part-3-1-1-3-states-and-entities) and [Part 3-1-3-5](#Part-3-1-3-5-Non-verbal-clauses)). These are repeated below with their participant role annotation.

Each nonverbal clause predicate has a set of numbered argument roles which map
to the semantic roles as shown in Table 11.

<div id="tab:nonverbal_arguments">
	
| **Clause Type**        | **Predicate**    | **ARG0**  | **ARG1**         | **ARG2**         |
| :--------------------- | :--------------- | :-------- | :--------------- | :--------------- |
| Thetic Possession      | have-91          | possessor | possessum        | ---              |
| Predicative Possession | belong-91        | possessum | possessor        | ---              |
| Thetic Location        | exist-91         | location  | theme            | ---              |
| Predicative Location   | have-location-91 | theme     | location         | ---              |
| Property Predication   | have-mod-91      | ---       | theme            | property         |
| Object Predication     | have-role-91     | theme     | reference point  | object category  |
|                        | have-org-role-91 | theme     | organization     | role             |
|                        | kinship-91       | theme     | family member    | kinship rel.     |
| Equational             | identity-91      | theme     | equated referent | ---              |

Table 11: Argument structure of non-verbal clause predicates
</div>

The argument that can be predicativized in languages using the predicativized-argument strategy is always
the argument role with the highest number. The examples in [\[3-2-1-1-1 (1)\]](#3-2-1-1-1 (1)) show how
nonverbal clauses are annotated with participant roles. Note that these
annotations will be the same at every stage of the road map.

<span id="3-2-1-1-1 (1)" label="3-2-1-1-1 (1)">\[3-2-1-1-1 (1)\]</span>

<span id="3-2-1-1-1 (1a)" label="3-2-1-1-1 (1a)">\[3-2-1-1-1 (1a)\]</span>
Thetic/presentational Possession - Kukama <br />

```
Mijiri-tin  ɨara-yara  
Miguel-CER  canoe-owner  
‘Miguel does have a canoe.’ (Lit. ‘Miguel is a canoe-owner’)

(h/ have-91
	:ARG0 (p/ person
		:name (n/ name :op1 "Mijiri")) 
	:ARG1 (i/ ɨarayara ‘canoe’
		:ref-number Singular)
	:aspect State
	:modstr FullAff) 
```
<span id="3-2-1-1-1 (1b)" label="3-2-1-1-1 (1b)">\[3-2-1-1-1 (1b)\]</span> Predicative
Possession - English <br />
```
The dog belongs to the teacher.  
  
(b/ belong-91
	:ARG0 (d/ dog
		:ref-number Singular) 
	:ARG1 (t/ teacher
		:ref-number Singular)
	:aspect State
	:modstr FullAff) 
```
<span id="3-2-1-1-1 (1c)" label="3-2-1-1-1 (1c)">\[3-2-1-1-1 (1c)\]</span> Thetic/presentational Location - English <br />
```
On the rock was a symbol.  
  
(e/ exist-91
	:ARG0 (r/ rock
		:ref-number Singular)
	:ARG1 (s/ symbol
		:ref-number Singular)
	:aspect State
	:modstr FullAff)  
```
<span id="3-2-1-1-1 (1d)" label="3-2-1-1-1 (1d)">\[3-2-1-1-1 (1d)\]</span> Predicative
Location - Yabem (Dempwolff 1939) <br />
```
àndu  kê-kô 	malac  
house 3SG-be.at village  
‘The house is in the village.’
(h/ have-location-91
	:ARG0 (a/ àndu ‘house’
		:ref-number Singular)
	:ARG1 (m/ malac ‘village’
		:ref-number Singular)
	:aspect State
	:modstr FullAff)
```
<span id="3-2-1-1-1 (1e)" label="3-2-1-1-1 (1e)">\[3-2-1-1-1 (1e)\]</span> Property
Predication - English <br />
```
The cat is black.  
(h/ have-mod-91
	:ARG1 (c/ cat
		:ref-number Singular) 
	:ARG2 (b/ black)
	:aspect State
	:modstr FullAff)  
```
<span id="3-2-1-1-1 (1f)" label="3-2-1-1-1 (1f)">\[3-2-1-1-1 (1f)\]</span> Object Predication - Kukama <br />
```
ajan kunumi 	tsumi  
this young.man 	shaman  
‘This young man is a shaman.’
(h/ have-role-91
	:ARG0 (k/ kunumi ‘young man’
		:mod (a/ ajan 'this')
		:ref-number Singular)
	:ARG2 (t/ tsumi ‘shaman’)
	:aspect State
	:modstr FullAff)  
```
<span id="3-2-1-1-1 (1g)" label="3-2-1-1-1 (1g)">\[3-2-1-1-1 (1g)\]</span> Object Equational - English <br />
```
She is the winner.  
(i/ identity-91
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Singular) 
	:ARG1 (p2/ person
		:ARG0-of (w/ win-01))
	:aspect State
	:modstr FullAff)
```

[Back to Table of Contents](#toc)

###### Part 3-2-1-1-2. Valency alternations
 
Certain types of semantic valency alternations are reflected in the participant role annotation. At Stage 0, these alternations influence the choice of general participant role labels. For information-packaging alternations, such as
passives, antipassives, or valency-rearranging applicatives,
participants are annotated in the same way as in the basic construction
in the language. If a participant is omitted, for example the agent in a passive construction as in [\[3-2-1-1-2 (1)\]](#3-2-1-1-2 (1)) from Berber (Guerssel 1986:52), then it simply isn’t annotated at Stage 0. This means that agentless passives and anticausatives will have the same participant role annotation at Stage 0. 

<span id="3-2-1-1-2 (1)" label="3-2-1-1-2 (1)">\[3-2-1-1-2 (1)\]</span>

<span id="3-2-1-1-2 (1a)" label="3-2-1-1-2 (1a)">\[3-2-1-1-2 (1a)\]</span> <br />
```
Y-usy 		wrba 	tafirast.  
3M.SG-pick.up 	boy:CST	pear  
‘The boy picked up the pear.’
(u/ yusy-00 ‘pick up’  
	:actor (w/ wrba ‘boy’
		:ref-number Singular) 
	:undergoer (t/ tafirast ‘pear’
		:ref-number Singular)
	:aspect Performance
	:modstr FullAff)
```

<span id="3-2-1-1-2 (1b)" label="3-2-1-1-2 (1b)">\[3-2-1-1-2 (1b)\]</span> <br />
```
T-ttw-asy		tfirast.  
3F.SG-DETR-pick.up	pear  
‘The pear was picked up.’
(t/ tttwasy-00 ‘pick up’  
	:undergoer (t2/ tafirast ‘pear’
		:ref-number Singular)
	:aspect Performance
	:modstr FullAff) 
```

**Causatives.** There are a few different types of causatives that
require different annotation solutions. For most causatives of
transitives, the causer is annotated as
`:causer`, the causee as
`:actor`, and the rest of the participants
receive the same annotation labels that they would in a a non-causative
construction. In [\[3-2-1-1-2 (2)\]](#3-2-1-1-2 (2)) from Kukama, *nai*
‘grandmother’ is annotated as `:causer`,
the causee *churan* ‘kid’ is annotated as
`:actor`, and *uni* ‘water’ as `:undergoer`.

<span id="3-2-1-1-2 (2)" label="3-2-1-1-2 (2)">\[3-2-1-1-2 (2)\]</span>
```
nai 		kurata-ta	churan=ui	uni=pu  
grandmother 	drink-CAUS	kid=PST 	water=INS 
‘Grandmother made the kid drink the water.’
(k/ kuratata 'make drink'
    :causer (p/ person
    	:ARG0-of (k2/ kinship-91
		:ARG2 (n/ nai 'grandmother'))
	:ref-number Singular)
    :actor (c/ churan 'kid')
    :undergoer (u/ uni 'water')
    :aspect Performance
    :modstr FullAff)  
```

There are certain causatives of transitives which do not use the `:causer` role. These are constructions which express transfer events, including mental/cognitive transfer. Some
languages express these types of events with monomorphemic verbs, like English, but other languages use causatives of transitive verbs.
Languages may differ in terms of which types of causative constructions are construed as transfer; in order to annotate the same semantic events in the same way across languages, the `:actor, :theme, :recipient` roles are used for transfer of possession (giving), sending, and mental transfer, which includes showing and communication. Bezhta in [\[3-2-1-1-2 (3b)\]](#3-2-1-1-2 (3b)) (Comrie, Khalilov, Khalilova 2015:560) uses the causative of *b-egā-yo* ‘see’ as equivalent to English *show*.


<span id="3-2-1-1-2 (3)" label="3-2-1-1-2 (3)">\[3-2-1-1-2 (3)\]</span>

<span id="3-2-1-1-2 (3a)" label="3-2-1-1-2 (3a)">\[3-2-1-1-2 (3a)\]</span> <br />
```
hogco-l 	raɬad 		b-egā-yo  
he.OBL-LAT 	sea(iii) 	iii-see-PST  
‘He saw the sea.’ 
(b/ begāyo-00 ‘see’
	:experiencer (p/ person
		:ref-person 3rd
		:ref-number Singular)
	:stimulus (r/ raɬad ‘sea’)
	:aspect State
	:modstr FullAff)

```
<span id="3-2-1-1-2 (3b)" label="3-2-1-1-2 (3b)">\[3-2-1-1-2 (3b)\]</span>
```
hogco 		kibba-l 	raɬad 		b-ega-l-lo  
he.OBL(ERG) 	girl.OBL-LAT 	sea(iii) 	iii-see-CAUS-PST 
‘He showed the sea to the girl.’
(b/ begallo-00 ‘show’
	:actor (p/ person
		:ref-person 3rd
		:ref-number Singular)
	:theme (r/ raɬad ‘sea’)
	:recipient (k/ kibba ‘girl’
		:ref-number Singular)
	:aspect Performance
	:modstr FullAff)
```

For causatives of ditransitives, the causer receives the
`:causer` role, the causee the `:actor` role, and the other participants receive the same annotation as in a non-causative construction. This can be seen in [\[3-2-1-1-2 (4)\]](#3-2-1-1-2 (4)) from Shipibo-Konibo
(Valenzuela 2003:612). If ‘the man’ was expressed in the clause, that participant would be annotated as `:recipient`.


<span id="3-2-1-1-2 (4)" label="3-2-1-1-2 (4)">\[3-2-1-1-2 (4)\]</span> <br />
```
Ja-tian 	ja 	xontako 		jawen 	tita-n 		xoi 			meni-ma-\[a\]i 	keen-yama-\[a\]i-bi...  
that-TEMP 	that 	unmarried.girl:ABS 	POS3 	mother-ERG 	roasted.meat/fish:ABS 	give-CAUS-INC 	want-NEG-SDS-EM  
‘Then her mother makes the unmarried girl give roasted meat/fish (to the
man who had asked her in matrimony) even though she doesn’t want to...’
(m/ menima-00 'make give'
	:causer (p/ person
		:ARG0-of (k/ kinship-91
			:ARG1 (x/ xontako 'unmarried girl'
				:mod (j/ ja 'that')
				:ref-number Singular)
			:ARG2 (t/ titan 'mother'))
			:ref-number Singular)
	:actor x
	:theme (x2/ xoi 'roasted meat/fish')
	:temporal (j2/ jatian 'that time')
	:concession (k2/ keenyamaaibi-00 'want'
		:experiencer x
		:stimulus (m
			:modpred k2)
		:aspect State
		:modstr FullNeg)
	:aspect Habitual
	:modstr FullAff)
```

There are two types of causatives of intransitives, based on the two types of intransitives. For intransitives whose single participant corresponds to an `:undergoer` role, such as
change-of-state verbs in many languages, the causer is annotated as `:actor` and the single participant retains
its `:undergoer` label. This can be seen in
[\[3-2-1-1-2 (5)\]](#3-2-1-1-2 (5)) from Falam Chin (King 2011:195) below.


<span id="3-2-1-1-2 (5)" label="3-2-1-1-2 (5)">\[3-2-1-1-2 (5)\]</span>

<span id="3-2-1-1-2 (5a)" label="3-2-1-1-2 (5a)">\[3-2-1-1-2 (5a)\]</span> <br /> 
```
Ka 	kedam 	hri	a 	cat.  
1SG 	shoe 	string	3SG.NOM	broken.1  
‘My shoelace is broken/broke.’
(c/ cat-00 ‘broken’ 
	:undergoer (h/ hri 'string'
		:part-of (k/ kedam 'shoe')
		:poss (p/ person
			:ref-person 1st
			:ref-number Singular)
		:ref-number Singular)
	:aspect State
	:modstr FullAff)
```

<span id="3-2-1-1-2 (5b)" label="3-2-1-1-2 (5b)">\[3-2-1-1-2 (5b)\]</span> <br /> 
```
Thangte in 	ka 	kedam 	hri 	a 	cat-ter.  
Thangte ERG 	1SG 	shoe 	string 	3SG.NOM broken.1-CAUS  
‘Thangte broke my shoelace.’
(c/ catter-00 ‘break’  
	:actor (p/ person
		:name (n/ name :op1 "Thangte"))
	:undergoer (h/ hri 'string'
		:part-of (k/ kedam 'shoe')
		:poss (p2/ person
			:ref-person 1st
			:ref-number Singular)
		:ref-number Singular
	:aspect Performance
	:modstr FullAff)
```

Regardless of whether the causative or anticausative verb is derived (or if neither is derived), the anticausative/intransitive meaning is annotated with a single `:undergoer` participant and the causative/transitive meaning is annotated with an
`:actor` and an `:undergoer` participant.

When the single participant of the intransitive corresponds to the
`:actor` role, then the causer receives the `:causer` annotation and the single participant retains its `:actor` label. This
can be seen in [\[3-2-1-1-2 (6)\]](#3-2-1-1-2 (6)) from Falam Chin (King 2011:195) below.

<span id="3-2-1-1-2 (6)" label="3-2-1-1-2 (6)">\[3-2-1-1-2 (6)\]</span>

<span id="3-2-1-1-2 (6a)" label="3-2-1-1-2 (6a)">\[3-2-1-1-2 (6a)\]</span> <br />
```
Cinte a 	hni.  
Cinte 3SG.NOM 	laugh.1  
‘Cinte laughed.’ 
(h/ hni-00 ‘laugh’
	:actor (p/ person
		:name (n/ name :op1 "Cinte"))
	:aspect Endeavor
	:modstr FullAff)
```
<span id="3-2-1-1-2 (6a)" label="3-2-1-1-2 (6a)">\[3-2-1-1-2 (6a)\]</span> <br /> 
```
Parte 	in 	Cinte a 	hni-ter.  
Parte 	ERG 	Cinte 3SG.NOM 	laugh.1-CAUS  
‘Parte made Cinte laugh.’
(h/ hniter-00 ‘make laugh’ 
	:causer (p/ person
		:name (n/ name :op1 "Parte")) 
	:actor (p2/ person
		:name (n2/ name :op1 "Cinte"))  
	:aspect Performance
	:modstr FullAff)
```

**Applicatives.**  Peterson (2007) distinguishes between “valency-increasing” applicatives and “valency-rearranging” applicatives. In valency-rearranging applicatives, a participant is expressed as an oblique in the basic construction and expressed as a core argument in the applicative construction; they are generally associated with the increased saliency or topicality of the oblique participant. Therefore, these fit into the category of pragmatic valency alternations, and both the basic and applicative construction receive the same participant role
annotation. This can be seen in
[\[3-2-1-1-2 (7)\]](#3-2-1-1-2 (7)) from Falam Chin (King 2011:240).

<span id="3-2-1-1-2 (7)" label="3-2-1-1-2 (7)">\[3-2-1-1-2 (7)\]</span>

<span id="3-2-1-1-2 (7a)" label="3-2-1-1-2 (7a)">\[3-2-1-1-2 (7a)\]</span>
```
Parte in 	Thangte hrang=ah 	hmeh 	a 	suang.  
Parte ERG 	Thangte for=LOC 	curry 	3SG.NOM cook.1  
‘Parte cooked some curry for Thangte.’
(s/ suang-00 ‘cook’
	:actor (p/ person
		:name (n/ name :op1 "Parte"))
	:undergoer (h/ hmeh ‘curry’) 
	:affectee (p2/ person
		:name (n2/ name :op2 "Thangte"))
	:aspect Performance
	:modstr FullAff)
```
<span id="3-2-1-1-2 (7b)" label="3-2-1-1-2 (7b)">\[3-2-1-1-2 (7b)\]</span>
```
Parte in 	Thangte hmeh 	a 	suan-sak  
Parte ERG 	Thangte curry 	3SG.NOM cook.2-BEN  
‘Parte cooked Thangte some curry.’
(s/ suangsak-00 ‘cook for’
	:actor (p/ person
		:name (n/ name :op1 "Parte"))
	:undergoer (h/ hmeh ‘curry’) 
	:affectee (p2/ person
		:name (n2/ name :op1 "Thangte"))
	:aspect Performance
	:modstr FullAff)
```
<span id="3-2-1-1-2 (7c)" label="3-2-1-1-2 (7c)">\[3-2-1-1-2 (7c)\]</span>
```
as-teny-aye'	pa'ang
1SG-buy-DECL	palm
‘I bought palm hearts.’
(t/ entenyay'a-00
	:actor (p/ person
		:ref-person 1st
		:ref-number Singular)
	:theme (p2/ pa'ang 'palm)
	:aspect Performance
	:modstr FullAff)
```
<span id="3-2-1-1-2 (7d)" label="3-2-1-1-2 (7d)">\[3-2-1-1-2 (7d)\]</span>
```
as-teny-as-ke'		pa'ang	ap-angkok	Eduardo
1SG-buy-APPL-DECL	palm  	2/3M-POSS	Eduardo
‘I bought palm hearts from Eduardo.’
(t/ entenyaskama-00
	:actor (p/ person
		:ref-person 1st
		:ref-number Singular)
	:theme (p2/ pa'ang 'palm)
	:source (p3/ person
		:name (n/ name :op1 "Eduardo"))
	:aspect Performance
	:modstr FullAff)
```

Whether the beneficiary, *Thangte*, is expressed as an oblique or a core argument, it is annotated as `:affectee`. Valency-increasing applicatives involve the addition of a participant, compared to the basic construction. Here, the added participant is
simply annotated with the appropriate semantic role. This can be seen in [\[3-2-1-1-2 (7c)\]](#3-2-1-1-2 (7c))-[\[3-2-1-1-2 (7d)\]](#3-2-1-1-2 (7d)) from Sanapaná.

**Reflexives & Reciprocals** For reflexive and reciprocal constructions, the single participant is annotated with both of the semantic role labels which it is fulfilling in the construction. This can be seen in [\[3-2-1-1-2 (8a)\]](#3-2-1-1-2 (8a)) and [\[3-2-1-1-2 (8b)\]](#3-2-1-1-2 (8b)) from Supyire (Carlson 1994:416-7).

<span id="3-2-1-1-2 (8)" label="3-2-1-1-2 (8)">\[3-2-1-1-2 (8)\]</span>

<span id="3-2-1-1-2 (8a)" label="3-2-1-1-2 (8a)">\[3-2-1-1-2 (8a)\]</span>
```
U 	a 	ù-yé 	bánì  
he 	PERF 	he-REFL wound  
‘He has wounded himself.’
(b/ bánì-00 ‘wound’ 
	:actor (p/ person
		:ref-person 3rd
		:ref-number Singular) 
	:undergoer p
	:aspect Performance
	:modstr FullAff)
```
<span id="3-2-1-1-2 (8b)" label="3-2-1-1-2 (8b)">\[3-2-1-1-2 (8b)\]</span><br /> 
```
Pi 	a 	pì-yé 		kánù  
they 	PERF	they-REFL 	love  
‘They loved each other.’
(k/ kánù-00 ‘love’
	:actor (p/ person
		:ref-person 3rd
		:ref-number Plural)
	:undergoer p
	:aspect State
	:modstr FullAff)
```

The annotation of participant roles for valency alternations in Step 1 of the road map is summarized in table 12 below.

<div id="tab:valency_alternations">

| **Valency Alternation**                  | **Which participants to annotate** | **Which participant roles**     |
| :----------------------------------------- | :------------------------------------ | :------------------------------------------------------------------------ |
| Passives | Every overt participant | Same as in basic construction |
| Anticausatives | Every overt participant | Same as in basic construction |
| Valency-rearranging applicatives | Every overt participant | Same as in basic construction |
| Causatives of transitives | Every overt participant | `:causer`, `:actor`, other participants same as in basic construction |
| Transfer events expressed as causatives | Every overt participant | `:actor`, `:theme`, `:recipient` |
| Causatives of ditransitives | Every overt participant | `:causer`, `:actor`, `:theme`, `:recipient` |
| Causatives of inactive intransitives | Every overt participant | `:actor`, `:theme` |
| Causatives of active intransitives | Every overt participant | `:causer`, `:actor` |
| Valency-increasing applicatives | Every overt participant | Same as in basic construction, appropriate role for new participant |
| Reflexives | A single participant with two roles | Both roles the participant fulfills in the construction |
| Reciprocals | A single participant with two roles | Both roles the participant fulfills in the construction |

Table 2: Argument structure of valency alternations
</div>

[Back to Table of Contents](#toc)

##### Part 3-2-1-2. Stage 1

The Stage 1 participant role annotation requires access to
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

(t/ tease.02
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Singular)
	:ARG1 (b/ boy
		:ref-number Singular)
	:ARG2 (h/ hat
		:poss b)
	:aspect Endeavor
	:modstr FullAff)
```

Since the nonverbal clause functions require the use of lexicalized predicates at Stage 0, these are annotated in the same way at Stage 1 (see [Part 3-2-1-1-1](#part-3-2-1-1-1-nonverbal-clauses)). Unlike Stage 0, implicit participants are
annotated for their semantic role at Stage 1. This is shown in
[\[3-2-1-2 (2)\]](#3-2-1-2 (2)).

<span id="3-2-1-2 (2)" label="3-2-1-2 (2)">\[3-2-1-2 (2)\]</span> 
```
She parked the truck in the driveway. They loaded the boxes.

(s1p/ park-01
	:ARG0 (s1p2/ person
		:ref-person 3rd
		:ref-number Singular)
	:ARG1 (s1t/ truck
		:ref-number Singular)
	:ARG2 (s1d/ driveway)
	:aspect Performance
	:modstr FullAff) 

(s2l/ load-01
	:ARG0 (s2p/ person
		:ref-person 3rd
		:ref-number Plural)
	:ARG1 (s2t/ thing)  
	:ARG2 (s2b/ box
		:ref-number Plural)
	:aspect Performance
	:modstr FullAff)
(s2/ sentence
	:temporal (DCT :before s2l)
	:modal (AUTH :FullAff s2l)
	:coref (s1t :same-entity s2t))
```

The second sentence in [\[3-2-1-2 (2)\]](#3-2-1-2 (2)) does not
include explicit mention of the truck, but it is understood from the
context that the truck is the goal participant of the loading event. Therefore, an implicit `thing' participant is identified for the ```:ARG1``` role of the loading event at Stage 1. In the document-level annotation, this participant is then flagged as coreferential with the truck in the previous sentence.

[Back to Table of Contents](#toc)

###### Part 3-2-1-2-1. Valency alternations

The approach to valency alternations at Stage 1 is largely the same as
that detailed for Stage 0 in [Part 3-2-1-1-2](#part-3-2-1-1-2-valency-alternations). However, at Stage 1,
predicates with valency-changing morphology should have their own frame
files with lexicalized arguments. Therefore, the annotation of
participant roles for valency alternations is the same as that for other
types of predicates. The predicate is matched with its frame files and
the participants are annotated accordingly with numbered argument roles rather than predicate-general ones.


[Back to Table of Contents](#toc)

##### Part 3-2-1-3. Inverse participant roles

AMR, the predecessor of UMR, makes use of **inverse** participant roles for a number of different purposes, such as the annotation of events that function as modifiers of referring expressions (typically relative clauses or participles, see [Part 3-1-1-2](#part-3-1-1-2-processes-in-modification-and-reference)), the annotation of embedded interrogatives, and the annotation of participant nominalizations. These three uses of inverse participant roles are illustrated in [\[3-2-1-3 (1)\]](#3-2-1-3 (1)). The use of, for example, the `:ARG1-of` relation in [\[3-2-1-3 (1a)\]](#3-2-1-3 (1a)), which is the inverse of the numbered argument role `:ARG1`, allows us to maintain a single-rooted graph structure by embedding the *see*-event underneath the participant it modifies (*sweater*). Such event concept nodes which are linked to other concepts by means of inverse participant roles can then further take their own full argument structure annotation and attribute values for e.g. aspect. Such inverses of numbered argument roles also allow us to make use of PropBank framefiles as much as possible: by annotating *runner* in [\[3-2-1-3 (1c)\]](#3-2-1-3 (1c)) as `(p/ person :ARG0-of r/ run-02)`, we can directly link this annotation to the existing lexicon rather than having to enter an ad-hoc object concept node `(r/ runner)`.

<span id="3-2-1-3 (1)" label="3-2-1-3 (1)">\[3-2-1-3 (1)\]</span>

<span id="3-2-1-3 (1a)" label="3-2-1-3 (1a)">\[3-2-1-3 (1a)\]</span> 
```
I bought the sweater that you saw.
(b/ buy-0101
	:ARG0 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:ARG1 (s/ sweater
		:ARG1-of (s2/ see-01
			:ARG0 (p2/ person
				:ref-person 2nd
				:ref-number Singular)
			:aspect State
			:modstr FullAff)
		:ref-number Singular)
	:aspect Performance
	:modstr FullAff)
```

<span id="3-2-1-3 (1b)" label="3-2-1-3 (1b)">\[3-2-1-3 (1b)\]</span> 
```
I didn't see whether he bought the sweater.
(s/ see-01
	:ARG0 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:ARG1 (t/ truth-value
		:Polarity-of (b/ buy-01
			:ARG0 (p2/ person
				:ref-person 3rd
				:ref-number Singular)
			:ARG1 (s2/ sweater
				:ref-number Singular)
			:aspect Performance
			:modstr NeutAff))
	:Aspect State
	:Modstr FullNeg)
```

<span id="3-2-1-3 (1c)" label="3-2-1-3 (1c)">\[3-2-1-3 (1c)\]</span> 
```
The runner was wearing a sweater.
(w/ wear-01
	:ARG0 (p/ person
		:ARG0-of (r/ run-02)
		:ref-number Singular)
	:ARG1 (s/ sweater
		:ref-number Singular)
	:aspect State
	:modstr FullAff)
```

UMR expands upon this AMR system of inverse relations by adding inverses for the general (i.e. non-predicate-specific) participant roles to be used at stage 0 of the road map. So, in addition to having inverses of numbered participant roles, there are now also `:Actor-of` and `:Undergoer-of` roles, and analogues for each of the general participant roles described in table 9 in [Part 3-2-1-1](#part-3-2-1-1-stage-0)). Example [\[3-2-1-3 (1a)\]](#3-2-1-3 (2)) below illustrates the use of the inverse `:Stimulus-of` role to annotate the same relative clause as in [\[3-2-1-3 (1a)\]](#3-2-1-3 (1a)) above.

<span id="3-2-1-3 (2)" label="3-2-1-3 (2)">\[3-2-1-3 (2)\]</span> 

```
I bought the sweater that you saw.
(b/ buy-01
	:actor (p/ person
		:ref-person 1st
		:ref-number Singular)
	:theme (s/ sweater
		:Stimulus-of (s2/ see-01
			:experiencer (p2/ person
				:ref-person 2nd
				:ref-number Singular)
			:aspect State
			:modstr FullAff)
		:ref-number Singular)
	:aspect Performance
	:modstr FullAff)
```

One more context in which inverse participant roles are used is in the annotation of certain relations that are mostly thought of (and mostly expressed in languages) as nominal modification - specifically, kinship relations and certain other relational nouns, e.g. those designating functions within organizations. For the annotation of noun phrases like *my father*, or *the President of the University of New Mexico*, UMR uses a `(p/ person)` concept node as the top of the graph, connected with an inverse participant role to a non-verbal clause predicate (which can then take further argument roles to express other elements in the NP). The most general, coarse-grained non-verbal clause predicate to be used in such annotations is `have-role-91`, although more specific predicates (e.g. `kinship-91, have-org-role-91`) for frequently encountered concrete relation types are also available. The rolesets used for their arguments are detailed in [Part 3-1-3-5](#part-3-1-3-5-non-verbal-clauses)). The use of these predicates in such annotations is illustrated in [\[3-2-1-3 (3)\]](#3-2-1-3 (3)).
  
<span id="3-2-1-3 (3)" label="3-2-1-3 (3)">\[3-2-1-3 (3)\]</span> 

<span id="3-2-1-3 (3a)" label="3-2-1-3 (3a)">\[3-2-1-3 (3a)\]</span> 
```
I met my father.
(m/ meet-03
	:ARG0 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:ARG1 (p2/ person
		:ARG0-of (k/ kinship-91
			:ARG1 p
			:ARG2 (f/ father)))
	:aspect Performance
	:modstr FullAff)
```
<span id="3-2-1-3 (3a)" label="3-2-1-3 (3a)">\[3-2-1-3 (3a)\]</span> 
```
I met the President of the University of New Mexico.
(m/ meet-03
	:ARG0 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:ARG1 (p2/ person
		:ARG0-of (h/ have-org-role-91
			:ARG1 (a/ academic_organization
				:name (n/ name
					:op1 "University
					:op2 "of"
					:op3 "New"
					:op4 "Mexico")
				:wiki "University_of_New_Mexico")
			:ARG2 (p3/ president)))
	:aspect Performance
	:modstr FullAff)
```
[Back to Table of Contents](#toc)

##### Part 3-2-1-4. Table of verb meanings

Table X below contains the general participant role annotation for the microroles associated with 89 verb meanings. The verb meanings and microroles are from the Valency Patterns Leipzig project (ValPaL; Hartmann et al. 2013). For two verb meanings, WIPE and PEEL, the ValPaL data reflects distinct verb senses: a motion sense (ex: She wiped the crumbs from the table) and a change-of-state (COS) sense (ex: He wiped the table). 

As mentioned in [Part 3-2-1-1](#part-3-2-1-1-stage-0), the single participant in a monovalent event can either be annotated as <span class="smallcaps">`actor`</span> or as <span class="smallcaps">`undergoer`</span>. This distinction depends on the amount of control that the single participant has in carrying out the event. For events that are more controlled by the participant ("active" events), the participant is annotated as <span class="smallcaps">`actor`</span>; for events that are less controlled by the participant ("inactive" events), the participant is annotated as <span class="smallcaps">`undergoer`</span>. Languages that reflect this distinction in their morphosyntax (i.e., languages with active alignment) do not always draw the distinction between active events and inactive events in the same place. There is, however, a cross-linguistic organization in terms of how languages with active alignment code these events in their morphosyntax.

The following semantic event classes reflect an ordering from most active to most inactive (Croft 2012; Croft to appear).

Controlled activities (ex: run)  
Position events (ex: hang)  
Inherent properties (ex: short)  
Bodily actions (ex: cough)  
Change of state (ex: become ill)  
Transitory properties (ex: be ill)  
Uncontrolled activities (ex: fall)  

For the purposes of UMR, controlled activities, position events, inherent properties, and more controlled types of bodily actions (ex: laugh) are annotated with an <span class="smallcaps">`actor`</span> participant. Less controlled types of bodily actions (ex: cry) and the remaining semantic event classes are annotated with an <span class="smallcaps">`undergoer`</span> participant.

Annotators may use Table X as a reference point for annotating general participant roles for various semantic verb classes.

<div id="tab:predicateroles">


| **Verb Meaning** | **Microrole** | **UMR annotation** |
| :--------------------- | :--------------- | :-------- | 
|**Active (A-like) S** | | |
| RUN	| runner | <span class="smallcaps">`actor`</span> |
| CLIMB | climber | <span class="smallcaps">`actor`</span> |
| 		| climbing goal | <span class="smallcaps">`undergoer`</span> |
| JUMP | jumper | <span class="smallcaps">`actor`</span> |
| GO | goer | <span class="smallcaps">`actor`</span> |
|	| going goal | <span class="smallcaps">`goal`</span> |
| LEAVE | leaver | <span class="smallcaps">`actor`</span> |
|		| left place/person | <span class="smallcaps">`source`</span> |
| SIT DOWN | sit downer | <span class="smallcaps">`actor`</span> |
|		| sitting-down place  | <span class="smallcaps">`goal`</span> |
| DIG | digger | <span class="smallcaps">`actor`</span> |
| PLAY | player | <span class="smallcaps">`actor`</span> |
| SING | singer | <span class="smallcaps">`actor`</span> |
| SIT | sitter | <span class="smallcaps">`actor`</span> |
|		| sitting place  | <span class="smallcaps">`place`</span>  |
| LIVE | liver | <span class="smallcaps">`actor`</span> |
|	| living place  | <span class="smallcaps">`place`</span>  |
| LAUGH | laugher | <span class="smallcaps">`actor`</span> |
| BLINK | blinker | <span class="smallcaps">`actor`</span> |
| COUGH | cougher | <span class="smallcaps">`actor`</span> |
| **Inactive (P-like) S**  | | |
| CRY | crier | <span class="smallcaps">`undergoer`</span> |
| DIE | dieer | <span class="smallcaps">`undergoer`</span> |
| SINK | sunken entity | <span class="smallcaps">`undergoer`</span> |
| BURN | burnt thing | <span class="smallcaps">`undergoer`</span> |
| BOIL | boiled thing | <span class="smallcaps">`undergoer`</span> |
| BE SAD | sad person | <span class="smallcaps">`undergoer`</span> |
| BE HUNGRY | hungry person | <span class="smallcaps">`undergoer`</span>|
| BE DRY | dry thing | <span class="smallcaps">`undergoer`</span> |
| BE ILL | sick person | <span class="smallcaps">`undergoer`</span> |
| ROLL | rolling entity | <span class="smallcaps">`undergoer`</span> |
| FALL | fallee | <span class="smallcaps">`undergoer`</span> |
| RAIN | rain | <span class="smallcaps">`undergoer`</span> |
| **Reflexive/Reciprocal** | | |
| DRESS | dresser | <span class="smallcaps">`actor`</span> |
|		| dressee | <span class="smallcaps">`undergoer`</span> |
| SHAVE (a body part) | shaver (of body part) | <span class="smallcaps">`actor`</span> |
|	| shaved body part | <span class="smallcaps">`undergoer`</span> |
| WASH | washer | <span class="smallcaps">`actor`</span> |
|		| washed entity | <span class="smallcaps">`undergoer`</span> |
| HELP | helper | <span class="smallcaps">`actor`</span> |
|		| helpee | <span class="smallcaps">`undergoer`</span> |
| FOLLOW | follower | <span class="smallcaps">`actor`</span> |
|		| followee | <span class="smallcaps">`undergoer`</span> |
| MEET | meeter | <span class="smallcaps">`actor`</span> |
|		| met person | <span class="smallcaps">`undergoer`</span> |
| HUG | hugger | <span class="smallcaps">`actor`</span> |
|	| huggee  | <span class="smallcaps">`undergoer`</span> |
| **Change-of-State** | | |
| BREAK | breaker | <span class="smallcaps">`actor`</span> |
|		| broken thing | <span class="smallcaps">`undergoer`</span> |
|		| breaking instrument | <span class="smallcaps">`instrument`</span> |
| KILL | killer | <span class="smallcaps">`actor`</span> |
|		| killee | <span class="smallcaps">`undergoer`</span> |
|		| killing instrument | <span class="smallcaps">`instrument`</span> |
| BEAT | beater | <span class="smallcaps">`actor`</span> |
|		| beatee | <span class="smallcaps">`undergoer`</span> |
|		| beating instrument | <span class="smallcaps">`instrument`</span> |
| CUT | cutter | <span class="smallcaps">`actor`</span> |
|		| cut thing | <span class="smallcaps">`undergoer`</span> |
|		| cutting instrument | <span class="smallcaps">`instrument`</span> |
| GRIND | grinder | <span class="smallcaps">`actor`</span> |
|		| ground thing | <span class="smallcaps">`undergoer`</span> |
| COOK | cooker | <span class="smallcaps">`actor`</span> |
|		| cooked food | <span class="smallcaps">`undergoer`</span> |
| EAT | eater | <span class="smallcaps">`actor`</span> |
|		| eaten food | <span class="smallcaps">`undergoer`</span> |
| DRINK | drinking person | <span class="smallcaps">`actor`</span> |
|		| drunked thing | <span class="smallcaps">`undergoer`</span> |
| COVER | coverer | <span class="smallcaps">`actor`</span> |
|		| cover | <span class="smallcaps">`instrument`</span> |
|		| covered thing | <span class="smallcaps">`undergoer`</span> |
| FILL | filler | <span class="smallcaps">`actor`</span> |
|		| filling material | <span class="smallcaps">`instrument`</span> |
|		| filled container | <span class="smallcaps">`undergoer`</span> |
| WIPE (cos) | wiper | <span class="smallcaps">`actor`</span> |
|			| wiped surface | <span class="smallcaps">`undergoer`</span> |
| PEEL (cos) | peeler | <span class="smallcaps">`actor`</span> |
|			| peeled object | <span class="smallcaps">`undergoer`</span> |
| **Contact** | | |
| HIT | hitter | <span class="smallcaps">`actor`</span> |
|	| hittee | <span class="smallcaps">`undergoer`</span> |
|	| hitting instrument | <span class="smallcaps">`instrument`</span> |
| TOUCH | toucher | <span class="smallcaps">`actor`</span> |
|	| touchee | <span class="smallcaps">`undergoer`</span> |
|	| touching instrument | <span class="smallcaps">`instrument`</span> |
| PUSH | pusher | <span class="smallcaps">`actor`</span> |
|	| pushee | <span class="smallcaps">`undergoer`</span> |
| **Experiential** | | |
| LOOK AT | looker | <span class="smallcaps">`experiencer`</span> |
|		| looked at entity | <span class="smallcaps">`stimulus`</span> |
| SEE | seeer | <span class="smallcaps">`experiencer`</span> |
|	| seen entity | <span class="smallcaps">`stimulus`</span> |
| APPEAR | appearer | <span class="smallcaps">`stimulus`</span> |
| SMELL | smeller | <span class="smallcaps">`experiencer`</span> |
|	| smelled entity | <span class="smallcaps">`stimulus`</span> |
| HEAR | hearer | <span class="smallcaps">`experiencer`</span> |
|	| heard sound | <span class="smallcaps">`stimulus`</span> |
| FEAR | fearer | <span class="smallcaps">`experiencer`</span> |
|	| fear stimulus | <span class="smallcaps">`stimulus`</span> |
| FRIGHTEN | frightenee | <span class="smallcaps">`experiencer`</span> |
|	| frightener | <span class="smallcaps">`stimulus`</span> |
| LIKE | liker | <span class="smallcaps">`experiencer`</span> |
|	| liked entity | <span class="smallcaps">`stimulus`</span> |
| KNOW | knower | <span class="smallcaps">`experiencer`</span> |
|	| known thing/person | <span class="smallcaps">`stimulus`</span> |
| THINK | thinker | <span class="smallcaps">`experiencer`</span> |
|	| thought content | <span class="smallcaps">`stimulus`</span> |
| WANT | wanter | <span class="smallcaps">`experiencer`</span> |
|	| wanted thing | <span class="smallcaps">`stimulus`</span> |
| FEEL PAIN | pain-feeler | <span class="smallcaps">`experiencer`</span> |
|	| pain locus | <span class="smallcaps">`stimulus`</span> |
| **Partly-unrealized** | | |
| SEARCH FOR | searcher | <span class="smallcaps">`actor`</span> |
|			| searched thing | <span class="smallcaps">`undergoer`</span> |
| HUNT (FOR) | hunter | <span class="smallcaps">`actor`</span> |
|			| hunted thing | <span class="smallcaps">`undergoer`</span> |
| **Application** | | |
| PUT | putter | <span class="smallcaps">`actor`</span> |
|		| put thing | <span class="smallcaps">`theme`</span>  |
|		| putting goal | <span class="smallcaps">`goal`</span> |
| POUR | pourer | <span class="smallcaps">`actor`</span> |
|		| poured substance | <span class="smallcaps">`theme`</span>  |
|		| pouring goal | <span class="smallcaps">`goal`</span> |
| LOAD | loader | <span class="smallcaps">`actor`</span> |
|		| loaded thing | <span class="smallcaps">`theme`</span>  |
|		| loading place  | <span class="smallcaps">`goal`</span> |
| TIE | tier | <span class="smallcaps">`actor`</span> |
|		| tied thing | <span class="smallcaps">`theme`</span>  |
|		| tying goal | <span class="smallcaps">`goal`</span> |
| **Removal** | | |
| TAKE | taker | <span class="smallcaps">`actor`</span> |
|		| taken thing | <span class="smallcaps">`theme`</span>  |
|		| taking source | <span class="smallcaps">`source`</span> |
| TEAR | tearer | <span class="smallcaps">`actor`</span> |
| 		| torn thing | <span class="smallcaps">`theme`</span>  |
|		| tearing source | <span class="smallcaps">`source`</span> |
| WIPE (motion) | wiper | <span class="smallcaps">`actor`</span> |
|				| wiped material | <span class="smallcaps">`theme`</span>  |
|				| wiped surface | <span class="smallcaps">`source`</span> |
| PEEL (motion) | peeler | <span class="smallcaps">`actor`</span> |
|			| peel | <span class="smallcaps">`theme`</span>  |
|			| peeled object | <span class="smallcaps">`source`</span> |
| **Creation** | | |
| BUILD | builder | <span class="smallcaps">`actor`</span> |
|		| built thing | <span class="smallcaps">`undergoer`</span> |
|		| building material | <span class="smallcaps">`instrument`</span> |
| MAKE | maker | <span class="smallcaps">`actor`</span> |
|		| made thing | <span class="smallcaps">`undergoer`</span> |
| **Transfer**
| GIVE | giver | <span class="smallcaps">`actor`</span> |
|		| gift | <span class="smallcaps">`theme`</span>  |
|		| giving recipient | <span class="smallcaps">`recipient`</span> |
| SEND | sender | <span class="smallcaps">`actor`</span> |
|		| sent thing | <span class="smallcaps">`theme`</span>  |
|		| sending recipient | <span class="smallcaps">`recipient`</span> |
| CARRY | carrier | <span class="smallcaps">`actor`</span> |
|		| carried thing | <span class="smallcaps">`theme`</span>  |
|		| carrying goal | <span class="smallcaps">`goal`</span> |
| THROW | thrower | <span class="smallcaps">`actor`</span> |
|		| thrown thing | <span class="smallcaps">`theme`</span>  |
|		| throwing goal | <span class="smallcaps">`goal`</span> |
| BRING | bringer | <span class="smallcaps">`actor`</span> |
|		| brought thing | <span class="smallcaps">`theme`</span>  |
|		| bringing recipient | <span class="smallcaps">`recipient`</span> |
| STEAL | stealer | <span class="smallcaps">`actor`</span> |
|		| stolen thing | <span class="smallcaps">`theme`</span>  |
|		| stealing source | <span class="smallcaps">`affectee`</span> |
| GET | receiver | <span class="smallcaps">`recipient`</span> |
|		| received thing | <span class="smallcaps">`theme`</span> |
| **Communication** | | |
| TALK | talker | <span class="smallcaps">`actor`</span> |
|		| talked about content | <span class="smallcaps">`theme`</span>  |
|		| talked to person | <span class="smallcaps">`recipient`</span> |
| ASK FOR | asker | <span class="smallcaps">`actor`</span> |
|		| requested thing | <span class="smallcaps">`theme`</span>  |
|		| askee | <span class="smallcaps">`recipient`</span> |
| SHOUT AT | shouter | <span class="smallcaps">`actor`</span> |
|		   | shoutee | <span class="smallcaps">`recipient`</span> |
| TELL | teller | <span class="smallcaps">`actor`</span> |
|		| told content | <span class="smallcaps">`theme`</span>  |
|		| tellee | <span class="smallcaps">`recipient`</span> |
| SHOW | shower | <span class="smallcaps">`actor`</span> |
|		| shown thing | <span class="smallcaps">`theme`</span>  |
|		| showing addressee | <span class="smallcaps">`recipient`</span> |
| HIDE | hider | <span class="smallcaps">`actor`</span> |
|		| hidden thing | <span class="smallcaps">`theme`</span>  |
|		| hiding affectee | <span class="smallcaps">`affectee`</span> |
| SCREAM | screamer | <span class="smallcaps">`actor`</span> |
|TEACH | teacher | <span class="smallcaps">`actor`</span> |
|		| taught content | <span class="smallcaps">`theme`</span>  |
|		| teachee | <span class="smallcaps">`recipient`</span> |
| SAY | sayer | <span class="smallcaps">`actor`</span> |
|	  | said content | <span class="smallcaps">`theme`</span>  |
|     | saying addressee | <span class="smallcaps">`recipient`</span> |
| NAME | namer | <span class="smallcaps">`actor`</span> |
|	   | name | <span class="smallcaps">`theme`</span>  |
|	   | namee | <span class="smallcaps">`recipient`</span> |	

Table X: Verb meanings and non-lexicalized role annotation
</div>

[Back to Table of Contents](#toc)

  #### Part 3-2-2. Non-participant role UMR relations
  
Apart from predicate-specific and general participant roles, UMR also has a set of relations that are mainly used to mark NP-internal relations, to mark some types of modifiers of predicates, and to make the meanings of certain natural language expressions computationally tractable. Most of those relations are inherited from AMR, but for some of them, there are some changes in their use.

[Back to Table of Contents](#toc)

  ##### Part 3-2-2-1. Temporal relations

Some relations are used to describe entities in a standard, canonical form. This is the case for ```:calendar, :century, :day, :dayperiod, :decade, :era, :month, :quarter, :season, :time, :timezone, :weekday, :year,``` and ```:year2```. The use of these relations is exemplified in [\[3-2-2-1 (1)\]](#3-2-2-1 (1)).

<span id="3-2-2-1 (1)" label="3-2-2-1 (1)">\[3-2-2-1 (1)\]</span> 

<span id="3-2-2-1 (1a)" label="3-2-2-1 (1a)">\[3-2-2-1 (1a)\]</span> 
```
March 23rd, 2021
(d/ date-entity
	:year 2021
	:month 3
	:day 23)
```
<span id="3-2-2-1 (1b)" label="3-2-2-1 (1b)">\[3-2-2-1 (1b)\]</span> 
```
Friday the 13th
(d/ date-entity
	:weekday (f/ Friday)
	:day 13)
```
<span id="3-2-2-1 (1c)" label="3-2-2-1 (1c)">\[3-2-2-1 (1c)\]</span> 
```
3.30 pm Albuquerque time
(d/ date-entity
	:time 15:30
	:timezone (z/ MST))
```
[Back to Table of Contents](#toc)

  ##### Part 3-2-2-2. Modifiers

Other relations mostly function to modify object concepts - they are often expressed in languages as modifiers of some sort within an NP. Semantically, modification relations in referring expressions come in two kinds: anchoring and typifying (Croft, to appear). Anchoring modifiers "situate the intended referent of the referring expression via reference to another object", in other words, they provide referential grounding for a referent expression. Many anchoring modification relations are construed in languages as possessive relations: ownership (which situates a referent via reference to its owner), part-whole relations (which situate a referent via reference to a larger entity it is a part of), and kinship relations (which situate a referent via reference to another person that has a particular kind of relation to them). As described in [Part 3-2-1-3](#part-3-2-1-3-inverse-participant-roles), kinship relations are annotated through the `kinship-91` predicate, even when they are not predicated. For ownership and part-whole relations, UMR uses `:poss` and `:part-of` relations with the possessum or part as the parent and the possessor or whole as the daughter, as in [\[3-2-2-2 (1)\]](#3-2-2-1 (1)).

<span id="3-2-2-2 (1)" label="3-2-2-2 (1)">\[3-2-2-2 (1)\]</span> 

<span id="3-2-2-2 (1a)" label="3-2-2-2 (1a)">\[3-2-2-2 (1a)\]</span> 

```
John's car
(c/ car
	:poss (p/ person
		:name (n/ name	:op1 "John"))
	:ref-number Singular)
```
<span id="3-2-2-2 (1b)" label="3-2-2-2 (1b)">\[3-2-2-2 (1b)\]</span> 
```
Guitar strings
(s/ string
	:part-of (g/ guitar)
	:ref-number Plural)
```
Typifying modifiers, on the other hand, "enrich the referent description by subcategorizing it or selecting the quantity (cardinality, amount, proportion, piece) of the
category or type denoted by the head noun." For such modifiers, a high-level, coarse-grained relation `:mod` is available. For example, in [\[3-2-2-2 (2a)\]](#3-2-2-2 (2a)), the modifier *women* does not narrow down the reference of *magazine* to a specific identifiable instance, but rather to a subclass of magazines. It is therefore annotated with the `:mod` relation, as opposed to a phrase like *that woman's magazine*, where *woman* would be annotated with the `:poss` relation. The `:mod` relation additionally inherits some uses from UMR. It is used to annotate demonstrative determiners, and it is used to annotate property concept modifiers that do not have their own frame files. Those uses are exemplified in [\[3-2-2-2 (2b)\]](#3-2-2-2 (2b))-[\[3-2-2-2 (2c)\]](#3-2-2-2 (2c)) A number of more fine-grained subtypes of the `:mod` relation are also available - `:age`, for indicating the age of referents as in [\[3-2-2-2 (2d)\]](#3-2-2-2 (2d)); `:consist-of`, for indicating the membership of groups [\[3-2-2-2 (2e)\]](#3-2-2-2 (2e)); `:topic`, for indicating what a referent is about as in [\[3-2-2-2 (2f)\]](#3-2-2-2 (2f)), and `:medium` for indicating channels of communication, such as languages as in [\[3-2-2-2 (2g)\]](#3-2-2-2 (2g)).

<span id="3-2-2-2 (2)" label="3-2-2-2 (2)">\[3-2-2-2 (2)\]</span> 

<span id="3-2-2-2 (2a)" label="3-2-2-2 (2a)">\[3-2-2-2 (2a)\]</span> 
```
a women's magazine
(m/ magazine
	:mod (w/ woman)
	:ref-number Singular)
```
<span id="3-2-2-2 (2b)" label="3-2-2-2 (2b)">\[3-2-2-2 (2b)\]</span> 
```
These shirts of mine
(s/ shirt
	:poss (p/ person
		:ref-person 1st
		:ref-number Singular)
	:mod (t/ these)
	:ref-number Plural)
```
<span id="3-2-2-2 (2c)" label="3-2-2-2 (2c)">\[3-2-2-2 (2c)\]</span> 
```
My quirky shirts
(s/ shirt
	:poss (p/ person
		:ref-person 1st
		:ref-number Singular)
	:mod (q/ quirky)
	:ref-number Plural)
```
<span id="3-2-2-2 (2d)" label="3-2-2-2 (2d)">\[3-2-2-2 (2d)\]</span> 
```
The thirty year-old man
(m/ man
	:age (t/ temporal-quantity
		:quant 30
		:unit (y/ year))
	:ref-number Singular)
```
<span id="3-2-2-2 (2e)" label="3-2-2-2 (2e)">\[3-2-2-2 (2e)\]</span> 

```
A swarm of bees
(s/ swarm
	:consist-of (b/ bee
		:ref-number Plural))
```
<span id="3-2-2-2 (2f)" label="3-2-2-2 (2f)">\[3-2-2-2 (2f)\]</span> 

```
Information about the case
(i/ information
	:topic (c/ case))
```

<span id="3-2-2-2 (2g)" label="3-2-2-2 (2g)">\[3-2-2-2 (2g)\]</span> 
```
a French song
(t/ thing
	:ARG1-of (s/ sing-01)
	:medium (l/ language
		:wiki "French_language"
		:name (n/ name :op1 "French")))
```

[Back to Table of Contents](#toc)

##### Part 3-2-2-3. Circumstantial temporals and locatives

A number of relations serve to modify events rather than objects - they are used to annotate circumstantial locative and temporal information rather than participants. The `:direction` and `:path` relations are used to annotate cardinal directions and extended spatial paths, respectively, as in [\[3-2-2-3 (1a)\]](#3-2-2-3 (1a)) and [\[3-2-2-3 (1b)\]](#3-2-2-3 (1b)). The `:duration` and `:frequency` relations, illustrated in [\[3-2-2-3 (1c)\]](#3-2-2-3 (1c)) - [\[3-2-2-3 (1e)\]](#3-2-2-3 (1e)), are optionally used to annotate aspectual information that may be overtly present but that cannot be captured in the `:aspect` attribute - as clarified in [Part 3-3-1](#part-3-3-1-Aspect), the latter abstracts away from duration and frequency information.

<span id="3-2-2-3 (1)" label="3-2-2=3 (1)">\[3-2-2-3 (1)\]</span> 

<span id="3-2-2-3 (1a)" label="3-2-2-3 (1a)">\[3-2-2-3 (1a)\]</span> 
```
He drove west.
(d/ drive-01
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Singular)
	:direction (w/ west)
	:aspect Activity
	:modstr FullAff)
```
<span id="3-2-2-3 (1b)" label="3-2-2-3 (1b)">\[3-2-2-3 (1b)\]</span> 
```
He drove through the tunnel.
(d/ drive-01
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Singular)
	:path (t/ tunnel)
	:aspect Performance
	:modstr FullAff)
```
<span id="3-2-2-3 (1c)" label="3-2-2-3 (1c)">\[3-2-2-3 (1c)\]</span> 
```
I visited New York City for a week.
(v/ visit-01
	:ARG0 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:ARG1 (c/ city
		:name (n/ name
			:op1 "New"
			:op2 "York"
			:op3 "City")
		:wiki "New_York_City")
	:duration (t/ temporal-quantity
		:quant 1
		:unit (w/ week))
	:aspect Endeavor
	:modstr FullAff)
```
<span id="3-2-2-3 (1d)" label="3-2-2-3 (1d)">\[3-2-2-3 (1d)\]</span> 
```
I visited New York City twice.
(v/ visit-01
	:ARG0 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:ARG1 (c/ city
		:name (n / name
			:op1 "New"
			:op2 "York"
			:op3 "City")
		:wiki "New_York_City")
	:frequency 2
	:aspect Performance
	:modstr FullAff)
```
<span id="3-2-2-3 (1e)" label="3-2-2-3 (1e)">\[3-2-2-3(1e)\]</span> 
```
I visit New York City every December.
(v/ visit-01
	:ARG0 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:ARG1 (c/ city
		:name (n / name
			:op1 "New"
			:op2 "York"
			:op3 "City")
		:wiki "New_York_City")
	:frequency (r/ rate-entity-91
		:ARG4 (d/ date-entity
			:month 12))
	:aspect Habitual
	:modstr FullAff)
```

[Back to Table of Contents](#toc)

  ##### Part 3-2-2-4. Named entities

The relations `:name`, `:wiki`, and `:opX` are mostly used in the treatment of named entities. Whenever an entity is explicitly mentioned by name in the text to be annotated, it receives a `:name` relation, whose daughter is an `(n/ name)` node. This node then has as many numbered `:opX` relations as the number of words this name consists of, each of which takes one of these words as their daughter. In [\[3-2-2-3 (1e)\]](#3-2-2-3 (1e)) above, for example, the `(n/ name)` concept corresponding to *New York City* takes an `:op1`, `:op1`, and `:op3` relation, one for each orthographic word. Named entities can also take a `:wiki` relation, whose daughter is the title of the Wikipedia page corresponding to the entity in question. Numbered `:opX` relations are also used as the daughters of various abstract concepts used for expressing relations between clauses or phrases (e.g. coordination), as in [\[3-2-2-4 (1)\]](#3-2-2-4 (1)).

<span id="3-2-2-4 (1)" label="3-2-2 (5)">\[3-2-2-4 (1)\]</span> 
```
I saw a spider and a snake.
(s/ see-01
	:ARG0 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:ARG1 (a/ and
		:op1 (s2/ spider
			:ref-number Singular)
		:op2 (s3/ snake
			:ref-number Singular))
	:aspect State
	:modstr FullAff)
```

[Back to Table of Contents](#toc)

  ##### Part 3-2-2-5. Quantification

The `:ord`, `:quant`, `:range`, `:scale`, `:unit`, and `:value` relations are used to annotate semantics of quantification, as illustrated in [\[3-2-2-5 (1)\]](#3-2-2-5 (1)). The `:ord` role is used to express ordinals. It always takes an `(o/ ordinal-entity)` concept as its daughter, which in turn takes a `:value` relation to express the ordinal position, as in [\[3-2-2-5 (1a)\]](#3-2-2-5 (1a)). It may furthermore take a `:range` relation to indicate a specific time period in which the relevant ordinal position holds, as in [\[3-2-2-5 (1b)\]](#3-2-2-5 (1b)). The `:value` relation is, apart from ordinals, used for annotating percentages, phone numbers, e-mail addresses, and urls, as illustrated in [\[3-2-2-5 (1c)\]](#3-2-2-5 (1c)) and [\[3-2-2-5 (1d)\]](#3-2-2-5 (1d)). The `:quant` relation is used for annotating both exact and approximate cardinalities of sets of countable objects as in [\[3-2-2-5 (1e)\]](#3-2-2-5 (1e)) and [\[3-2-2-5 (1f)\]](#3-2-2-5 (1f)), as well as for the number of "units" of non-countable substances, as in [\[3-2-2-5 (1g)\]](#3-2-2-5 (1g)). This latter use includes temporal durations and spatial distances, as in [\[3-2-2-3 (1c)\]](#3-2-2-3 (1c)) above. The `:unit` relation is used for both standardized, well-established units such as dollars in [\[3-3-2 (1a)\]](#3-3-2 (1a)) below or weeks in [\[3-2-2-3 (1c)\]](#3-2-2-3 (1c)) above, and for ad-hoc mensural constructions, such as cups in [\[3-2-2-5 (1g)\]](#3-2-2-5 (1g)). Lastly, the `:scale` relation is used for quantities where a `:quant 0` value does not actually represent a 0-quantity, such as on the Richter or Decibel scale, as in [\[3-2-2-5 (1h)\]](#3-2-2-5 (1h))

<span id="3-2-2-5 (1)" label="3-2-2-5 (1)">\[3-2-2-5 (1)\]</span> 

<span id="3-2-2-5 (1a)" label="3-2-2-5 (1a)">\[3-2-2-5 (1a)\]</span> 
```
I visited New York for the third time.
(v/ visit-01
	:ARG0 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:ARG1 (c/ city
		:name (n/ name
			:op1 "New"
			:op2 "York")
		:wiki "New_York_City")
	:ord (o/ ordinal-entity
		:value 3)
	:aspect Performance
	:modstr FullAff)
```
<span id="3-2-2-5 (1b)" label="3-2-2-5 (1b)">\[3-2-2-5 (1b)\]</span> 
```
I visited New York for the third time in six months.
(v/ visit-01
	:ARG0 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:ARG1 (c/ city
		:name (n/ name
			:op1 "New"
			:op2 "York")
		:wiki "New_York_City")
	:ord (o/ ordinal-entity
		:value 3
		:range (t/ temporal-quantity
			:quant 6
			:unit (m/ month)))
	:aspect Performance
	:modstr FullAff)
```
<span id="3-2-2-5 (1c)" label="3-2-2 (6c)">\[3-2-2 (6c)\]</span> 
```
30 percent
(p/ percentage-entity
	:value 30)
```
<span id="3-2-2-5 (1d)" label="3-2-2-5 (1d)">\[3-2-2-5 (1d)\]</span> 
```
http://umr-tool.cs.brandeis.edu/display_post
(u/ url-entity
	:value "http://umr-tool.cs.brandeis.edu/display_post")
```
<span id="3-2-2-5 (1e)" label="3-2-2-5 (1e)">\[3-2-2-5 (1e)\]</span> 
```
Three houses
(h/ house
	:quant 3)
```
<span id="3-2-2-5 (1f)" label="3-2-2-5 (1f)">\[3-2-2-5 (1f)\]</span> 
```
More than three houses
(h/ house
	:quant (m/ more-than :op1 3))
```
<span id="3-2-2-5 (1g)" label="3-2-2-5 (1g)">\[3-2-2-5 (1g)\]</span> 
```
Three cups of milk
(m/ milk
	:quant 3
	:unit (c/ cup))
```
<span id="3-2-2-5 (1h)" label="3-2-2-5 (1h)">\[3-2-2-5 (1h)\]</span> 
```
6.5 on the Richter scale
(s/ seismic-quantity
	:quant 6.5
	:scale (r/ richter))
```

[Back to Table of Contents](#toc)

  ##### Part 3-2-2-6. Other relations

The `:example` relation, illustrated in [\[3-2-2-6 (1a)\]](#3-2-2-6 (1a)), is used to annotate illustrative examples of object categories. The `:polite` relation is used to indicate that an utterance (often a command) is marked for deference with respect to the interlocutor, as in [\[3-2-2-6 (1b)\]](#3-2-2-6 (1b)). 

<span id="3-2-2-6 (1)" label="3-2-2-6 (1)">\[3-2-2-6 (1)\]</span> 

<span id="3-2-2-6 (1a)" label="3-2-2-6 (1a)">\[3-2-2-6 (1a)\]</span> 
```
Countries like Germany and France
(c/ country
	:example (a/ and
		:op1 (c2/ country
			:name (n/ name	:op1 "Germany")
			:wiki "Germany")
		:op2 (c3/ country
			:name (n2/ name	:op1 "France")
			:wiki "France")))
```
<span id="3-2-2-6 (1b)" label="3-2-2-6 (1b)">\[3-2-2-6 (1b)\]</span> 
Could you close the window?
```
(c / close.01
	:ARG0 (p / person
		:ref-person 2nd
		:ref-number Singular)
	:ARG1 (w / window)
	:Aspect Performance
	:Mode Imperative
	:polite +)
```

The `:condition` and `:concession` relations are alternative ways of annotating the `have-condition-91` and `have-concession-91` predicates - their use is detailed in [Part 4-3](#part-4-3-modal-dependency).

Lastly, annotators have at their disposal an `:other` relation, as already mentioned in table 5 in [Part 3-2-1-1](#part-3-2-1-1-stage-0). If they encounter any concept that they believe needs to be included in the UMR annotation, but UMR does currently not have a defined procedure of annotating it, they may simply add it to the graph using this `:other` relation, linking it to the concept node that seems appropriate.

[Back to Table of Contents](#toc)

### Part 3-3. UMR attributes
  
#### Part 3-3-1. Aspect

The aspect annotation consists of a single value that is annotated for
every event identified in [Part 3-1-1](#part-3-1-1-eventive-concepts). The aspect annotation doesn’t
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

![Aspect lattice](https://github.com/umr4nlp/umr-guidelines/blob/master/Guidelines_figures/Aspect%20Lattice_2022.png)

Below are the aspect values with a brief definition.

```habitual```: occurs/occurred usually or habitually  
```imperfective```: ambiguous between state and process  
```process```: unspecified type of process  
```atelic process```: process that does not reach a result state  
```perfective```: process that comes to an end  
```state```: unspecified type of state  
```reversible state```: acquired state that is not permanent  
```irreversible state```: acquired state that is permanent  
```inherent state```: state that is not acquired and permanent  
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

[Back to Table of Contents](#toc)

##### Part 3-3-1-1. Event Nominals

The first decision concerns the morphosyntactic expression of the event. Events expressed as nominals often lack any grammatical clues as to their aspectual structure. This makes determining an aspectual
annotation value difficult. We do, however, know that these events are
processes, and not states, since nominals expressing states are not
identified as events. On the lattice,
```process``` is the aspectual value that includes all types of processes. Therefore, events expressed as event
nominals, as in [\[3-3-1-1 (1)\]](#3-3-1-1 (1)), are annotated as
```process```.


<span id="3-3-1-1 (1)" label="3-3-1-1 (1)">\[3-3-1 (1)\]</span>

<span id="3-3-1-1 (1a)" label="3-3-1-1 (1a)">\[3-3-1-1 (1a)\]</span>
```
He presented his research at **the meeting** yesterday.
(p/ present-01
	:ARG0 (p2/ person
		:ref-person 3rd
		:ref-number Singular)
	:ARG1 (t/ thing
		:ARG1-of (r/ research-01
			:ARG0 p2))
	:place (m/ meet-01
		:aspect Process)
	:temporal (y/ yesterday)
	:aspect Performance
	:modstr FullAff)
```
<span id="3-3-1-1 (1b)" label="3-3-1-1 (1b)">\[3-3-1-1 (1b)\]</span>   
```
After **the game**, she went home.
(g/ go-01
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Singular)
	:ARG4 (h/ home)
	:temporal (a/ after
		:op1 (g2/ game
			:aspect Process))
	:aspect Performance
	:modstr FullAff)
```
Any event packaged in a referring expression is considered an event
nominal and annotated with `process`. This
includes underived nominals, nominalizations, and gerunds, as in
[\[3-3-1-1 (2)\]](#3-3-1-1 (2)).

<span id="3-3-1-1 (2)" label="3-3-1-1 (2)">\[3-3-1-1 (2)\]</span>

<span id="3-3-1-1 (2a)" label="3-3-1-1 (2a)">\[3-3-1-1 (2a)\]</span>   
```
**The second training** was cancelled yesterday.
(c/ cancel-01
	:ARG1 (t/ train-01
		:ord (o/ ordinal-entity
			:value 2)
		:aspect Process)
	:temporal (y/ yesterday)
	:aspect Performance
	:modstr FullAff) 
```
<span id="3-3-1-1 (2b)" label="3-3-1-1 (2b)">\[3-3-1-1 (2b)\]</span> The dog
interrupted the meeting with **his barking**.  
```
(i/ interrupt-01
	:ARG0 (d/ dog
		:ref-number Singular)
	:ARG1 (m/ meet-01
		:aspect Process)
	:manner (b/ bark-01
		:ARG0 d
		:aspect Process)
	:aspect Performance
	:modstr FullAff) 
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

[Back to Table of Contents](#toc)

##### Part 3-3-1-2. Habitual

The next step concerns the application of the
```habitual``` aspect value. This value should
be applied to all events that are presented as occurring usually or
habitually, as in [\[3-3-1-2 (1)\]](#3-3-1-2 (1)).


<span id="3-3-1-2 (1)" label="3-3-1-2 (1)">\[3-3-1-2 (1)\]</span>

<span id="3-3-1-2 (1a)" label="3-3-1-2 (1a)">\[3-3-1-2 (1a)\]</span> 
```
He **bakes** pies.
(b/ bake-01
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Singular)
	:ARG1 (p2/ pie
		:ref-number Plural)
	:aspect Habitual
	:modstr FullAff) 
```
<span id="3-3-1-2 (1b)" label="3-3-1-2 (1b)">\[3-3-1-2 (1b)\]</span>  
```
She **rides** her bike to work.
(r/ ride-01
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Singular)
	:ARG1 (b/ bike
		:poss p)
	:goal (w/ work-01
		:ARG0 p
		:aspect Process)
	:aspect Habitual
	:modstr FullAff)
```
<span id="3-3-1-2 (1c)" label="3-3-1-2 (1c)">\[3-3-1-2 (1c)\]</span>   
```
They **vacation** in Taos every winter.
(v/ vacation-01
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Plural)
	:ARG (c/ city
		:name (n/ name :op1 "Taos")
		:wiki "Taos_New_Mexico")
	:frequency (r/ rate-entity-91
		:ARG3 (t/ temporal-quantity
			:quant 1
			:unit (y/ year))
		:ARG4 (w/ winter))
	:aspect Habitual
	:modstr FullAff)  
```
<span id="3-3-1-2 (1d)" label="3-3-1-2 (1d)">\[3-3-1-2 (1d)\]</span>
```
They **used to vacation** in Taos every winter.
(v/ vacation-01
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Plural)
	:ARG (c/ city
		:name (n/ name :op1 "Taos")
		:wiki "Taos_New_Mexico")
	:frequency (r/ rate-entity-91
		:ARG3 (t/ temporal-quantity
			:quant 1
			:unit (y/ year))
		:ARG4 (w/ winter))
	:aspect Habitual
	:modstr FullAff)   
```

In English, present habitual events are signalled by the Simple Present
construction; past tense habitual events are expressed with the *used
to* construction. Note that the ```habitual```
annotation is not used for ability modals (e.g., *he can bake apple
pie*); these events should continue on to the next step.

[Back to Table of Contents](#toc)
##### Part 3-3-1-3. State

The next step assesses whether the event is a
```state```. The distinction between states and
processes is necessary for event identification (as states are only
identified as events when predicated, see [Part 3-1-1](#part-3-1-1-eventive-concepts)). According to Vendler (1967), states are those events which are stative—that is, no change takes place over the course of the event. There are various ways to express states in predication, shown in [\[3-3-1-3 (1)\]](#3-3-1-3 (1)); note that all of the nonverbal clause types identified in [Part 3-1-1-3](#part-3-1-1-3-states-and-entities) and annotated with UMR predicates are annotated as ```state```.


<span id="3-3-1-3 (1)" label="3-3-1-3 (1)">\[3-3-1-3 (1)\]</span>

<span id="3-3-1-3 (1a)" label="3-3-1-3 (1a)">\[3-3-1-3 (1a)\]</span>  
```
My cat **loves** tuna.
(l/ love-01
	:ARG0 (c/ cat
		:poss (p/ person
			:ref-person 1st
			:ref-number Singular)
		:ref-number Singular)
	:ARG1 (t/ tuna)
	:aspect State
	:modstr FullAff)  
```
<span id="3-3-1-3 (1b)" label="3-3-1-3 (1b)">\[3-3-1-3 (1b)\]</span>  
```
The doctor **is tall**.
(h/ have-mod-91
	:ARG1 (d/ doctor
		:ref-number Singular)
	:ARG2 (t/ tall)
	:aspect State
	:modstr FullAff)
```
<span id="3-3-1-3 (1c)" label="3-3-1-3 (1c)">\[3-3-1-3 (1c)\]</span>   
```
The book **is on the table**.
(h/ have-location-91
	:ARG0 (b/ book
		:ref-number Singular)
	:ARG1 (t/ table)
	:aspect State
	:modstr FullAff)  
```
<span id="3-3-1-3 (1d)" label="3-3-1-3 (1d)">\[3-3-1-3 (1d)\]</span>   
```
She **is an architect**.
(h/ have-role-91
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Singular)
	:ARG2 (a/ architect)
	:aspect State
	:modstr FullAff) 
```
<span id="3-3-1-3 (1e)" label="3-3-1-3 (1e)">\[3-3-1-3 (1e)\]</span>   
```
Your glass **is in the kitchen**.
(h/ have-location-91 
	:ARG0 (g/ glass
		:poss (p/ person
			:ref-person 2nd
			:ref-number Singular))
	:ARG1 (k/ kitchen)
	:aspect State
	:modstr FullAff)
```

Modal verbs, as in [\[3-3-1-3 (2)\]](#3-3-1-3 (2)), and events under the scope of
ability modals, as in [\[3-3-1-3 (3)\]](#3-3-1-3 (3)), are also annotated as
```state```.

<span id="3-3-1-3 (2)" label="3-3-1-3 (2)">\[3-3-1-3 (2)\]</span>

<span id="3-3-1-3 (2a)" label="3-3-1-3 (2a)">\[3-3-1-3 (2a)\]</span>  
```
He **wants** to travel to Albuquerque. 
(w/ want-01
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Singular)
	:ARG1 (t/ travel-01
		:ARG0 p
		:ARG4 (c/ city
			:name (n/ name :op1 "Albuquerque")
			:wiki "Albuquerque")
		:aspect Performance
		:modpred w)
	:aspect State
	:modstr FullAff)
```
<span id="3-3-1-3 (2b)" label="3-3-1-3 (2b)">\[3-3-1-3 (2b)\]</span> 
```
The cat **needs** to be fed.
(n/ need-01
	:ARG0 (c/ cat)
	:ARG1 (f/ feed-01
		:ARG c
		:aspect Performance
		:modpred n)
	:aspect State
	:modstr FullAff)
```
<span id="3-3-1-3 (2c)" label="3-3-1-3 (2c)">\[3-3-1-3 (2c)\]</span>   
```
He’s **dreading** their decision.
(d/ dread  
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Singular)
	:ARG1 (d2/ decide-01
		:ARG0 (p2/ person
			:ref-person 3rd
			:ref-person Plural)
		:aspect Process
		:modpred d)
	:aspect State
	:modstr FullAff)
```
<span id="3-3-1-3 (3)" label="3-3-1-3 (3)">\[3-3-1-3 (3)\]</span>

<span id="3-3-1-3 (3a)" label="3-3-1-3 (3a)">\[3-3-1-3 (3a)\]</span>   
```
She <u>is able to</u> **sing** that aria.
(s/ sing-01
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Singular)
	:ARG1 (a/ aria
		:mod (t/ that)
		:ref-number Singular)
	:aspect State
	:modstr NeutAff)
```
<span id="3-3-1-3 (3b)" label="3-3-1-3 (3b)">\[3-3-1-3 (3b)\]</span>   
```
This car <u>can</u> **go** up to 150 mph.
(g/ go-01
	:ARG0 (c/ car
		:mod (t/ this)
		:ref-number Singular)
	:manner (s/ speed-quantity
		:quant 150
		:unit (m/ miles-per-hour))
	:aspect State
	:modstr NeutAff)
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

<span id="3-3-1-3 (4a)" label="3-3-1-3 (4a)">\[3-3-1-3 (4a)\]</span> 
```
My cat **is black and white**.
(h/ have-mod-91
	:ARG1 (c/ cat
		:poss (p/ person
			:ref-person 1st
			:ref-number Singular)
		:ref-number Singular)
	:ARG2 (a/ and
		:op1 (b/ black)
		:op2 (w/ white)
	:aspect Inherent State
	:modstr FullAff)
```
<span id="3-3-1-3 (4b)" label="3-3-1-3 (4b)">\[3-3-1-3 (4b)\]</span>   
```
My cat **is hungry**.
(h / hunger-01
	:ARG0 (c/ cat
		:poss (p/ person
			:ref-person 1st
			:ref-number Singular))
		:ref-number Singular)
	:aspect Reversible State
	:modstr FullAff)
```
<span id="3-3-1-3 (4c)" label="3-3-1-3 (4c)">\[3-3-1-3 (4c)\]</span>   
```
The wine glass **is shattered**.
(s/ shatter-01
	:ARG1 (g/ glass
		:purpose (w/ wine)
		:ref-number Singular)
	:aspect Irreversible State
	:modstr FullAff)
```
<span id="3-3-1-3 (4d)" label="3-3-1-3 (4d)">\[3-3-1-3 (4d)\]</span>  
```
It **is 2:30pm**.
(b/ be-temporally-at-91
	:ARG1 (n/ now)
	:ARG2 (d/ date-entity
		:time 14:30)
	:aspect Point State
	:modstr FullAff)
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

[Back to Table of Contents](#toc)

##### Part 3-3-1-4. Activity

The ```activity``` label applies to processes
when there is no evidence that the event has come to an end, as in
[\[3-3-1-4 (1)\]](#3-3-1-4 (1)).

<span id="3-3-1-4 (1)" label="3-3-1-4(1)">\[3-3-1-4 (1)\]</span>

<span id="3-3-1-4 (1a)" label="3-3-1-4 (1a)">\[3-3-1-4 (1a)\]</span>   
```
He is still **writing** his paper.
(w/ write-01
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Singular)
	:ARG1 (p2/ paper
		:poss p
		:ref-number Singular)
	:mod (s/ still)
	:aspect Activity
	:modstr FullAff)
```
<span id="3-3-1-4 (1b)" label="3-3-1-4 (1b)">\[3-3-1-4 (1b)\]</span>   
```
He was **writing** his paper yesterday.
(w/ write-01
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Singular)
	:ARG1 (p2/ paper
		:poss p
		:ref-number Singular)
	:temporal (y/ yesterday)
	:aspect Activity
	:modstr FullAff)
```

This covers cases where it is clear that the process is still ongoing at
document creation time, as in [\[3-3-1-4 (1a)\]](#3-3-1-4 (1a)), but also cases
where it is ambiguous whether or not the process continues, as in
[\[3-3-1-4 (1b)\]](#3-3-1-4 (1b)).

This step is largely dependent on context and real world knowledge,
however there are some grammatical cues that can help. Events in the
present tense, as in [\[3-3-1-4 (2)\]](#3-3-1-4 (2)), are annotated as
```activity```.

<span id="3-3-1-4 (2)" label="3-3-1-4 (2)">\[3-3-1-4 (2)\]</span>   
```
He **is playing** the violin.
(p/ play-01
	:ARG0 (p2/ person
		:ref-person 3rd
		:ref-number Singular)
	:ARG2 (v/ violin)
	:aspect Activity
	:modstr FullAff)
```

Inceptive and continuative aspectual marking, as in [\[3-3-1-4 (3)\]](#3-3-1-4 (3)),
also do not imply that an event has (necessarily) ended.

<span id="3-3-1-4 (3)" label="3-3-1-4 (3)">\[3-3-1-4 (3)\]</span>

<span id="3-3-1-4 (3a)" label="3-3-1-4 (3a)">\[3-3-1-4 (3a)\]</span>
```
He <u>started</u> **playing** the violin.
(p/ play-01
	:ARG0 (p2/ person
		:ref-person 3rd
		:ref-number Singular)
	:ARG2 (v/ violin)
	:aspect Activity
	:modstr FullAff)
```
<span id="3-3-1-4 (3b)" label="3-3-1-4 (3b)">\[3-3-1-4 (3b)\]</span>   
```
He <u>kept on</u> **playing** the violin.
(p/ play-01
	:ARG0 (p2/ person
		:ref-person 3rd
		:ref-number Singular)
	:ARG2 (v/ violin)
	:aspect Activity
	:modstr FullAff)
```
If an annotator is unsure about whether the text indicates that an event has ended or not, the ```atelic process```
label can be used.

There are two finer-grained ```activity```
categories which can optionally be distinguished. Certain types of
activities describe directed change, as in
[\[3-3-1-4 (4)\]](#3-3-1-4 (4)), whereas other activities describe
undirected change, as in [\[3-3-1-4 (5)\]](#3-3-1-4 (5));
these are annotated as ```directed activity```
and ```undirected activity``` respectively.


<span id="3-3-1-4 (4)" label="3-3-1-4 (4)">\[3-3-1-4 (4)\]</span>
```
The soup was **cooling** on the counter.
(c/ cool
	:ARG1 (s/ soup)
	:place (c2/ counter)
	:aspect Directed Activity
	:modstr FullAff)
```

<span id="3-3-1-4 (5)" label="3-3-1-4 (5)">\[3-3-1-4 (5)\]</span>
```
The cat was **meowing** outside the door.
(m/ meow-01
	:ARG0 (c/ cat
		:ref-number Singular)
	:place (o/ outside
		:op1 (d/ door))
	:aspect Undirected Activity
	:modstr FullAff)
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

[Back to Table of Contents](#toc)

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

<span id="3-3-1-5 (1a)" label="3-3-1-5 (1a)">\[3-3-1-5 (1a)\]</span>   
```
Mary <u>stopped</u> **mowing** the lawn.
(m/ mow-01
	:ARG0 (p/ person
		:name (n/ name :op1 "Mary"))
	:ARG1 (l/ lawn)
	:aspect Endeavor
	:modstr FullAff)
```
<span id="3-3-1-5 (1b)" label="3-3-1-5 (1b)">\[3-3-1-5 (1b)\]</span>   
```
Mary **mowed** the lawn <u>for thirty minutes</u>.
(m/ mow-01
	:ARG0 (p/ person
		:name (n/ name :op1 "Mary"))
	:ARG1 (l/ lawn)
	:duration (t/ temporal-quantity
		:unit (m2/ minute)
		:quant 30)
	:aspect Endeavor
	:modstr FullAff)
```
<span id="3-3-1-5 (1c)" label="3-3-1-5 (1c)">\[3-3-1-5 (1c)\]</span> \*Mary
<u>finished</u> **mowing** the lawn <u>for thirty minutes</u>.  

<span id="3-3-1-5 (1d)" label="3-3-1-5 (1d)">\[3-3-1-5 (1d)\]</span>  
```
They **walked** <u>along the river</u>. 
(w/ walk-01
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Plural)
	:ARG2 (a/ along
		:op1 (r/ river))
	:aspect Endeavor
	:modstr FullAff)
```
<span id="3-3-1-5 (1e)" label="3-3-1-5 (1e)">\[3-3-1-5 (1e)\]</span>  
```
They <u>finished</u> **walking** <u>along the river</u>.
(w/ walk-01
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Plural)
	:ARG2 (a/ along
		:op1 (r/ river))
	:aspect Performance
	:modstr FullAff) 
```
<span id="3-3-1-5 (1f)" label="3-3-1-5 (1f)">\[3-3-1-5 (1f)\]</span>   
```
They **walked** <u>along the river</u> <u>in 3 hours</u>.
(w/ walk-01
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Plural)
	:ARG2 (a/ along
		:op1 (r/ river))
	:duration (t/ temporal-quantity
		:unit (h/ hour)
		:quant 3)
	:aspect Performance
	:modstr FullAff) 
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

<span id="3-3-1-5 (2a)" label="3-3-1-5 (2a)">\[3-3-1-5 (2a)\]</span> 
```
The cat **meowed** for two hours until I woke up.
(m/ meow-01
	:ARG0 (c/ cat)
	:duration (t/ temporal-quantity
		:unit (h/ hour)
		:quant 2)
	:temporal (u/ until
		:op1 (w/ wake-01
			:ARG1 (p/ person
				:ref-person 1st
				:ref-number Singular)
			:aspect Performance
			:modstr FullAff))
	:aspect Undirected Endeavor
	:modstr FullAff)
```
<span id="3-3-1-5 (2b)" label="3-3-1-5 (2b)">\[3-3-1-5 (2b)\]</span> 
```
The soup **cooled**for an hour before we ate it.
(c/ cool-01
	:ARG1 (s/ soup)
	:duration (t/ temporal-quantity
		:unit (h/ hour)
		:quant 1)
	:temporal (b/ before
		:op1 (e/ eat-01
			:ARG0 (p/ person
				:ref-person 1st
				:ref-number Plural)
			:ARG1 s
			:aspect Performance
			:modstr FullAff))
	:aspect Directed Endeavor
	:modstr FullAff)
```

<span id="3-3-1-5 (2c)" label="3-3-1-5 (2c)">\[3-3-1-5 (2c)\]</span> 
```
The cat **meowed** (once).
(m/ meow-01
	:ARG0 (c/ cat
		:ref-number Singular)
	:aspect Semelfactive
	:modstr FullAff)
```

The finer-grained annotations for
```performance``` distinguish between punctual
events (```directed achievement```) and durative
events (```incremental accomplishment```,
```nonincremental accomplishment```), with even
finer-grained categories based on the type of change.

Achievements are punctual events, meaning that they are conceptualized as
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

<span id="3-3-1-5 (3)" label="3-3-1-5 (3)">\[3-3-1-5 (3)\]</span>

<span id="3-3-1-5 (3a)" label="3-3-1-5 (3a)">\[3-3-1-5 (3a)\]</span> 
```
The door **opened**.
(o/ open-01
	:ARG1 (d/ door
		:ref-number Singular)
	:aspect Reversible Directed Achievement
	:modstr FullAff)
```
<span id="3-3-1-5 (3b)" label="3-3-1-5 (3b)">\[3-3-1-5 (3b)\]</span> 
```
The window **shattered**.
(s/ shatter-01
	:ARG1 (w/ window
		:ref-number Singular)
	:aspect Irreversible Directed Achievement
	:modstr FullAff)
```
<span id="3-3-1-5 (3c)" label="3-3-1-5 (3c)">\[3-3-1-5 (3c)\]</span> 
```
I **ate** an apple pancake.
(e/ eat-01
	:ARG0 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:ARG1 (p2/ pancake
		:mod (a/ apple)
		:ref-number Singular)
	:aspect Incremental Accomplishment
	:modstr FullAff)
```
<span id="3-3-1-5 (3d)" label="3-3-1-5 (3d)">\[3-3-1-5 (3d)\]</span>
```
Harry **repaired** the computer.
(r/ repair-01
	:ARG0 (p/ person
		:name (n/ name :op1 "Harry"))
	:ARG1 (c/ computer
		:ref-number Singular)
	:aspect Nonincremental Accomplishment
	:modstr FullAff)
```
[Back to Table of Contents](#toc)

#### Part 3-3-2. Mode

UMR adopts the `:mode` attribute from AMR. The values for the `:mode` attribute include:

```expressive```: used for exclamational words such as _hmm_, _wow_, _yup_ etc., which express emotion but don't clearly refer to events, objects or properties, as in [\[3-3-2 (1a)\]](#3-3-2 (1a)). This value is not used for mere emphasis, or for exclamation marks.

```imperative```: used for commands, as in [\[3-3-2 (1b)\]](#3-3-2 (1b)).

```interrogative```: used for both polar questions and content questions, as in [\[3-3-2 (1c)\]](#3-3-2 (1c)).

<span id="3-3-2 (1)" label="3-3-2 (1)">3-3-2 (1)</span>

<span id="3-3-2 (1a)" label="3-3-2 (1a)">3-3-2 (1a)</span>
```
Yup , a couple of hundred dollars is going to save the day !
(s/ save-02 
      :ARG0 (c/ couple
            :op1 (m/ monetary-quantity
	    	:quant 100
                :unit (d/ dollar)))
      :ARG1 (d/ day
      	    :ref-number Singular)
      :aspect Performance
      :modstr FullAff
      :mode expressive)
```
<span id="3-3-2 (1b)" label="3-3-2 (1b)">3-3-2 (1b)</span>
```
Chalk another good one up to the wife .
(c/ chalk-up-02
      :ARG0 (p/ person
      	    :ref-person 2nd
	    :ref-number Singular)
      :ARG1 (a/ another
            :ARG1-of (g/ good-02)
	    :quant 1)
      :ARG2 (w/ wife)
      :aspect Performance
      :modstr PrtAff
      :mode imperative)
```

<span id="3-3-2 (1c)" label="3-3-2 (1c)">3-3-2 (1c)</span>
```
Did you see that?
(s/ see-01
      :ARG0 (p/ person
      	:ref-person 2nd
	:ref-number Singular)
      :ARG1 (t/ that)
      :aspect State
      :modstr NeutAff
      :mode interrogative
      :polarity amr-unknown)
```

[Back to Table of Contents](#toc)

#### Part 3-3-3. Polarity
UMR mainly treats propositional negation at the document-level in the modal dependency annotation. However, the AMR attribute `:polarity` is also maintained in the UMR sentence-level annotation. It is used to flag any morphosyntactic indicators of negation that are present in the clause, as in [\[3-3-3 (1)\]](#3-3-3 (1)). These do not necessarily signal semantic negation. This is the case, for example, for some instances of derivational negation of adjectives in English. 

<span id="3-3-3 (1)" label="3-3-3 (1)">3-3-3 (1)</span>

<span id="3-3-3 (1a)" label="3-3-3 (1a)">3-3-3 (1a)</span>
```
Unhealthy food.

(t/ thing
	:ARG1-of (e/ eat-01)
	:mod (h/ healthy
		:polarity -))
```

[Back to Table of Contents](#toc)

#### Part 3-3-4. Quant

<span id="3-3-4 (1)" label="3-3-4 (1)">3-3-4 (1)</span>

```
As of now , five million tickets have been sold on the StubHub website .
(s/ sell-01
      :ARG1 (t/ ticket
      	:quant 5000000)
      :location (w/ website
            :mod (c/ company
	    	:wiki "StubHub"
		:name (n/ name :op1 "StubHub")))
      :temporal (a/ as-of
            :op1 (n2/ now))
      :Aspect Performance)
```

[Back to Table of Contents](#toc)

#### Part 3-3-5. Ref
As opposed to AMR, which uses an English-based lexical treatment of pronominal reference, UMR approaches pronominal reference and person/number marking in a cross-linguistically motivated way. It annotates person and number through two attributes - `:ref-person` for grammatical person information, and `:ref-number` for grammatical number marking. These attributes can apply to any entity concept. If an explicit nominal is marked for plural or dual number, for instance, the node for this entity concept can take the relevant attribute value label, as in [\[3-3-5 (1)\]](#3-3-5 (1)).

<span id="3-3-5 (1)" label="3-3-5 (1)">3-3-5 (1)</span>

<span id="3-3-5 (1a)" label="3-3-5 (1a)">3-3-5 (1a)</span>
```
Bill saw rare birds today.
(s/ see-01
	:ARG0 (p/ person
		:name (n/ name	:op1 "Bill"))
	:ARG1 (b/ bird
		:mod (r/ rare)
		:ref-number Plural)
	:aspect State
	:modstr FullAff)
```

<span id="3-3-5 (1b)" label="3-3-5 (1b)">3-3-5 (1b)</span>
```
áine	ŋara-di-a-ru.
woman	that-3PL-EP-DU
'Those two women'

(a/ áine 'woman'
	:mod (ŋ/ ŋara 'that')
	:ref-number Dual)
```

For arguments expressed only through verbal cross-referencing, or arguments that are implicit, both `:ref-person` and `:ref-number` can be used to represent their pronominal features. In such cases where there is no overt nominal expression to attach those values to, UMR "hallucinates" a concept (typically a named-entity category, e.g. `person`, `thing`) to attach the attribute labels to in order to facilitate cross-lingual compatibility, as in [\[3-3-5 (2)\]](#3-3-5 (2)). In the context preceding this one-word sentence, the speaker talks about how upon first contact between the Sanapaná and Latinoparaguayans, the Paraguayans gifted the Sanapaná food and clothes. Here, the Sanapaná speaker describes the reaction of his ancestors to these gifts. From the prefixal indexation on the verb (2nd/3rd person masculine + distributive) and the preceding context (talking about the Sanapaná ancestors), we know that the `:actor` argument of the *eat*-verb is third person plural. Therefore, we annotate this argument with a `(p/ person)` concept, which in turn takes `:ref-person` and `:ref-number` attributes with the values `3rd` and `Plural`. The `:undergoer` of this predicate is not explicitly expressed at all, but from previous context we know it is the food that they were offered by the Paraguayans. We therefore annotate it with a `(t/ thing)` concept that will later in the document-level annotation be marked as coreferential with a mention of 'food' in the previous context.

<span id="3-3-5 (2)" label="3-3-5 (2)">3-3-5 (2)</span>
```
m-e-hl-t-om-o=hlta
NEG-2/3M.IRR-DSTR-eat-TI-IPFV=PHOD
'They did not eat it.'

(e/ entoma-00 'eat'
	:actor (p/ person
		:ref-person 3rd
		:ref-number Plural)
	:undergoer (t/ thing)
	:aspect Performance
	:modstr FullNeg)
```

The possible values for the `:refer-person` attribute are based on Cysouw's (2003) cross-linguistic study of person-marking systems in the languages of the world. They are organized in a lattice as seen below. The default level of categories contains the well-known and familiar `1st`, `2nd`, and `3rd` person values. Some languages have more fine-grained person systems, distinguishing a first person `exclusive` from a first person `inclusive` value in non-singular numbers (depending on whether the interlocutor is included in the group that is being referred to). Other languages have more coarse-grained systems, making no distinction between first and second person, or between second and third person (like Sanapaná above).

![Person lattice](https://github.com/umr4nlp/umr-guidelines/blob/master/Guidelines_figures/Person%20Lattice_2022.png)

The possible number values for the `:refer-number` attribute are based on Corbett (2000). The default level here consists simply of `singular` vs. `non-singular`. Languages with more fine-grained categories in their system may have more fine-grained `dual`, `trial`, `paucal`, and `greater plural` categories, which fit together as shown in the figure below.

![Number lattice](https://github.com/umr4nlp/umr-guidelines/blob/master/Guidelines_figures/Number%20Lattice.jpg)

[Back to Table of Contents](#toc)

#### Part 3-3-6. Degree
In AMR, markers of degree such as English _very_ (high degree of a scalar quality, as in _very cold_) and _somewhat_ (low degree of a scalar quality, as in _somewhat dirty_) are treated lexically - a `:degree` relation is added to the property concept that is admodified. However, in many languages, such degree expressions are morphological rather than periphrastic - they form a single word with the property concept word. Such a lexical treatment is hard for these languages. UMR therefore allows annotators to treat `:degree` as an attribute, with three possible values: `intensifier`, `downtoner`, and `equal`. These values can in this way be attached directly to the whole property concept word without the need for morphological decomposition, as shown in [\[3-3-6 (1)\]](#3-3-6 (1)). For languages with periphrastic degree expressions like English, the lexical entry for words such as _very_ and _somewhat_ can be constructed to include reference to which of the three degree values listed above it expresses. In that way, English annotations would be comparable to annotations in a language like Sanapaná.

<span id="3-3-6 (1)" label="3-3-6 (1)">3-3-6 (1)</span>
```
ak-yav-ay'-a=ngkoye		yamet
2/3F-be.large-TI-PFV.NMLZ=INTNS	tree
'The tree is very large.'
(h/ have-mod-91
	:ARG1 (y/ yamet 'tree')
	:ARG2 (e/ enyavay'a-00 'large'
		:degree Intensifier)
	:aspect State
	:modstr FullAff)
	
(h/ have-mod-91
	:ARG1 (t/ tree)
	:ARG2 (l/ large
		:degree (v/ very))
	:aspect State
	:modstr FullAff)
Lexicon: Very - Intensifier
```

[Back to Table of Contents](#toc)

## Part 4. Document-Level Representation
### Part 4-1. Coreference


Anaphoric expressions such as pronouns cannot be properly interpreted without identifying their referents. This is generally done by linking an anaphoric expression to a named entity, a process generally known as *coreference* in the field of NLP. Coreference is an established NLP task, and the goal here is to identify the most relevant types of coreference in the UMR framework.  

[Back to Table of Contents](#toc)

#### Part 4-1-1. Entity coreference

For the UMR corereference annotation, we first need to answer two questions. The first is what counts as an anaphorical expression. For UMR annotation, we focus on pronouns. The second question is what types of coreference relations we are considering. The most common type of coreference relations are *identity* relations, and we label such relations as *same*. Identity relations means two expressions have the same referent. In [\[4-1-1 (1)\]](#4-1-1 (1)), *he* refers to the same person as the person whose name is "Edmond Pope", and it is therefore annotated in the document-level representation with a `:same-entity` relation to the `s2p` node.

<span id="4-1-1 (1)" label="4-1-1 (1)">4-1 (1)</span>

```
Snt2: Pope is the American businessman who was convicted last week on spying charges and sentenced to 20 years in a Russian prison.
(i/ identity-91
     :ARG0 (p/ person :wiki "Edmond_Pope"
     	:name (n/ name "op1 "Pope))
     :ARG1 (b/ businessman
	:mod (n2/ nationality :wiki "United_States"
	   :name (n3/ name :op1 "America")))
	:ARG1-of (c/ convict-01
	   :ARG2 (c2/ charge-05
	      :ARG1 b
	      :ARG2 (s/ spy-02
	         :ARG0 b
		 :modpred c2))
	   :temporal (w/ week
	      :mod (l/ last))
	   :aspect Performance
	   :modstr FullAff)
	:ARG1-of (s2/ sentence-01
	   :ARG2 (p2/ prison
	      :mod (c3/ country :wiki "Russia"
	         :name (n4/ name :op1 "Russia))
	      :duration (t/ temporal-quantity
	         :quant 20
		 :unit (y/ year)))
	   :ARG3 s
	   :aspect Performance
	   :modstr FullAff)
     :aspect State
     :modstr FullAff)

Snt3: He denied any wrongdoing.
(d/ deny-01 
      :ARG0 (p/person
         :ref-person 3rd
	 :ref-number Singular)
      :ARG1 (t/ thing
            :ARG1-of (d2/ do-02
                  :ARG0 p
                  :ARG1-of (w/ wrong-02)
		  :modpred d))
      :aspect Performance
      :modstr FullAff)
  
(s3/ sentence
    :temporal((DCT :before s3d)
              (s3d :before s3d2))
    :modal((AUTH :FullAff s3p))
	   (s3p :FullAff s3d)
	   (s3d :Unsp s3d2))
  :coref(s2p :same-entity s3p))
```

The example in [\[4-1-1 (2)\]](#4-1-1 (2)) shows how the `:subset-of` relation is used to relate mentions of sets of entities to mentions of entities belonging to such a set. For example, _we_ (`p3`) includes reference to two entities - the author/speaker of the sentence, and the person who is described as *possessive and controlling*. The pronoun _he_, given the constant `p2`, refers to one of these two entities. Therefore, in the document-level annotation, `p2` is annotated with a `:subset-of` relation to the `p3` node.

<span id="4-1-1 (2)" label="4-1-1 (2)">4-1-1 (2)</span>
```
He is very possessive and controlling but he has no right to be as we are not together.
(c/ contrast-01
      :ARG1 (a/ and
            :op1 (p/ possessive-03
                  :ARG0 (p/ person
		  	:ref-person 3rd
			:ref-number Singular)
                  :degree (v/ very)
		  :aspect State
		  :modstr FullAff)
            :op2 (h/ have-mod-91
                  :ARG1 p
		  :ARG2 (c2/ controlling)
                  :degree (v / very)
		  :aspect State
		  :modstr FullAff))
      :ARG2 (r/ right-05
            :ARG1 p
            :ARG2 a
            :ARG1-of (c3/ cause-01
                  :ARG0 (h2/ have-mod-91
		  	:ARG1 (p2/ person
				:ref-person 1st
				:ref-number Plural)
			:ARG2 (t/ together)
			:aspect State
			:modstr FullNeg))
            :aspect State
	    :modstr FullNeg))
(s/ sentence
  :temporal ((DCT :overlap s1p)
  	     (s1p :overlap s1h)
	     (s1h :overlap s1r)
	     (s1r :overlap s1h2))
  :modal ((AUTH :FullAff s1p)
  	  (AUTH :FullAff s1h)
	  (AUTH :FullNeg s1r)
	  (AUTH :FullNeg s1h2))
  :coref (p :subset-of p2))
```

[Back to Table of Contents](#toc)

#### Part 4-1-2. Event coreference
 
UMR uses the `:same-event` relation to represent cases where two event mentions refer to  the same event, as in [\[4-1-1 (1)\]](#4-1-1 (1)).
 
 <span id="4-1-2 (1)" label="4-1-2 (1)">4-1-2 (1)</span>
 
 <span id="4-1-2 (1a)" label="4-1-2 (1a)">4-1-2 (1a)</span>
```
El-Shater and Malek's property was confiscated and is believed to be worth millions of dollars.
(a/ and
      :op1 (c/ confiscate-01
            :ARG1 (a2/ and
                  :op1 (p/ property
                        :poss (p2/ person 
				:wiki "Khairat_el-Shater"
				:name (n/ name :op1 "El-Shater")))
                  :op2 (p3/ property
                        :poss (p4/ person
				:wiki -
				:name (n2/ name :op1 "Malek"))))
	    :aspect Performance
	    :modstr FullAff)
      :op2 (b/ believe-01
            :ARG1 (w/ worth-01
                  :ARG1 a2
                  :ARG2 (m/ multiple
                        :op1 (m2/ monetary-quantity 
			      :quant 1000000
                              :unit (d / dollar)))
	          :aspect State
		  :modpred b)
	    :aspect State
	    :modstr FullAff))
	    
(s1/ sentence
  :temporal ((PAST_REF :includes s1c)
  	     (DCT :overlap s1b)
	     (s1b :overlap s1w))
  :modal ((AUTH :FullAff s1c)
  	  (AUTH :FullAff NULL_BELIEVER)
	  (NULL_BELIEVER :FullAff s1b)
	  (s1b :Unsp s1w)))
```
 <span id="4-1-2 (1b)" label="4-1-2 (1b)">4-1-2 (1b)</span>
```
Abdel-Maksoud stated the confiscation will affect the Brotherhood's financial bases.
(s/ state-01
      :ARG0 (p/ person
           :wiki "Hamdeen_Sabahi"
	   :name (n/ name :op1 "Abdel-Maksoud"))
      :ARG1 (a/ affect-01
            :ARG0 (c/ confiscate-01)
            :ARG1 (b/ base
                  :poss (o/ organization
		  	:wiki "Muslim_Brotherhood"
			:name (n2/ name :op1 "Brotherhood"))
                  :mod (f/ finance))
	    :aspect Performance
	    :quot s
	    :modstr FullAff)
      :aspect Performance
      :modstr FullAff)

(s2/ sentence
  :temporal ((s1c :after s2s)
  	     (s2s :after s2a))
  :modal ((AUTH :FullAff s2s)
  	  (AUTH :FullAff s2p)
	  (s2p :FullAff s2c)
	  (s2p :FullAff s2a))
  :coref (s1c :same-event s2c))
```
Event identity also includes cases where the same underlying event is referred to with two very different linguistic expressions. This is the case for *introduced* and *provide* in [\[4-1-2 (2)\]](#4-1-2 (2)).

<span id="4-1-2 (2)" label="4-1-2 (2)">4-1-2 (2)</span>

<span id="4-1-2 (2a)" label="4-1-2 (2a)">4-1-2 (2a)</span>
```
The Three Gorges project on the Yangtze River has recently **introduced*** the first foreign capital.
(i/ introduce-01
      :ARG0 (p/ project
      	    :wiki "Three_Gorges_Dam"
	    :name (n/ name 
	    	:op1 "The"
		:op2 "Three"
		:op3 "Gorges")
            :place (r/ river
	    	:wiki "Yangtze"
		:name (n2/ name
			:op1 "Yangtze"
			:op2 "River")))
      :ARG1 (c/ capital
            :mod (f/ foreign)
            :ord (o/ ordinal-entity
	    	:value 1))
      :temporal (r2/ recent)
      :aspect Performance
      :modstr FullAff)
      
(s1/ sentence
	:temporal ((PAST_REF :includes s1r2)
		   (s1r2 :includes s1i))
	:modal (AUTH :FullAff s1i))
```
<span id="4-1-2 (2b)" label="4-1-2 (2b)">4-1-2 (2b)</span>
```
The loan, a sum of 12.5 million US dollars, is an export credit **provided** to the Three Gorges project by the Canadian government, which will be used mainly for the management system of the Three Gorges project.
(i/ identity-91
	:ARG0 (t/ thing
		:ARG1-of (l/ loan)
		:ARG0-of (i2/ identity
			:ARG1 (m/ monetary-quantity
				:quant 12500000
				:unit (d/ dollar
					:mod (c/ country
						:wiki "United_States"
						:name (n/ name :op1 "US"))))))
	:ARG1 (c2/ credit
		:mod (e/ export-01)
		:ARG1-of (p/ provide
			:ARG0 (g/ government-organization
				:ARG0-of (g/ govern-01
					:mod (c3/ country
						:wiki "Canada"
						:name (n2/ name :op1 "Canada"))))
			:ARG2 (p2/ project
				:wiki "Three_Gorges_Dam"
				:name (n3/ name
					:op1 "Three"
					:op2 "Gorges"))
			:aspect Performance
			:modstr FullAff)
		:ARG1-of (u/ use-01
			:ARG2 (s/ system
				:poss p2
				:mod (m2/ manage-01))
			:mod (m3/ main)
			:aspect Activity
			:modstr FullAff))
	:aspect State
	:modstr FullAff)
	    
(s2 / sentence
   :temporal ((DCT :overlap s2i)
   	      (Future_Ref :includes s2u))
   :modal ((AUTH :FullAff s2i)
   	   (AUTH :FullAff s2p)
	   (AUTH :FullAff s2u))
   :coref (s1i :same-event s2p))
```
The `:subset-of` relation is also used to annotate the subset relations between two event mentions, with one referring to a subset of another, as is the case in [\[4-1-2 (3)\]](#4-1-2 (3)). Both the _arrest_ made in Germany and the one made in the Netherlands are subevents of the _arrests_ that were ordered by judge Fragnoli. Therefore, both the `s1a2` node and the `s1a3` node are annotated with a `:subset-of` relation to `s2a`.

<span id="4-1-2 (3)" label="4-1-2 (3)">4-1-2 (3)</span>

<span id="4-1-2 (3a)" label="4-1-2 (3a)">4-1-2 (3a)</span>
```
1 arrest took place in the Netherlands and another in Germany.
(a/ and
      :op1 (a2/ arrest-01
      	    :quant 1
            :location (c/ country
	    	  :wiki "Netherlands"
                  :name (n/ name
		  	:op1 "Netherlands"))
	    :aspect Performance
	    :modstr FullAff)
      :op2 (a3/ arrest-01
            :location (c2/ country
	    	  :wiki "Germany"
                  :name (n2/ name
		  	:op1 "Germany"))
            :mod (a4/ another)
	    :aspect Performance)
	    :modstr FullAff)

(s/ sentence
	:temporal ((DCT :before a2)
		   (DCT :before a3))
	:modal ((AUTH :FullAff a2)
		(AUTH :FullAff a3)))
```
<span id="4-1-2 (3b)" label="4-1-2 (3b)">4-1-2 (3b)</span>
```
The arrests were ordered by anti-terrorism judge fragnoli.
(o/ order-01
      :ARG0 (p/ person
      	    :wiki -
            :name (n/ name
	    	:op1 "Fragnoli")
            :ARG0-of (o2/ oppose-01
                  :ARG1 (t/ terrorism))
            :ARG0-of (h/ have-role-91
                  :ARG2 (j/ judge-01)))
      :ARG2 (a/ arrest-01
      	    :aspect Process
	    :quot o)
      :aspect Performance
      :modstr FullAff)
 
 (s2 / sentence
 	:temporal (s2a :before s2o)
	:modal ((AUTH :FullAff s2o)
		(AUTH :FullAff s2p)
		(s2p :PrtAff s2a))
  	:coref ((s2a :subset-of s1a2)
		(s2a :subset-of s1a3)))
```

- Script / subevent?

For now UMR does not annotate cases where one event is a subevent of another event, or when an event is part of a "script". These will be annotated under temporal relations.

```
 Reports suggest that the group of nine were having a picnic on Friday when they were abducted in the Saada province of Yemen. A spokesman for the Yemeni Embassy said "The foreigners ventured outside the city of Saada without the required police escorts due to the heightened security situation in the area.
```
  
  
[Back to Table of Contents](#toc)


### Part 4-2. Temporal Dependency

The temporal annotation in UMR is done at both the sentence level and the document level. For instance, a time expression that serves as the modifier of a predicate is annotated at the sentence level. In [\[4-2 (1)\]](#4-2 (1)), the time expression 
*April 1998* is annotated as a temporal modifier of the predicate *sign*. Likewise, the temporal relation between an event and its document creation time (DCT) is also annotated at the sentence level. In [\[4-2 (1)\]](#4-2 (1)), the temporal relation between *sign* and the DCT is annotated as `:temporal (b2 /before :op (n/now))`. The temporal relation between an event and a time expression is annotated when a time expression is present in the sentence. The temporal relation between an event and the DCT is annotated when this temporal relation is defined in that context. For example, while the relation between *signed* and the DCT is clearly defined, the temporal relation between *fight* and the DCT is not.


<span id="4-2 (1)" label="4-2 (1)">4-2 (1)</span>
```
In April 1998 Arab countries signed an anti-terrorism agreement that binds the signatories to coordinate to fight terrorism.
(s/ sign-02
      :ARG0 (c/ country
            :mod (e/ ethnic-group 
	    	  :wiki "Arabs"
                  :name (n/ name :op1 "Arab")))
      :ARG1 (a/ agree-01
            :topic (c2/ counter-01
                  :ARG1 (t/ terrorism))
            :ARG0-of (b/ bind-01
                  :ARG1 c
                  :ARG2 (c3/ coordinate-01
                        :ARG1 c
                        :purpose (f/ fight-01
                              :ARG0 c
                              :ARG1 t
			      :aspect Activity
			      :modstr FullAff)
			:aspect Activity
			:modpred b)
		  :aspect Activity
		  :modstr FullAff))
      :temporal (d / date-entity :year 1998 :month 4)
      :temporal (b2 /before :op (n/now))
      :aspect Performance))
 ```

In addition to temporal relations at the sentence level, we also annotate temporal relations at the document level.
The document-level temporal relations focus on event-event and time-time relations. Time-time relations are annotated when 
a relative time depends on another time expression for its interpretation.

Event-event relations are annotated only when the temporal relations are clearly supported by morpho-syntactic clues or when there is a clear temporal sequence can be inferred. 

The temporal dependency is divided into two passes: the first pass involves setting up the temporal
superstructure – the top levels of the dependency structure - and the second
pass involves adding events to the temporal dependency structure. The temporal superstructure contains the temporal expressions (timexs) in the text and pre-defined metanodes and their temporal relations to each other; the rest of the temporal dependency contains the events and their temporal relations to timexs and other events.

[Back to Table of Contents](#toc)

#### Part 4-2-1. Temporal superstructure

The highest level of the temporal
dependency is always a single `ROOT` node. The temporal
superstructure consists of two types of nodes: time expressions and
pre-defined metanodes. `depends-on` is the
relation that is used to link all nodes in the superstructure.

[Back to Table of Contents](#toc)

##### Part 4-2-1-1. Pre-defined metanodes

The first type of node in the temporal superstructure are the
pre-defined metanodes: `PAST_REF`, `PRESENT_REF`,
`FUTURE_REF`, and `DCT` (document creation time).
Unlike time expressions, the pre-defined metanodes don’t correspond to
linguistic material in the text. All four of the pre-defined metanodes
should be added at the top of every temporal dependency structure.
Whether or not they are actually used in the annotation will be
determined when events are annotated in the next pass. As mentioned
above, there is a generic `:depends-on` relation between all nodes
in the temporal superstructure; this is shown in Figure
[\[tempsuper\]](#tempsuper).

[Back to Table of Contents](#toc)

##### Part 4-2-1-2. Time expressions

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
are not represented in the temporal dependency structure at any level. They do influence the aspect annotation, however (see [Part 3-3-1](#part-3-3-1-Aspect)).


<!-- (they do influence the aspect annotation; see §[3](#aspectannotation)) -->

All locatable time expressions are represented in the temporal
superstructure. Locatable time expressions are divided between concrete
and vague time expressions. Vague time expressions (e.g. *nowadays, in
the old days*) are represented as the children of `PRESENT_REF`,
`PAST_REF`, or `FUTURE_REF`. Concrete time expressions
are divided into relative and absolute time expressions. Relative
concrete time expressions (*yesterday, the week before*) are represented
as the children of either `DCT` (as in *yesterday*) or
another concrete time expression on which they depend for their
interpretation (as in *the week before*). Finally, absolute concrete
time expressions (*in 2019*) are represented as children of
`ROOT`.

[Back to Table of Contents](#toc)

##### Part 4-2-1-3. Key events

For news stories only, the temporal superstructure includes the “key
event” in the text. The key event is the main event around which the
news story is centered. It is often mentioned in the title or first
sentence of the news story and referred to many times in the text. The
key event should be added to the superstructure, with a relation to the
timex which most specifically locates it in time.

[Back to Table of Contents](#toc)

#### Part 4-2-2. Temporal relations

#### Part 4-2-2-1. Choosing the right temporal relation

The second pass in the temporal annotation involves placing events on to the
temporal dependency structure based on their temporal relations with
other events and time expressions. Unlike the modal dependency structure
which includes all of the events identified in the first pass (see [Part 3-1-1](#part-3-1-1-eventive-concepts) for event ID guidelines), the
temporal dependency structure only includes events whose aspect
annotation is NOT `State`. That is, events annotated with the
aspect value `State` are not annotated for temporal location.
This is because states, by definition, don’t involve change; therefore,
they generally cannot be located on a timeline in the same way as
non-stative events.

Each (non-stative) event will be annotated as the child of either a time
expression in the superstructure or another event (or both). The set of
temporal relations are shown below. Note that the labels characterize
the relation from child to parent.

`:contained`: child is entirely contained within the parent; parent begins before child and parent ends after child (Note: this is called ‘Includes’ in Zhang & Xue 2018).

`:after`: child is after parent.  

`:before`: child is before parent.

`:overlap`: child and parent overlap (either partially or fully).  

The goal of this temporal annotation scheme is to give each event the
most precise temporal location possible. We also want to avoid adding
annotations which do not give any additional information (i.e., the
relation falls out logically from the other annotations). Annotators
should proceed through the steps below for each event until it has at
least one temporal annotation.

1.  The most specific location for any event will be a
    `:contained` relation to a timex (although see the
    exception below). If possible, link the event to a time expression
    (timex). This can be any timex in the superstructure, but most of
    the time it will be in the same clause as the event. If the event
    cannot be related to a timex, proceed to 2. If the event is related
    to a timex, proceed to 3.
    
      - **Exception:** The only scenario in which an event which has a clear temporal
        relation with a timex doesn’t need to have this relation
        annotated is when the relation logically falls out from other
        annotations. This is the case when an event is a subevent of an
        event that is `:contained` in a timex. That is, if
        event A is `:contained` within event B (i.e., a
        subevent) and event B is `:contained` within a timex,
        then logically, event A must also be `:contained`
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
    
      - It has a `:modstr Aff` relation to the same conceiver as the
        child event in the modal annotation OR
    
      - It has the same modal relation to the same conceiver/event as
        the child event in the modal annotation OR
    
      - It is either the parent or the child of the event in the modal
        dependency.

3.  Even if the event can be related to a timex, its temporal location
    may be made more precise by specifying a second relation to an
    event. Only add an event-event relation if it makes the temporal
    location of the child event more specific. In practice, this means
    that events which are `:contained` within a timex will
    only be related to events `:contained` within the same
    timex or events which are not contained within any timex. (That is,
    two events `:contained` within different timexs should not
    be related to each other.) Aside from that, follow the same rules as
    in 2 for selecting a good parent event.

4.  If an event cannot be related to either a timex or another event,
    then relate it to the key event in the text, if there is one.

5.  If an event cannot be related to a timex, another event, or the key
    event, then link it to a tense metanode.

In order to demonstrate how these rules work, let’s look at the
annotation of ([\[4-2-2-1 (1)\]](#4-2-2-1 (1))) below.

<span id="4-2-2-1 (1)" label="4-2-2-1 (1)">\[4-2-2-1 (1)\]</span> 
Key event: landslide\_KEY
```
Lerias said that many Guinsaugon residents had been evacuated after landslides earlier in the week had killed more than 20 people on Leyte, but that many had returned Friday because the rains had stopped and the sun had come out.
(s/ say-01
      :ARG0 (p/ person
      	    :wiki -
            :name (n/ name :op1 "Lerias"))
      :ARG1 (c/ contrast
      	    :ARG1 (e/ evacuate-01
	    	:ARG2 (p2/ person
			:ARG0-of (r/ reside-01
				:ARG1 (c2/ city
					:wiki "Saint_Bernard,_Southern_Leyte"
					:name (n2/ name :op1 "Guinsaugon")))
			:quant (m/ many))
		:temporal (a/ after
			:op1 (k/ kill-01
				:ARG0 (l/ landslide
					:aspect Process)
				:ARG1 (p3/ person
					:quant (m2/ more-than :op1 20))
				:place (i/ island
					:wiki "Leyte
					:name (n3/ name :op1 "Leyte"))
				:temporal (w/ week)
				:temporal (b/ before
					:op1 s)
				:aspect Performance
				:quot s
				:modstr FullAff))
		:aspect Performance
		:quot s
		:modstr FullAff)
	    :ARG2 (r2/ return-01
	    	:ARG1 p2
		:temporal (d/ date-entity
			:weekday (f/ Friday))
		:ARG1-of (c3/ cause-01
			:ARG0 (a/ and
				:op1 (r3/ rain
					:aspect Endeavor
					:quot s
					:modstr FullAff)
				:op2 (c4/ come-out-09
					:ARG1 (s2/ sun)
					:aspect Performance
					:quot s
					:modstr FullAff)
		:aspect Performance
		:quot s
		:modstr FullAff)
	:aspect Performance
	:modstr FullAff)
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

For *say*, it does not have a `:contained` relation
with either of the time expressions (`Friday` and `earlier in the week`) in the example, so we move to step
2. It’s also the first event in the sentence, so (assuming it can’t be
linked to any of the events in the previous sentence), we move to step
4. We do know that *say* occurred after the key event in the
text, therefore we can add `(landslide_KEY :after say)` and
move on to the next event.

*Evacuate* is not necessarily `:contained` within
either of the timexs, so we move to step 2. Since *evacuate*
is a reported event, the reporting event, *say*, is an
appropriate parent in the temporal dependency; we can add
`(say :before evacuate)`.

Next, we have *landslide*. Following step 1,
*landslide* is `:contained` within the timex
*earlier in the week*, so we add
`(earlier_week :contained landslide)`. Then, we move to step 3
and see if the temporal location of *landslide* can be made
more specific by adding an event relation. The immediately preceding
event in the text, *evacuate*, has a clear temporal relation
and the same modal annotation as *landslide* and is therefore
a good parent. We can add `(evacuate :before landslide)`.

Then, we move on to *kill*. Like *landslide*,
*kill* is `:contained` within the timex *earlier in
the week*, so we can add `(earlier_week :contained kill)`.
Then we move to step 3 and can add a relation to *landslide*:
`(landslide :overlap kill)`.

*Return* can be linked to the timex *Friday*:
`(Friday :contained return)`. Moving to step 3, we look earlier
in the sentence for a parent event. Both *kill* and
*landslide* are `:contained` within a different timex, so they
don’t make good parents. That is, by virtue of the fact that
*return* is `:contained` on *Friday* and
*kill* and *landslide* are `:contained`
in *earlier in the week*, it logically falls out that
*return* happened after both *kill* and
*landslide*; therefore, we don’t need to annotate this
relation. *Evacuate*, however, is not `:contained`
within a timex and has the same modal annotation as *return*;
so, we can add `(evacuate :after return)`.

*Rain* does not have a `:contained` relation with a
timex, so we move to step 2. *Return* makes a good parent for
*rain* since it has the same modal annotation, so we can
add  
`(return :before rain)`.

Finally, *come-out* also does not have a
`:contained` relation with a timex. *rain* makes a
good parent, since it has the same modal annotation, so we can add
`(rain :overlap come-out)`. This gives us the full annotation
below.

| Events    | Modal annotation   | Temporal annotation                |
| :-------- | :----------------- | :--------------------------------- |
| say       | Pos(say,LERIAS)    | (landslide_KEY :after say)         |
| evacuate  | Pos(evacuate,say)  | (say :before evacuate)             |
| landslide | Pos(landslide,say) | (earlier_week :contained landslide)|
|           |                    | (evacuate :before landslide)       |
| kill      | Pos(kill,say)      | (earlier_week :contained kill)     |
|           |                    | (landslide :overlap kill)          |
| return    | Pos(return,say)    | (Friday :contained return)         |
|           |                    | (evacuate :after return)           |
| rain      | Pos(rain,say)      | (return :before rain)              |
| come-out  | Pos(come-out,say)  | (rain :overlap come-out)           |

[Back to Table of Contents](#toc)

##### Part 4-2-2-2. Contained or Overlap

Following the definition of the `:contained` and the
`:overlap` relations, `:overlap` must be used rather
than `:contained` for events that are perfectly simultaneous
(beginning and ending at the exact same time point). The
`:contained` relation will instead be used for all relations
where both the beginning and ending of one event are included within the
temporal duration of a second event - this includes subevent structure
and also events which have a purely temporal (and not causal or
conceptual) relation between them.

[Back to Table of Contents](#toc)

##### Part 4-2-2-3. Causally-related events

Causal relations between events are always annotated as
`:after` relations. This means that in examples such as *the
crops grew well because it rained enough*, `(rain :after grow)`
is annotated even though the causing event (raining) and the caused
event (growing) partly overlap. If the causal relationship is explicitly
predicated, it is identified as a separate event. It is then annotated
as `:after` the causing event, and the caused event is
annotated as following it. Therefore, *the opening of the food can
prompted my cat to meow* is annotated as `(open :after prompt)`
and `(prompt :after meow)`.

[Back to Table of Contents](#toc)

##### Part 4-2-2-4. Deontic modal events

For deontics and purpose clauses, the deontic or purpose complement
(e.g., *go* in *Mary wants to go*) is annotated with with an
`:after` relation to the deontic predicate (here, *want*).
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

[Back to Table of Contents](#toc)

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

![Modal dependency structure](https://github.com/umr4nlp/umr-guidelines/blob/master/Guidelines_figures/Modal%20Dep_2022.jpg)

```
Martin said that the package has probably already arrived.
(s/ say-01  
	:ARG0 (p/ person
		:name (n/ name :op1 "Martin")
	:ARG1 (a/ arrive-01  
		:ARG1 (p/ package
			:ref-number Singular)  
		quot: s
		modstr: PrtAff)
	modstr: Aff)
(s/ sentence
	:temporal ((PAST_REF :contained s1s)
		   (s1s :before s1a))
	**:modal ((AUTH :FullAff s1p)
		(AUTH :FullAff s1s)
		(s1p :PrtAff s1a)))**
```

The *say*-event and the *arrive*-event each get a modal strength value (`:modstr`), which can then be represented
in the dependency as an edge between the event and the relevant conceiver/source. The
`:quot` value indicates than an event is
being reported, and the participant role annotation can be used to
automatically select the conceiver for the reported event(s), here,
*Martin*.

This simplified, mostly sentence-level, annotation process is step 0 of the road map for modal annotation. Step 1 builds on this step to end up at a fully specified modal dependency structure. This means that Stage 1 annotation involves first doing the Stage 0 modality annotations. (This contrasts with participant roles, where annotators can largely ignore Stage 0 if the annotation language has existing frame files.)

[Back to Table of Contents](#toc)

#### Part 4-3-1. Stage 0

There are two types of modal annotations at Stage 0: a
`:modstr` annotation that consists of a
single epistemic strength/polarity value, and a dependency annotation
that indicates a relation between two events. There are two dependency
relations: `:modpred` for the link between a
modal event and the event(s) that it modalizes, and
`:quot` for the link between a reporting
event and the event(s) that it reports. Additionally, events in purpose clauses and events in conditional constructions must be taken up in the modal dependency tree. The right structure of the modal dependency graph for these events will be extrapolated from the sentence-level annotation: events in purpose clauses are daughters of events in the main clause they depend on, and are connected to them with the `:purpose` participant role. This can be leveraged to embed the purpose-event underneath the correct parent in the modal dependency graph as well. For conditionals, similarly, the protasis event will be embedded under the apodosis event with a `:condition` relation, or the protasis and apodosis events will both be `:ARG1` and `:ARG2` of a `have-condition-91` node. Again, this information will be taken up in the eventual modal dependency graph without annotators needing to indicate it a second time in the document-level modal annotation workflow.
The `:modstr` annotation applies to all events, except for those under the scope of a modal identified as its own event (i.e., events with `:mod` relations). This
is summarized below.

<div id="tab:modal_relations">

| **Event type** | **UMR Treatment** |
| :------------------------------- |:------------------------------------------------------------------------------------------|
| Events under the scope of modals | `:modpred` relation to CPT |
| Events under the scope of reporting events| `:modstr` annotation, `:quot` relation to reporting event |
| All other events | `:modstr` annotation |

Table 14: Modal relations at Stage 0
</div>

[Back to Table of Contents](#toc)

##### Part 4-3-1-1. modstr values

The modal strength values correspond to epistemic strength, i.e. the
author or conceiver’s certainty about the occurrence of the event in the real world, or certainty about another conceiver’s mental content. Based on Boye (2012), a typological study of modal systems across languages, and following FactBank (Pustejovsky et al. 2005), the UMR annotation is based around three levels of modal strength: `Full`, `Partial`, and `Neutral`, illustrated in [\[4-3-1-1 (1)\]](#4-3-1-1 (1)).

<span id="4-3-1-1 (1)" label="4-3-1-1 (1)">\[4-3-1-1 (1)\]</span>

<span id="4-3-1-1 (1a)" label="4-3-1-1 (1a)">\[4-3-1-1 (1a)\]</span> Full:  
The cat already **ate** breakfast.

<span id="4-3-1-1 (1b)" label="4-3-1-1 (1b)">\[4-3-1-1 (1b)\]</span>
Partial:  
The cat <u>probably</u> already **ate** breakfast.  

<span id="4-3-1-1 (1c)" label="4-3-1-1 (1c)">\[4-3-1-1 (1c)\]</span>
Neutral:  
The cat <u>might</u> have already **eaten** breakfast.

The `Full` modal strength value, as in [\[4-3-1-1 (1a)\]](#4-3-1-1 (1a)), corresponds to complete certainty; that is, the conceiver is 100% certain that the event occurs in the real world. The `Neutral` modal strength value, shown in [\[4-3-1-1 (1c)\]](#4-3-1-1 (1c)), indicates the possibility of the event; essentially, this corresponds to 50/50 certainty that the event occurs in the real world. The `Partial` modal strength value, as in [\[4-3-1-1 (1b)\]](#4-3-1-1 (1b)), falls between the `Full` and `Neutral` values; the conceiver believes that more likely than not, the event occurs in the real world.

But, `Full`, `Partial`, and `Neutral` aren’t the only possible modal strength annotation values. Languages differ in the modal strength distinctions that are conventionalized in their grammar. In order to accommodate these differences, we use a typological lattice of annotation values, constructed based on the structure of the annotation category across languages (Van Gysel et al. 2019).

One level of granularity in the lattice is designated as the “base
level”: annotators are encouraged to use categories from this level as
the default. These values are selected as the base level because these
distinctions occur the most frequently across languages. The higher and lower levels, respectively, contain equally typologically-motivated coarser-grained and finer-grained categories, which can be used when a language conventionalizes these distinctions in its grammar. Such lattices capture the idea that many semantic categories are structured as hierarchical scales, where the middle values can group together with either end, but the extremes of the scale are highly unlikely to be categorized together in any language. For example, no language has a grammatical form that is used for both `Full` and `Neutral` epistemic strength, but not `Partial`. The typological lattice for epistemic strength is shown below.

![Modal strength lattice](https://github.com/umr4nlp/umr-guidelines/blob/master/Guidelines_figures/Affirmative%20Modal%20Strength%20Lattice_2022.png)

![Modal strength lattice](https://github.com/umr4nlp/umr-guidelines/blob/master/Guidelines_figures/Negative%20Modal%20Strength%20Lattice_2022.png)

This lattice is based around the base level of `Full` vs. `Partial` vs.
`Neutral`, but also allows for the annotation of more coarse-grained
values that lump together the distinctions in the base level, and more
fine-grained annotation values. For contexts where it is unclear if the modal strength is `Full` or `Partial`, the `Non-neutral` value can be used; if it is unclear whether the modal strength is `Partial` or `Neutral`, then the `Non-full` value can be used. The most fine-grained modal strength values are generally used with languages that have grammatical forms that encode the relevant distinction.

Also following FactBank (Pustejovsky et al. 2006), the `:modstr`
annotation combines the epistemic strength values with a binary polarity distinction (`Affirmative`, `Negative`). This results in six modal strength/polarity values for the default level, shown below. Both the affirmative values and the negative values have their own set of related coarse-grained and fine-grained values.

<div>

| **Label**                              | **Value**                              |
| :------------------------------------- | :------------------------------------- |
| ```FullAff```     | full strength, affirmative polarity    |
| ```PrtAff```     | partial strength, affirmative polarity |
| ```NeutAFf```    | neutral strength, affirmative polarity |
| ```NeutNeg``` | neutral strength, negative polarity    |
| ```PrtNeg```  | partial strength, negative polarity    |
| ```FullNeg```    | full strength, negative polarity       |

</div>

These values and their interpretation are shown below; the corresponding FactBank values are in parentheses.

```FullAff```: full affirmative support; complete certainty that the event occurs (CT+)  
```PrtAff```: partial affirmative support; there is strong, but not definitive certainty that the event occurs (PR+)  
```NeutAff```: affirmative neutral support; there is neutral certainty that the event occurs/doesn’t occur; event is expressed positively (PS+)  
```NeutNeg```: negative neutral support; there is neutral certainty that the event occurs/doesn’t occur; negation of event is expressed (PS-)  
```PrtNeg```: partial negative support; there is strong but not definitive certainty that the event does not occur (PR-)  
```FullNeg```: full negative support; complete certainty that the event does not occur (CT-)

Degree of certainty corresponds most straightforwardly to the degree of confidence of a conceiver (often, the author) in the occurrence of an episodic event, i.e. the epistemic continuum from certainty to
possibility. We use these same values for the evidential continuum from direct evidence to second-hand (reported or inferred) evidence; see [Part 4-3-1-1-2](#part-4-3-1-1-2-evidential-justification) below). And these values are
interpreted into the domain of future-oriented or deontic modality, as
explained in [Part 4-3-1-1-3](#part-4-3-1-1-3-future-events-and-deontic-modality). The interpretation of
the value - as epistemic, evidential or deontic - is not reflected in
the modal strength annotation.

[Back to Table of Contents](#toc)

##### Part 4-3-1-1-1. Non-future events

For non-future (non-deontic) events, the `modstr` values correspond to the author’s level of certainty towards the occurrence of the event in the real world. Events presented as fact are annotated with
`FullAff`, while events for which the author categorically denies their occurrence are annotated `FullNeg`. When the author doesn’t present the
event as fact, but has a higher level of certainty towards the event
either being true or not true, this is annotated as
`PrtAff` or, when the polarity is negative, `PrtNeg`. When the author doesn’t lean either direction towards the event being true in the real world or not, the event is annotated as `NeutAff` or
`NeutNeg`, depending on the polarity of the
linguistic expression. These strength values are exemplified in
([\[4-3-1-1-1 (1)\]](#4-3-1-1-1 (1))).


<span id="4-3-1-1-1 (1)" label="4-3-1-1-1 (1)">\[4-3-1-1-1 (1)\]</span>

<span id="4-3-1-1-1 (1a)" label="4-3-1-1-1 (1a)">\[4-3-1-1-1 (1a)\]</span>   
```
The dog barked last night.
(b/ bark-01
	:ARG0 (d/ dog
		:ref-number Singular)
	:temporal (n/ night
		:mod (l/ last))
	:aspect Endeavor
	:modstr FullAff)  
```
<span id="4-3-1-1-1 (1b)" label="4-3-1-1-1 (1b)">\[4-3-1-1-1 (1b)\]</span>  
```
The dog probably barked last night.
(b/ bark-01
	:ARG0 (d/ dog
		:ref-number Singular)
	:temporal (n/ night
		:mod (l/ last))
	:aspect Endeavor
	:modstr PrtAff)  
```
<span id="4-3-1-1-1 (1c)" label="4-3-1-1-1 (1c)">\[4-3-1-1-1 (1c)\]</span>
```
The dog may have barked last night.
(b/ bark-01
	:ARG0 (d/ dog
		:ref-number Singular)
	:temporal (n/ night
		:mod (l/ last))
	:aspect Endeavor
	:modstr NeutAff)  
```
<span id="4-3-1-1-1 (1d)" label="4-3-1-1-1 (1d)">\[4-3-1-1-1 (1d)\]</span> 
```
The dog may not have barked last night.
(b/ bark-01
	:ARG0 (d/ dog
		:ref-number Singular)
	:temporal (n/ night
		:mod (l/ last))
	:aspect Endeavor
	:modstr NeutNeg)  
```
<span id="4-3-1-1-1 (1e)" label="4-3-1-1-1 (1e)">\[4-3-1-1-1 (1e)\]</span>
```
The dog probably didn't bark last night.
(b/ bark-01
	:ARG0 (d/ dog
		:ref-number Singular)
	:temporal (n/ night
		:mod (l/ last))
	:aspect Endeavor
	:modstr PrtNeg)  
``` 
<span id="4-3-1-1-1 (1f)" label="4-3-1-1-1 (1f)">\[4-3-1-1-1 (1f)\]</span>
```   
The dog didn't bark last night.
(b/ bark-01
	:ARG0 (d/ dog
		:ref-number Singular)
	:temporal (n/ night
		:mod (l/ last))
	:aspect Endeavor
	:modstr FullNeg)  
```  
[Back to Table of Contents](#toc)

##### Part 4-3-1-1-2. Evidential justification

Following Boye (2012) and Saurí and Pustejovsky (2009), we conflate evidential justification with epistemic support. Boye (2012) finds that there is cross-linguistic evidence for lumping epistemic support and evidential justification together into the same relations. Languages may encode direct evidential justification (sensory perception) with the same forms as full epistemic support; indirect justification (hearsay, inferential) may be encoded by the same forms as partial epistemic support.

Example [\[4-3-1-1-2 (1)\]](#4-3-1-1-2 (1)) shows how direct and indirect justification correspond to epistemic support.

<span id="4-3-1-1-2 (1)" label="4-3-1-1-2 (1)">\[4-3-1-1-2 (1)\]</span>

<span id="4-3-1-1-2 (1a)" label="4-3-1-1-2 (1a)">\[4-3-1-1-2 (1a)\]</span> 
```
(I saw) Mary feed the cat.
(s/ see-01
	:ARG0 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:ARG1 (f/ feed-01
		:ARG0 (p2/ person
			:name (n/ name :op1 "Mary"))
		:ARG2 (c/ cat
			:ref-number Singular)
		:aspect Performance
		**:modstr FullAff**)
	:aspect State
	:modstr FullAff)
```
<span id="4-3-1-1-2 (1b)" label="4-3-1-1-2 (1b)">\[4-3-1-1-2 (1b)\]</span> 
```
Mary must have fed the cat.
(f/ feed-01
	:ARG0 (p/ person
		:name (n/ name :op1 "Mary"))
	:ARG2 (c/ cat
		:ref-number Singular)
	:aspect Performance
	**:modstr PrtAff**)
```

In [\[4-3-1-1-2 (1a)\]](#4-3-1-1-2 (1a)), the author has direct knowledge of the feeding event, by way of witnessing it. Therefore, *feed* is annotated with `Aff` modal strength. In [\[4-3-1-1-2 (1b)\]](#4-3-1-1-2 (1b)), however, *must* signals that the author is inferring that the feeding event occurred without direct, perceptual knowledge. Therefore, *fed* in [\[4-3-1-1-2 (1b)\]](#4-3-1-1-2 (1b)) is annotated with `Prt` modal strength.

[Back to Table of Contents](#toc)

##### Part 4-3-1-1-3. Future events and deontic modality

For events presented as (potentially) happening in the future,
`:modstr` refers to the predictability of
the occurrence of the event in the future, as presented by the author.
Predictive future has full strength (`FullAff`
or `FullNeg`); intentions and commands
correspond to partial strength (`PrtAff` or
`PrtNeg`); and desire and permission
correspond to neutral (`NeutAff` or
`NeutNeg`) strength. Keep in mind that events under the scope of modals identified as their own event don't receive any `:modstr` value at all. This section refers to deontic meanings indicated by grammaticalized modals that don't fit the criteria to be identified as events.

This is illustrated in ([\[4-3-1-1-3 (1)\]](#4-3-1-1-3 (1))).

<span id="4-3-1-1-3 (1)" label="4-3-1-1-3 (1)">\[4-3-1-1-3 (1)\]</span>

<span id="4-3-1-1-3 (1a)" label="4-3-1-1-3 (1a)">\[4-3-1-1-3 (1a)\]</span>  
```
I will go to Santa Fe.
(g/ go-01
	:ARG1 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:ARG4 (c/ city
		:wiki "Santa_Fe,_New_Mexico"
		:name (n/ name
			:op1 "Santa"
			:op2 "Fe"))
	:aspect Performance
	:modstr FullAff)
```
<span id="4-3-1-1-3 (1b)" label="4-3-1-1-3 (1b)">\[4-3-1-1-3 (1b)\]</span>   
```
You must go to Santa Fe.
(g/ go-01
	:ARG1 (p/ person
		:ref-person 2nd
		:ref-number Singular)
	:ARG4 (c/ city
		:wiki "Santa_Fe,_New_Mexico"
		:name (n/ name
			:op1 "Santa"
			:op2 "Fe"))
	:aspect Performance
	:modstr PrtAff
	:mode Imperative)
```

<span id="4-3-1-1-3 (1c)" label="4-3-1-1-3 (1c)">\[4-3-1-1-3 (1c)\]</span>   
```
You can go to Santa Fe.
(g/ go-01
	:ARG1 (p/ person
		:ref-person 2nd
		:ref-number Singular)
	:ARG4 (c/ city
		:wiki "Santa_Fe,_New_Mexico"
		:name (n/ name
			:op1 "Santa"
			:op2 "Fe"))
	:aspect Performance
	:modstr NeutAff)
```
The predictive future, as in [\[4-3-1-1-3 (1a)\]](#4-3-1-1-3 (1a)), is annotated with
full modal strength because it presents the future event as a certainty
(i.e., it is as certain as is possible for future events). Commands, as
in [\[4-3-1-1-3 (1b)\]](#4-3-1-1-3 (1b)), are annotated with partial modal strength
because they present the future event as less likely than the predictive
future, but more likely to happen than the neutral strength deontics.
Finally, permission, as in [\[4-3-1-1-3 (1c)\]](#4-3-1-1-3 (1c)), is annotated as
neutral strength, since even if someone has permission to do something, there is no guarantee they will.

[Back to Table of Contents](#toc)

##### Part 4-3-1-2. modpred relation

Events under the scope of a modal identified as its own event are only
annotated with a `:modpred` relation to the
relevant modal. This is shown below in [\[4-3-1-2 (1)\]](#4-3-1-2 (1)).

<span id="4-3-1-2 (1)" label="4-3-1-2 (1)">\[4-3-1-2 (1)\]</span>

<span id="4-3-1-2 (1a)" label="4-3-1-2 (1a)">\[4-3-1-2 (1a)\]</span> 
```
Mary wants to visit France.
(w/ want-01
	:ARG0 (p/ person
		:name (n/ name :op1 "Mary"))
	:ARG1 (v/ visit-01
		:ARG0 p
		:ARG1 (c/ country
			:wiki "France"
			:name (n/ name :op1 "France"))
		:aspect Performance
		:modpred w
	:aspect State
	:modstr FullAff

(s/ sentence
	:temporal ((DCT :overlap s1w)
		   (s1w :after s1v))
	:modal ((AUTH :FullAff s1p)
		(s1p :FullAff s1w)
		(s1w :Unsp s1v))
```
<span id="4-3-1-2 (1b)" label="4-3-1-2 (1b)">\[4-3-1-2 (1b)\]</span> 
```
Rob thinks the dog escaped through the fence.
(t/ think-01
	:ARG0 (p/ person
		:name (n/ name :op1 "Rob"))
	:ARG1 (e/ escape-01
		:ARG0 (d/ dog
			:ref-number Singular)
		:path (f/ fence)
		:aspect Performance
		:modpred t)
	:aspect State
	:modstr FullAff)
(s/ sentence
	:temporal ((DCT :overlap s1t)
		   (s1t :before s1e))
	:modal ((AUTH :FullAff s1p)
		(s1p :FullAff s1t)
		(s1t :Unsp s1e)))
```
<span id="4-3-1-2 (1c)" label="4-3-1-2 (1c)">\[4-3-1-2 (1c)\]</span> 
```
They probably decided to leave on Monday.
(d/ decide-01
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Plural)
	:ARG1 (l/ leave-01
		:ARG0 p
		:temporal (d/ date-entity
			:weekday (m/ Monday))
		:aspect Performance
		:modpred d)
	:aspect Performance 
	:modstr PrtAff) 
(s/ sentence
	:temporal ((PAST_REF :contained s1d)
		   (s1m :contained s1l))
	:modal ((AUTH :PrtAff s1p)
		(s1p :FullAff s1d)
		(s1d :Unsp s1l)))
```
<span id="4-3-1-2 (1d)" label="4-3-1-2 (1d)">\[4-3-1-2 (1d)\]</span> 
```
His parents forbid him from smoking.
(f/ forbid-01
	:ARG0 (p/ person
		:ARG0-of (k/ kinship)
			:ARG1 (p2/ person
				:ref-person 3rd
				:ref-number Singular)
			:ARG2 (p3/ parent)
		:ref-number Plural)
	:ARG1 (s/ smoke-01
		:ARG0 p2
		:aspect Process
		:modpred f)
	:ARG2 p2
	:aspect State
	:modstr FullAff)
(s/ sentence
	:temporal ((DCT :overlap s1f)
		   (s1f :overlap s1s))
	:modal ((AUTH :FullAff s1p)
		(s1p :FullAff s1f)
		(s1f :Unsp s1s)))
```

Note that the modal itself is annotated with a
`:modstr` value (if it is not under the
scope of another modal). The actual modal value imparted by the modal
event is not annotated at Stage 0. It will be taken up in the lexical entries of modal complement-taking predicates and space-builders as the lexicon is being built, and will then automatically replace the unspecified link between the modal event and the modalized event in the document-level structure.

[Back to Table of Contents](#toc)

##### Part 4-3-1-3. quot relation

Events under the scope of a reporting predicate or a speech predicate
are annotated with a `:quot` relation to the
reporting or speech predicate. Unlike events under the scope of modals,
these events are also annotated with a
`:modstr` value.

<span id="4-3-1-3 (1)" label="4-3-1-3 (1)">\[4-3-1-3 (1)\]</span>

<span id="4-3-1-3 (1)" label="4-3-1-3 (1)">\[4-3-1-3 (1)\]</span> 
```
Mary said that she went to Santa Fe.
(s/ say-01
	:ARG0 (p/ person
		:name (n/ name :op1 "Mary"))
	:ARG1 (g/ go-01
		:ARG1 p
		:ARG4 (c/ city
			:wiki "Santa_Fe,_New_Mexico"
			:name (n2/ name
				:op1 "Santa"
				:op2 "Fe))
		:aspect Performance
		:modstr FullAff
		:quot s
	:aspect Performance
	:modstr FullAff) 
(s/ sentence
	:temporal ((PAST_REF :contained s1s)
		   (s1s :before s1g))
	:modal ((AUTH :FullAff s1s)
		(AUTH :FullAff s1p)
		(s1p :FullAff s1g)))
```
<span id="4-3-1-3 (1a)" label="4-3-1-3 (1a)">\[4-3-1-3 (1a)\]</span> 
```
The New York Times reported that Congress voted on the bill this afternoon.
(r/ report-01
	:ARG0 (n/ newspaper
		:name (n2/ name
			:op1 "The"
			:op2 "New"
			:op3 "York"
			:op4 "Times")
		:wiki "The_New_York_Times")
	:ARG1 (v/ vote-01
		:ARG0 (g/ government-organization
			:name (n3/ name :op1 "Congress")
			:wiki "United_States_Congress")
		:ARG1 (b/ bill
			:ref-number Singular)
		:temporal (a/ afternoon
			:mod (t/ this))
		:aspect Performance
		:modstr FullAff
		:quot r)
	:aspect Performance
	:modstr FullAff)
(s/ sentence
	:temporal ((PAST_REF :contained s1r)
		   (s1a :contained s1v))
	:modal ((AUTH :FullAff s1r)
		(AUTH :FullAff s1n)
		(s1n :FullAff s1v)))
```
<span id="4-3-1-3 (1b)" label="4-3-1-3 (1b)">\[4-3-1-3 (1b)\]</span> 
```
Mary might have said that she went to Santa Fe.
(s/ say-01
	:ARG0 (p/ person
		:name (n/ name :op1 "Mary"))
	:ARG1 (g/ go-01
		:ARG1 p
		:ARG4 (c/ city
			:wiki "Santa_Fe,_New_Mexico"
			:name (n2/ name
				:op1 "Santa"
				:op2 "Fe))
		:aspect Performance
		:modstr FullAff
		:quot s
	:aspect Performance
	:modstr NeutAff) 
(s/ sentence
	:temporal ((PAST_REF :contained s1s)
		   (s1s :before s1g))
	:modal ((AUTH :NeutAff s1s)
		(AUTH :NeutAff s1p)
		(s1p :FullAff s1g))) 
```
<span id="4-3-1-3 (1c)" label="4-3-1-3 (1c)">\[4-3-1-3 (1c)\]</span> 
```
Mary didn’t say that she went to Santa Fe.
(s/ say-01
	:ARG0 (p/ person
		:name (n/ name :op1 "Mary"))
	:ARG1 (g/ go-01
		:ARG1 p
		:ARG4 (c/ city
			:wiki "Santa_Fe,_New_Mexico"
			:name (n2/ name
				:op1 "Santa"
				:op2 "Fe))
		:aspect Performance
		:modstr FullAff
		:quot s
	:aspect Performance
	:modstr FullNeg) 
(s/ sentence
	:temporal ((PAST_REF :contained s1s)
		   (s1s :before s1g))
	:modal ((AUTH :FullNeg s1s)
		(AUTH :FullNeg s1p)
		(s1p :FullAff s1g))) 
```
<span id="4-3-1-3 (1d)" label="4-3-1-3 (1d)">\[4-3-1-3 (1d)\]</span> 
```
Mary said that John might have gone to Santa Fe.
(s/ say-01
	:ARG0 (p/ person
		:name (n/ name :op1 "Mary"))
	:ARG1 (g/ go-01
		:ARG1 (p2/ person
			:name (n2/ name :op1 "John"))
		:ARG4 (c/ city
			:wiki "Santa_Fe,_New_Mexico"
			:name (n3/ name
				:op1 "Santa"
				:op2 "Fe))
		:aspect Performance
		:modstr NeutAff
		:quot s
	:aspect Performance
	:modstr FullAff) 
(s/ sentence
	:temporal ((PAST_REF :contained s1s)
		   (s1s :before s1g))
	:modal ((AUTH :FullNeg s1s)
		(AUTH :NeutAff s1p)
		(s1p :NeutAff s1g))) 
```
<span id="4-3-1-3 (1e)" label="4-3-1-3 (1e)">\[4-3-1-3 (1e)\]</span> 
```
Mary said that John probably didn’t go to Santa Fe.
(s/ say-01
	:ARG0 (p/ person
		:name (n/ name :op1 "Mary"))
	:ARG1 (g/ go-01
		:ARG1 (p2/ person
			:name (n2/ name :op1 "John"))
		:ARG4 (c/ city
			:wiki "Santa_Fe,_New_Mexico"
			:name (n3/ name
				:op1 "Santa"
				:op2 "Fe))
		:aspect Performance
		:modstr PrtNeg
		:quot s
	:aspect Performance
	:modstr FullAff) 
(s/ sentence
	:temporal ((PAST_REF :contained s1s)
		   (s1s :before s1g))
	:modal ((AUTH :FullNeg s1s)
		(AUTH :PrtNeg s1p)
		(s1p :PrtNeg s1g)))  
```
As can be seen above, both the reporting predicate and the reported
events are annotated with a `:modstr` value.
The `:modstr` value of the reporting
predicate corresponds to the author’s certainty that the reporting event
happened. The `:modstr` value associated
with the reported events corresponds to the certainty with which the
sayer/reporter reports the events. For example, in
[\[4-3-1-3 (1d)\]](#4-3-1-3 (1d)), the author is certain about the saying event,
so it is annotated with `Aff`; but Mary is
unsure about the reality of the going event, and therefore it is
annotated with `Neut` modal strength.

[Back to Table of Contents](#toc)

##### Part 4-3-1-4. purpose relation

Events in purpose clauses are annotated with both a
`:modstr` value in the document-level annotation, and with the `:purpose` participant role relation to the main clause event in the sentence-level annotation.

<span id="4-3-1-4 (1)" label="4-3-1-4 (1)">\[4-3-1-4 (1)\]</span>
```
They dropped water in order to fight the fire.
(d/ drop-01
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Plural)
	:ARG1 (w/ water)
	:purpose (f/ fight-01
		:ARG0 p
		:ARG1 (f/ fire)
		:aspect Activity
		:modstr FullAff)
	:aspect Performance
	:modstr FullAff)
(s/ sentence
	:temporal ((PAST_REF :contained s1d)
		   (s1d :after :s1f))
	:modal ((AUTH :FullAff s1d)
		(AUTH :FullAff s1p)
		(s1p :PrtAff purpose)
		(purpose :FullAff s1f)))
```
<span id="4-3-1-4 (2)" label="4-3-1-4 (2)">\[4-3-1-4 (2)\]</span>
```
He walked quickly in order to not arrive late.
(w/ walk-01
	:ARG0 (p/ person
		:ref-person 3rd
		:ref-number Singular)
	:manner (q/ quickly)
	:purpose (a/ arrive-01
		:ARG1 p
		:temporal (l/ late)
		:aspect Performance
		:modstr FullNeg)
	:aspect Activity
	:modstr FullAff)
(s/ sentence
	:temporal ((PAST_REF :contained s1w)
		   (s1w :after s1a))
	:modal ((AUTH :FullAff s1w)
		(AUTH :FullAff s1p)
		(s1p :PrtAff purpose)
		(purpose :FullNeg s1a)))
```

The `:modstr` value represents any modals or
negation that are present within the purpose clause. That is, this value
doesn’t capture the fact that the purpose clause itself imparts a
non-full epistemic stance on its events; that is captured by the
`:purpose` relation.

[Back to Table of Contents](#toc)

##### Part 4-3-1-5. condition relation

The `:condition` relation in the sentence-level annotation indicates the relationship between events in conditional constructions. These events
also receive a `:modstr` annotation. As can
be seen in [\[4-3-1-5 (1)\]](#4-3-1-5 (1)), the event in the protasis is annotated with a `:condition` relation to the event in the
apodosis.

<span id="4-3-1-5 (1)" label="4-3-1-5 (1)">\[4-3-1-5 (1)\]</span>

<span id="4-3-1-5 (1a)" label="4-3-1-5 (1a)">\[4-3-1-5 (1a)\]</span> 
```
If she’s hungry, I’ll feed her dinner.
(f/ feed-01
	:ARG0 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:ARG1 (d/ dinner)
	:ARG2 (p2/ person
		:ref-person 3rd
		:ref-number Singular)
	:condition (h/ hunger-01
		:ARG0 p2
		:aspect State
		:modstr FullAff)
	:aspect Performance
	:modstr FullAff)
(s/ sentence
	:temporal ((DCT :overlap s1h)
		   (DCT :after s1f))
	:modal ((AUTH :NeutAff have-condition)
		(have-condition :FullAff s1h)
		(have-condition :FullAff s1f)))
```
<span id="4-3-1-5 (1b)" label="4-3-1-5 (1b)">\[4-3-1-5 (1b)\]</span> 
```
If she’s hungry, maybe I’ll cook pasta.
(c/ cook-01
	:ARG0 (p/ person
		:ref-person 1st
		:ref-number Singular)
	:ARG1 (p2/ pasta)
	:condition (h/ hunger-01
		:ARG0 (p3/ person
			:ref-person 3rd
			:ref-number Singular)
		:aspect State
		:modstr FullAff)
	:aspect Performance
	:modstr NeutAff)
(s/ sentence
	:temporal ((DCT :overlap s1h)
		   (DCT :after s1c))
	:modal ((AUTH :NeutAff have-condition)
		(have-condition :FullAff s1h)
		(have-condition :NeutAff s1c)))
```
<span id="4-3-1-5 (1c)" label="4-3-1-5 (1c)">\[4-3-1-5 (1c)\]</span> 
```
If she isn’t hungry, we’ll just watch a movie.
(w/ watch-01
	:ARG0 (p/ person
		:ref-person 1st
		:ref-number Plural)
	:ARG1 (m/ movie)
	:mod (j/ just)
	:condition (h/ hunger-01
		:ARG0 (p2/ person
			:ref-person 3rd
			:ref-number Singular)
		:aspect State
		:modstr FullNeg)
	:aspect Performance
	:modstr FullAff)
(s/ sentence
	:temporal ((DCT :overlap s1h)
		   (DCT :after s1w))
	:modal ((AUTH :NeutAff have-condition)
		(have-condition :FullNeg s1h)
		(have-condition :FullAff s1c))) 
```
As with purpose clauses, the `:modstr` value
doesn’t capture the uncertainty imparted by the conditional construction
itself; it corresponds to any negation or modals which are expressed
inside of the conditional construction. The modal value of the
conditional construction is captured by the
`:condition` value.

[Back to Table of Contents](#toc)

##### Part 4-3-1-6. Modal dependency structure

At Stage 0, there are some pieces of the modal dependency structure that
are unspecified. The modal strength that a modal verb imparts on its
complement is one of these pieces. As the modal annotation progresses,
this information is added to the frame files for modal verbs. For
example, the complements of English *want* have a
`:modstr NeutAff` value; this will be indicated
in the frame file as shown below.

```
Predicate: want.01 
	Roles:  
	Arg0: wanter  
	Arg1: thing wanted  
	Arg2: beneficiary  
	Arg3: in-exchange-for  
	Arg4: from 

:modstr of complement: NeutAff  
```

For the complements of modals, the `:modstr`
values work largely the same way that they do for other events; however,
they reflect the beliefs of the
`:experiencer` participant of the modal
event, who is often not the author. For example, in
[\[4-3-1-6 (1)\]](#4-3-1-6 (1)), Mary believes that the visit event may take
place in the future (`NeutAff` strength), but
the author disagrees.

<span id="4-3-1-6 (1)" label="4-3-1-6 (1)">\[4-3-1-6 (1)\]</span> Mary wants
to visit France next month, but I don’t think that’s possible.

The value associated with the modal event in its frame file corresponds
to Mary’s beliefs, as the `:experiencer` of
the wanting event.

Some predicates impart full, positive
(`FullAff`) strength on their complements,
often called factive predicates (e.g., *manage to*). Strong epistemic
modals (e.g., *expect that, deduce*) and strong deontic modals,
including intention modals (e.g., *plan to, decide to*) and obligation
modals (e.g., *need, demand*), impart `PrtAff`
strength on their complements. Weak deontic modals, including desire
(e.g., *want*) and permission (e.g., *allow*), impart
`NeutAff` strength on their complements.
Certain modals may also lexicalize negation, such as *doubt*, *forbid*,
or *wish*. These are annotated with the
`NeutNeg`,
`PrtNeg`, and
`FullNeg` values, respectively.

[Back to Table of Contents](#toc)

#### Part 4-3-2. English modals

This list gives the modal strength value associated with common English
modal constructions (this is certaintly not an exhaustive list). For
modal predicates that are identified as their own event (e.g.,
deontic predicates), the modal strength value characterizes the dependency link between the modal predicate node and its child event. For example, *want* is in the `NeutAff` list, which indicates that there
is a `NeutAff` link between the `want` node and its
complement event node in the full dependency structure.   

`FullAff` (full affirmative)

  - Simple assertions: declarative sentences

  - Certainty: *certainly, be sure, definitely, necessarily*

  - Predictive future: *will,* non-intentional *be going to*

  - Factual predicates: *manage to, finished*

`PrtAff` (partial affirmative)

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

`NeutAff` (neutral affirmative)

  - Weak epistemic modals: *may, might/might have, could have*

  - Weak epistemic adverbs/adjectives: *maybe, possibly/be possible
    that*

  - Conditionals (done automatically in the conversion from sentence-level to document-level structure)

  - Hope/Fear: *hope, fear, worry, dread*

  - Weak deontic modals
    
      - Desire: *want, prefer, would like to*
    
      - Permission: *let, permit, allow*

`NeutNeg` (neutral negative)

  - Doubt: *doubt, call into question, be dubious that, be skeptical
    that*

  - Combination of (some) <span>NeutAff</span> lexical items with negation

`PrtNeg` (partial negative)

  - Strong negative deontics: *forbid, ban, disallow*

  - Negative imperatives

  - Combination of (some) <span>PrtAff</span> lexical items with negation

`FullNeg` (full negative)

  - Negation: *not, never, no* + noun phrase

  - Negative complement taking predicates that entail that the event
    didn’t happen: *deny, prevent, prohibit, block, cease, it is
    impossible that, avoid*

  - Counterfactuals

  - Wishes: *wish*

[Back to Table of Contents](#toc)
  
 ## Part 5. Annotation Cheat Sheet
 
 * Sentence-level Annotation
 	* Choose the **top node** of the graph for the sentence you are annotating.
 		* If the sentence contains **one main event** (typically a lexical verb in a main clause), **annotate it** as the **top of the graph** (see [Part 3-1-1](#part-3-1-1-eventive-concepts) and [Part 3-1-3](#part-3-1-3-concept-word-mismatches) on how to decide what counts as one event).
 			* Highlight the word token that corresponds to the event. 
 			* If a citation form of it is in the lexicon already, click the "Lexicalized Concept" button and select this lemma.
 			* If it is not in the lexicon yet, click the "add to Lexicon" button and create a lexical entry for it first.
 		* If the sentence contains a **"non-verbal clause"** concept as its main event, choose the relevant **non-verbal clause predicate** as the top node (see [Part 3-1-1-3](#part-3-1-1-3-states-and-entities), [Part 3-1-3-5](#Part-3-1-3-5-Non-verbal-clauses)).
 		* If the sentence contains **multiple events** expressed in multiple clauses, decide what the top node is **based on the logical relation** between the events:
	 		* If one event is an argument of another event, choose the **main event** as the top node.
	 		* If one event is a **circumstantial participant** or **adverbial participant** in another event, choose the **main event** as the top node.
	 		* If two events are **coordinated** but a fine-grained meaning on the lowest level of the lattice in [Part 3-1-6](#part-3-1-6-discourse-relations) can be identified, choose the **main event** as the top node following the guidelines in the aforementioned section.
	 		* If two events are **coordinated** but a fine-grained meaning on the lowest level of the lattice in [Part 3-1-6](#part-3-1-6-discourse-relations) can not be identified, choose the **relevant coordinator concept** as the top node (see [Part 3-1-6](#part-3-1-6-discourse-relations)).
 			
 		
 	* Annotate the **participants** of the top node - these can be both entities and events.
 		* For each participant, select the correct **role/relation** from the "roles" drop-down menu:
 			* If the top node is an **abstract concept predicate**, use the appropriate **numbered argument roles** or **:opX** roles (see [Part 3-2-1-1-1](#part-3-2-1-1-1-nonverbal-clauses) for non-verbal clause predicates, [Part 3-1-6](#part-3-1-6-discourse-relations) for discourse relations).
 			* If the top node is a **sense-disambiguated lexicalized concept** with frame files, use the relevant **numbered argument roles** (see [Part 3-1-4](#part-3-1-4-word-senses)).
 			* If the top node is a **lexical event concept without frame files**, use the relevant **general participant roles** ([Part 3-2-1-1](#part-3-2-1-1-stage-0)).
 			* For **circumstantial participants** (e.g. temporal and spatial roles, conditions etc.), use the relevant **general participant roles** (see [Part 3-2-1-1](#part-3-2-1-1-stage-0)).
 		* Select the correct **concept** (see [Part 3-1-3](#part-3-1-3-concept-word-mismatches) for identification of participants expressed as part of the same word of the event):
 			* If the participant is overtly expressed as a **nominal**, add the **nominal word from the sentence** to the graph.
	 			* Highlight the word token in the sentence.
	 			* Click the "Lexicalized Concept" button, and then the word token in the drop-down menu.
 			* If the participant is overtly expressed as a **verb** (e.g. complement clause, adverbial), add the **verbal word from the sentence** to the graph.
	 			* Highlight the word token in the sentence.
	 			*  If a citation form of it is in the lexicon already, click the "Lexicalized Concept" button and select this lemma.
	 			* If it is not in the lexicon yet, click the "add to Lexicon" button and create a lexical entry for it first.
 			* If the participant is expressed **pronominally**, is **impersonal**, is a **proper noun**, or is **not expressed overtly**, add the correct **named entity concept label** (e.g. _person_, _thing_, _river_ etc.) to the graph ([Part 3-1-2](#part-3-1-2-named-entities)).
	 			* If the participant's name is overt in the sentence:
		 			* Choose the correct label from the "Named Entity Types" drop-down menu
		 			* Highlight the word tokens corresponding to it and add them using the "Lexicalized Concept" button.
	 			* If the participant's name is not overt in the sentence
		 			* Choose or type the correct label in the "Abstract Concept" drop-down menu and add it using the "Add Abstract Concept" button.
 			* If the participant **has been annotated in the graph for this sentence already** (e.g. reentrancy of a main clause participant in a complement clause), select the constant for this participant in the graph and add it using the "Lexicalized Concept" button.
 			* If the participant is expressed as a **participant nominalization**, choose either of the following options:
 				* Add the word **directly from the sentence** by highlighting it and using the "Lexicalized Concept" button.
 				* Add the correct **named entity concept label** to the graph through the "Named Entity Types" or "Abstract Concept" drop-down menu and modify it with an **inverse argument role** to the relevant event concept (see [Part 3-2-1-3](#part-3-2-1-3-inverse-participant-roles)).
 		* **Repeat** these steps for every node you have added that corresponds to an **event concept**.
 	* Annote the **modifiers** of each participant.
 		* If a participant is modified by a **property concept**, either:
	 		* Annotate it with an **:ARG1-of** relation to the **have-mod-91** predicate, and complete the argument structure of this predicate (see [Part 3-2-1-1-1](#part-3-2-1-1-1-nonverbal-clauses), [Part 3-2-1-3](#part-3-2-1-3-inverse-participant-roles)).
	 		* Select the **:mod** relation from the "roles" drop-down menu, highlight the modifier word token in the sentence, and add it to the graph using the "Lexicalized Concept" button.
 		* If a participant is modified by an **event concept** (e.g. a relative clause), annotate it with an **inverse numbered or general participant role** to this event concept, and complete the argument structure of this predicate (see [Part 3-2-1-3](#part-3-2-1-3-inverse-participant-roles)).
 		* If a participant is modified by an **object concept**:
 			* Annotate it with the **:mod** relation or one of its more fine-grained sub-relations if it is a **typifying modifier** (see [Part 3-2-2](#part-3-2-2-Non-participant-role-UMR-relations)).
 			* Annotate it with the **:poss**, **:part-of**, or **:ARG0-of (k/ kinship-91)** relations if it is an **anchoring modifier** (see [Part 3-2-2](#part-3-2-2-Non-participant-role-UMR-relations), [Part 3-2-1-3](#part-3-2-1-3-inverse-participant-roles)).
 		* If a participant is modified by a **quantifier**, annotate it with the **:quant** relation or otherwise follow the guidelines for quantification (see [Part 3-1-5](#part-3-1-5-scope-for-quantification-and-negation), [Part 3-2-2](#part-3-2-2-Non-participant-role-UMR-relations), [Part 3-3-4](#part-3-3-4-quant)).
 		* If a participant is a **named entity**, apply the **:name** and **:wiki** relations to the appropriate named entity category concept node, if you have not done so yet (see [Part 3-1-2](#part-3-1-2-named-entities)).
 	* Annotate **attributes** of participants and events.
 		* Give participants with **overt number marking** (e.g. number-marked NPs, verbal indexes with number information), a **:ref-number** attribute with the relevant value (see [Part 3-3-5](#part-3-3-5-ref)).
 		* Give **_person_ nodes** from pronouns, verbal indexation, or implicit participants - but not those corresponding to named entities - a _:ref-person_ attribute with the relevant value (see [Part 3-3-5](#part-3-3-5-ref)).
 		* Give concepts identified as **events** (see [Part 3-1-1](#part-3-1-1-eventive-concepts) for Event ID guidelines) an **:aspect** attribute with the relevant value (see [Part 3-3-1](#part-3-3-1-Aspect)).
 		* Give concepts identified as **events** (see [Part 3-1-1](#part-3-1-1-eventive-concepts) for Event ID guidelines) the relevant **modal attributes** ([Part 4-3](#part-4-3-modal-dependency)):
	 		* Give events **under the scope of a modal event** (e.g. a wanting-event) a **:modpred** relation with the space-building complement-taking predicate as the parent.
	 		* Give events **under the scope of a reporting event** a **:quot** relation with the reporting verb as the parent, and a **:modstr** relation with the relevant strenght.
	 		* Give **all other events** a **:modstr** annotation with the relevant strength.
 		* For **interrogative, imperative,** or **expressive** clauses, give the main verb a **:mode** attribute with the relevant value (see [Part 3-3-2](#part-3-3-2-mode)).
 		* Give constituents that are **morphosyntactically negated** or verbs in **polar questions** a **:polarity** attribute with the relevant value (see [Part 3-3-3](#part-3-3-3-polarity)).
 		* Give concepts that are modified with a **downtoner** or **intensifier** a **:degree** attribute with the relevant value ([Part 3-3-6](#part-3-3-6-degree)).
 
 * Document-level Annotation
 	* For any **event concept** or **object concept**:
 		* Assess whether it is **coreferential** with a previously mentioned event or object concept. In the case of object concepts, also assess whether it is a **subset** of another concept.
 		* If so, choose the relevant **coreference relation**, with the previous mention as the head and the current mention as the child (see [Part 4-1](#part-4-1-coreference)).
 	* Assess  the **modal dependency structure** generated on the basis of the sentence-level modal annotation.
	 	* Edit any errors.
	 	* If possible, substitute the relevant modal strength value for any **:Unsp** links generated between conceivers and events because of **:modpred** relations in the sentence-level annotation.
 	* Give every concept **identified as an event** (see [Part 3-1-1](#part-3-1-1-eventive-concepts) for Event ID guidelines) and each **time expression** in the text a temporal annotation (see [Part 4-2](#part-4-2-temporal-dependency)).

[Back to Table of Contents](#toc)

 ## Part 6. Integrated examples

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
    :temporal (b/before :op (n/now))
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
   :temporal (b/before :op (n/now))
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
       :temporal (b/before :op (n/now))
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
                   :temporal (b/before :op1 (n /now))
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
       :temporal (b /before :op (n /now))
       :aspect Endeavor)

```

[Back to Table of Contents](#toc)

##  Part 7: Alphabetical Index of UMR Annotation Categories

In the following alphabetical index, annotation values are distinguished by their italic typeface in the first column. In the last column, the principal section(s) in which each term is defined or discussed is indicated in boldface.

| Term           |              Category               |           Sections           |
| :-------: | :----------------------------------: | :------------------------------: |
| -00 suffix  | UMR annotation convention | 2-2-1, **3-1-4** |
| *1st person* | Person semantic category, person annotation value | 2-1, 3-1-3-1, **3-3-5** |
| *2nd person* | Person semantic category, person annotation value | 2-1, **3-3-5** |
| *3rd person* | Person semantic category, person annotation value | 2-1, 3-1-3-1, **3-3-5** |
| Ability | Modal semantic category | 3-3-1-2, **3-3-1-3** |
| Absolute time expression | Temporal semantic category | **4-2-1-2** |
| Abstract concept | Category of UMR objects | 1, 2-1, **2-2-3**, 2-2-4, 3-1-1-3, 3-1-3-5, 3-1-6 |
| Abstract Meaning Representation (AMR) | Annotation scheme | 1, **2-1**, 2-2, 2-2-1, 2-2-2, 2-2-3, 2-2-4, 2-2-5, 3-1-2, 3-2-1, 3-2-1-3, 3-2-2, 3-3-2, 3-3-3, 3-3-5, 3-3-6 |
| *Activity* | Aspectual semantic category, aspect annotation value | 2-1, 2-2-5, 3-3-1, **3-3-1-4**, 3-3-1-5 |
| *Actor* | Participant role | 2-1, 2-2-1, 3-1-3-1, **3-2-1-1**, 3-2-1-1-2, 3-3-5 |
| *Actor-of* | Participant role | **3-2-1-3** |
| (pure) Addition | Discourse relation | **3-1-6** |
| Additive | Discourse relation | **3-1-6** |
| Adjective | Part of Speech | 2-2-5, **3-3-1**, 3-3-3, 4-3-2 |
| Adverbial subordination | Strategy | **3-1-6** |
| Adversative | Discourse relation | **3-1-6** |
| *Aff* | Modal annotation value | 1, 4-2-2-1, **4-3-1-1**, 4-3-1-1-1, 4-3-1-1-2, 4-3-1-1-3, 4-3-1-3, 4-3-1-6, 4-3-2 |
| *Affectee* | Participant role | **3-2-1-1**, 3-2-1-1-2 |
| *After* | Temporal annotation value | 1, **4-2-2-1**, 4-2-2-3, 4-2-2-4 |
| *Age* | Non-participant role relation | **3-2-2-2** |
| Anaphoric expression | Coreference semantic category | 4-1, **4-1-1** |
| Anchoring modification | Modification semantic category | **3-2-2-2** |
| And + but | Discourse relation | **3-1-6** |
| And + contrast | Discourse relation | **3-1-6** |
| And + unexpected | Discourse relation | **3-1-6** |
| Anterior | Discourse relation | **3-1-6** |
| Anticausative | Valency-changing category | **3-2-1-1-2** |
| Antipassive | Valency-changing category | **3-2-1-1-2** |
| Applicative | Valency-changing category | 3-1-3-2, **3-2-1-1-2** |
| Apprehensional | Discourse relation | **3-1-6** |
| Arabic | Language | 2-2 |
| Arapaho | Language | 3-1-3-1 |
| *ARG0* | Participant role | 2-1, 2-2-1, 3-1-3-5, 3-2-1, 3-2-1-1-1, **3-2-1-2** |
| *ARG0-of* | Participant role | **3-2-1-3** |
| *ARG1* | Participant role | 2-1, 2-2-1, 3-1-3-5, 3-2-1, 3-2-1-1-1, **3-2-1-2**, 3-2-1-2, 4-3-1 |
| *ARG1-of* | Participant role | **3-2-1-3** |
| *ARG2* | Participant role | 2-2-1, 3-2-1, **3-2-1-2**, 4-3-1 |
| Argument | Semantic category | 1, 2-1, 2-2, **2-2-1**, 3-1-3, 3-1-3-1, 3-1-3-4, 3-1-3-5, 3-1-4, 3-2-1, 3-2-1-1, 3-2-1-1-1, 3-2-1-1-2, 3-2-1-2-1, 3-2-1-3, 3-3-5 |
| Argument structure | UMR annotation category | 1, 2-1, 2-2, 2-2-1, 2-2-2, 3-1-3-2, 3-1-3-4, 3-1-3-5, **3-2-1**, 3-2-1-3 |
| Aspect | Semantic category, UMR attribute | 1, 2-1, 2-2, 2-2-4, 2-2-5, **3-1-1**, 3-1-3-3, 3-2-1-3, 3-2-2-3, 3-3-1, 3-3-1-1, 3-3-1-2, 3-3-1-3, 3-3-1-4, 3-3-1-5, 4-2-1-2, 4-2-2-1 |
| Assertion | Modal semantic category | **4-3-2** |
| Associated motion | Semantic category | **3-1-3-4** |
| *Atelic Process* | Aspectual semantic category, aspect annotation value | 3-3-1, 3-3-1-3, **3-3-1-4** |
| Attribute | Category of UMR objects | 2-1, 2-2-4, **2-2-5**, 3-1-3-3, 3-1-6, 3-2-1-3, 3-2-2-3, **3-3**, 3-3-1, 3-3-2, 3-3-3, 3-3-4, 3-3-5, 3-3-6 |
| *Author/AUTH* | Modal annotation value | 1, **4-3-1-1**, 4-3-1-1-1, 4-3-1-1-2, 4-3-1-1-3, 4-3-1-3, 4-3-1-6 |
| Auxiliary | Strategy | **3-1-3-3** |
| Balinese | Language | 3-2-1 |
| Before | Temporal annotation value | 1, 4-2, **4-2-2-1** |
| Bezhta | Language | 3-2-1-1-2 |
| Bound morphology | Strategy | 3-1-3, 3-1-3-2, **3-1-3-3**, 3-2-1-2-1, 3-3-6 |
| *Calendar* | Temporal annotation relation | **3-2-2-1** |
| Cardinality | Quantification semantic category | 3-2-2-2, **3-2-2-5** |
| Causal relations | Semantic category | 3-1-1-3, **3-1-6**, 4-2-2-2, 4-2-2-3 |
| Causative | Valency-changing category | 3-1-3-2, **3-2-1-1-2** |
| *Cause* | Participant role | 3-1-3-2, 3-1-6, **3-2-1-1** |
| Caused event | Semantic category | **3-1-3-2**, 3-1-6, **4-2-2-3** |
| *Causer* | Participant role | **3-2-1-1**, 3-2-1-1-2 |
| Caused event | Semantic category | **3-1-3-2**, 3-1-6, **4-2-2-3** |
| *Century* | Temporal annotation relation | **3-2-2-1** |
| Certainty | Modal semantic category | 4-3, **4-3-1-1**, 4-3-1-1-1, 4-3-1-1-3, 4-3-1-3, 4-3-1-5, 4-3-2 |
| Change of state | Event type | **3-2-1-1**, 3-2-1-1-2 |
| Chinese | Language | 2-2, 3-1-4 |
| Circumstantial | Participant role category | **3-2-1-1** |
| Circumstantial locative | Participant role category | 3-1-3-4, **3-2-2-3** |
| Circumstantial temporal | Participant role category | **3-2-2-3** |
| Classifier | Strategy | **3-1-3-1** |
| Command | Mode semantic category | 3-2-2-6, **3-3-2**, 4-3-1-1-3 |
| *Companion* | Participant role | **3-2-1-1** |
| Completive | Aspectual semantic category | 3-1-3-3, **3-3-1-5** |
| Complex figure construal | Information packaging | **3-1-6** |
| Complex sentence | Sentence type | **3-1-6**, 4-3-1-4, 4-3-1-5 |
| Compound | Strategy | **3-1-1-2** |
| Conative | Modal semantic category | **3-1-3-3** |
| *Conceiver* | Modal annotation value | 4-2-2-1, 4-3, **4-3-1-1** |
| Concept | Category of UMR objects | 1, **2-1**, 2-2, 2-2-1, 2-2-2, 2-2-3, 2-2-4, 2-2-5, **3-1**, 3-1-1, 3-1-3, 3-1-3-1, 3-1-3-2, 3-1-3-3, 3-1-3-5, 3-1-3-6, 3-1-4, 3-1-5, 3-2-1-3, 3-2-2-4, 3-2-2-5, 3-2-2-6, 3-3-5, 3-3-6 |
| Concept-word mismatch | UMR annotation complication | **3-1-3** |
| *Concession* | Participant role | **3-1-6**, 3-2-2-6 |
| Concessive | Discourse relation | **3-1-6** |
| Concessive conditional | Discourse relation | **3-1-6** |
| Concrete time expression | Temporal semantic category | **4-2-1-2** |
| *Condition* | Participant role | 3-1-6, 3-2-2-6, 4-3-1, **4-3-1-5**, 4-3-2 |
| Conditional | Discourse relation | **3-1-6**, 4-3-1, 4-3-1-5 |
| Conjunctive | Discourse relation | **3-1-6** |
| *Consist-of* | Non-participant role relation | 2-2-4, **3-2-2-2** |
| Consecutive | Discourse relation | **3-1-6** |
| Constant | Category of UMR objects | **1** |
| Contact | Event type | **3-2-1-1** |
| *Contained* | Temporal annotation value | 1, **4-2-2-1**, 4-2-2-2 |
| Container adverbial | Aspectual semantic category | **3-3-1-5** |
| Continuative | Aspectual semantic category | 3-1-3-3, **3-3-1-4** |
| (pure) Contrast | Discourse relation | **3-1-6** |
| Coordination | Strategy | **3-1-6**, 3-2-2-4 |
| Coreference | Semantic category | 1, 2-1, 2-2, 3-1-1-4, 3-1-3-1, **4-1**, 4-1-1, 4-1-2 |
| Coreference, entities | Coreference semantic category | 3-1-3-1, **4-1-1** |
| Coreference, events | Coreference semantic category | 3-1-1-4, **4-1-2** |
| Counterfactual | Modal semantic category | **4-3-2** |
| *Country* | Named entity type | **3-1-2** |
| Creation | Event type | **3-2-1-1** |
| Cross-lingual annotation | UMR annotation practice | **1**, 2-2, 2-2-3, 2-2-4, 2-2-5, 3-1-1, 3-1-1-1, 3-1-1-2, 3-1-3, 3-1-3-2, 3-1-3-3, 3-1-3-5, 3-2-1-1, 3-3-5, 4-3-1-1-2 |
| *Day* | Temporal annotation relation | 2-2-4, **3-2-2-1** |
| *Dayperiod* | Temporal annotation relation | **3-2-2-1** |
| *Decade* | Temporal annotation relation | **3-2-2-1** |
| Degree | Semantic category, UMR attribute | 2-1, 2-2-5, **3-3-6** |
| Deontic | Modal semantic category | 4-2-2-4, 4-3, 4-3-1-1, **4-3-1-1-3**, 4-3-1-6, 4-3-2 |
| Desiderative | Modal semantic category | 3-1-3-3, 4-2-2-4, **4-3-1-1-3**, 4-3-1-2, 4-3-1-6, 4-3-2 |
| Direct evidence | Evidential semantic category | 4-3-1-1, **4-3-1-1-2** |
| *Directed achievement* | Aspectual semantic category, aspect annotation value | 3-3-1, **3-3-1-5** |
| *Directed activity* | Aspectual semantic category, aspect annotation value | 3-3-1, **3-3-1-4**, 3-3-1-5 |
| *Directed endeavor* | Aspectual semantic category, aspect annotation value | 3-3-1, **3-3-1-5** |
| *Direction* | Non-participant role relation | **3-2-2-3** |
| Discourse relations | Semantic category | **3-1-6** |
| Disjunctive | Discourse relation | **3-1-6** |
| Document Creation Time (DCT) | Temporal annotation value | 1, 3-3-1-4, 4-2, **4-2-1-1**, 4-2-1-2 |
| Document-level representation | UMR annotation practice | 1, 2-1, 2-2, 2-2-5, 3-1-6, 3-3-3, **4**, 4-1-1, 4-2, 4-3-1, 4-3-1-4 |
| Doubt | Modal semantic category | **4-3-1-6**, 4-3-2 |
| *Downtoner* | Degree semantic category, degree annotation value | 2-1, **3-3-6** |
| *Dual* | Number semantic category, number annotation value | 2-1, **3-3-5** |
| *Duration* | Non-participant role relation | 2-2-4, **3-2-2-3** |
| Durative adverbial | Aspectual semantic category | **3-3-1-5** |
| Edge | Category of UMR objects | **2-1**, 2-2, 2-2-1, 4-3 |
| Embedded interrogative | Semantic category | **3-2-1-3** |
| *Endeavor* | Aspectual semantic category, aspect annotation value | 2-1, 2-2-5, 3-3-1, **3-3-1-5** |
| English | Language | 1, 2-2, 2-2-1, 2-2-5, 3-1-3, 3-1-3-1, 3-1-3-2, 3-1-3-3, 3-1-3-4, 3-1-3-5, 3-1-4, 3-1-6, 3-2-1, 3-2-1-1-1, 3-2-1-1-2, 3-3-1, 3-3-1-1, 3-3-1-2, 3-3-1-3, 3-3-1-5, 3-3-3, 3-3-5, 3-3-6, 4-3-1-6, 4-3-2 |
| Epistemic modality | Modal semantic category | 3-1-6, 4-3, 4-3-1, **4-3-1-1**, 4-3-1-1-2, 4-3-1-4, 4-3-1-6, 4-3-2 |
| *Equal* | Degree semantic category, degree annotation value | **3-3-6** |
| Equational | Non-verbal clause category | **3-1-1-3**, 3-1-3-5, 3-2-1-1-1 |
| *Era* | Temporal annotation relation | **3-2-2-1** |
| Event | Semantic category | 1, 2-1, 2-2-1, **3-1-1**, 3-1-1-1, 3-1-1-2, 3-1-1-3, 3-1-1-4, 3-1-3-1, 3-1-3-2, 3-1-3-3, 3-1-3-4, 3-1-6, 3-2-1, 3-2-1-1, 3-2-1-1-2, 3-2-1-2, 3-2-1-3, 3-2-2-3, 3-3-1, 3-3-1-1, 3-3-1-2, 3-3-1-3, 3-3-1-4, 3-3-1-5, 4-1-2, 4-2, 4-2-1-1, 4-2-1-2, 4-2-1-3, 4-2-2-1, 4-2-2-2, 4-2-2-3, 4-2-2-4, 4-3, 4-3-1, 4-3-1-1, 4-3-1-1-1, 4-3-1-1-2, 4-3-1-1-3, 4-3-1-2, 4-3-1-3, 4-3-1-4, 4-3-1-5, 4-3-1-6, 4-3-2 |
| Event identification | UMR annotation practice | 2-2-1, **3-1-1**, 3-1-1-1, 3-1-1-2, 3-1-1-3, 3-1-1-4, 3-1-3-2, 3-1-3-3, 3-1-3-4, 3-1-3-5, 3-2-1-2, 3-3-1, 3-3-1-1, 3-3-1-3, 4-2-2-1, 4-2-2-3, 4-3-1, 4-3-1-1-3, 4-3-1-2, 4-3-2 |
| Event nominal | Strategy | **3-1-1**, 3-1-1-2, **3-3-1-1** |
| Eventive modifier | Modification semantic category | 2-2-1, **3-1-1-2**, 3-2-1-3 |
| Evidentiality | Semantic category | 4-3, 4-3-1-1, **4-3-1-1-2** |
| *Example* | Non-participant role relation | **3-2-2-6** |
| *Exclusive* | Person semantic category, person annotation value | **3-3-5** |
| Exclusive disjunctive | Discourse relation | **3-1-6** |
| Exhaustive disjunction | Discourse relation | **3-1-6** |
| *Experiencer* | Participant role | 2-1, **3-2-1-1**, 4-3-1-6 |
| Experiential | Event type | **3-2-1-1** |
| *Expressive* | Mode annotation value | 2-1, **3-3-2** |
| External cause | Participant role category | **3-2-1-1** |
| FactBank | Annotation scheme | **4-3-1-1** |
| Factive predicate | Event type | **4-3-1-6**, 4-3-2 |
| Falam Chin | Language | 3-2-1-1-2 |
| Fear | Modal semantic category | **4-3-2** |
| Figure-ground construal | Information packaging | **3-1-6** |
| *Force* | Participant role | **3-2-1-1** |
| Frame files | Annotation scheme | **3-1-4**, 3-2-1, 3-2-1-1-1, **3-2-1-2**, 3-2-1-2-1, 3-2-1-3, 4-3, 4-3-1-6 |
| *Frequency* | Non-participant role relation | 2-2-4, **3-2-2-3** |
| Frustrative | Modal semantic category | **3-1-3-3** |
| Full support | Modal semantic category | **4-3-1-1***, 4-3-1-1-2, 4-3-1-1-3, 4-3-1-6, 4-3-2 |
| Future-oriented modality | Modal semantic category | 4-3-1-1, **4-3-1-1-3** |
| *Future_ref* | Temporal annotation value | **4-2-1-1**, 4-2-1-2 |
| General participant roles | Participant role category | 2-1, 2-2-1, 3-2-1, **3-2-1-1**, 3-2-1-1-2, 3-2-1-2-1, 3-2-1-3, 3-2-2 |
| Generic events | Event type | **3-1-1-4** |
| Gerund | Strategy | **3-1-1**, 3-3-1-1 |
| *Goal* | Participant role | 3-1-3-4, **3-2-1-1** |
| *Greater plural* | Number semantic category, Number annotation value | **3-3-5** |
| *Habitual* | Aspectual semantic category, aspect annotation value | 2-1, 2-2-5, 3-3-1, **3-3-1-2** |
| Hope | Modal semantic category | **4-3-2** |
| Hua | Language | 3-1-6 |
| Identity | Coreference semantic category | **4-1-1, 4-1-2** |
| *Imperative* | Mode annotation value | 2-1, 3-1-6, 3-2-2-6, **3-3-2**, 4-3-2 |
| *Imperfective* | Aspectual semantic category, aspect annotation value | 3-3-1, **3-3-1-3** |
| Implicit event | Event type | **3-1-1-4**, 3-1-3-5 |
| Implicit participant | Participant type | 2-1, 3-2-1-1, 3-2-1-1-2, **3-2-1-2**, 3-3-5 |
| Inactive action | Event type | **3-3-1-3** |
| Inceptive | Aspectual semantic category | **3-3-1-4** |
| Inchoative | Aspectual semantic category | **3-1-3-3** |
| *Inclusive* | Person semantic category, person annotation value | **3-3-5** |
| Inclusive disjunctive | Discourse relation | **3-1-6** |
| *Incremental accomplishment* | Aspectual semantic category, aspect annotation value | 3-3-1, **3-3-1-5** |
| Independent argument structure | UMR annotation diagnostic | **3-1-3-4** |
| Indirect evidence | Evidential semantic category | **4-3-1-1-2** |
| Inferred evidence | Evidential semantic category | **4-3-1-1** |
| *Inherent state* | Aspectual semantic category, aspect annotation value | 3-3-1, **3-3-1-3** |
| *Instrument* | Participant role | 3-1-3-1, **3-2-1-1** |
| *Intensifier* | Degree semantic category, degree annotation value | 2-1, **3-3-6** |
| Intention | Modal semantic category | **4-3-1-1-3** |
| *Interrogative* | Mode annotation value | 2-1, **3-3-2** |
| Inverse participant roles | Participant role category | **3-2-1-3** |
| *Irreversible directed achievement* | Aspectual semantic category, aspect annotation value | 3-3-1, **3-3-1-5** |
| *Irreversible state* | Aspectual semantic category, aspect annotation value | 3-3-1, **3-3-1-3** |
| Juxtaposition | Strategy | **3-1-3-5** |
| *Key event* | Temporal annotation value | **4-2-1-3**, 4-2-2-1 |
| Kinship relations | Semantic category | **3-2-1-3**, 3-2-2-2 |
| Kukama | Language | 3-1-3-2, 3-1-3-5, 3-2-1-1-1, 3-2-1-1-2 |
| Lattice | Category of UMR objects | 2-2-4, 3-1-6, 3-3-1, 3-3-1-1, 3-3-5, 4-3, 4-3-1-1 |
| Lemma | Category of UMR objects | 2-1, 3-1-3-6, **3-1-4** |
| Lexicon | Category of UMR objects | 2-1, 2-2-1, **3-1-4**, 3-2-1, 3-2-1-1-1, 3-2-1-2, 3-2-1-2-1, 3-2-1-3, 3-3-6 |
| Locatable time expression | Temporal semantic category | **4-2-1-2** |
| Manipuri | Language | 3-1-3-3 |
| *Manner* | Participant role | 3-1-6, **3-2-1-1** |
| *Material* | Participant role | **3-2-1-1** |
| Means | Discourse relation | **3-1-6** |
| *Medium* | Non-participant role relation | 2-2-4, **3-2-2-2** |
| Mensural constructions | Quantification semantic category | 2-2, **3-2-2-5** |
| Metanodes | Temporal annotation category | 4-2, 4-2-1, **4-2-1-1**, 4-2-2-1 |
| *Mod* | Non-participant role relation | 2-2-4, **3-2-2-2** |
| *Mod* | Modal annotation value | 4-3-1, **4-3-1-2** |
| Modal dependencies | Category of UMR objects | 1, 2-1, 3-1-3-3, 3-3-3, 4-2-2-1, **4-3**, 4-3-1, 4-3-1-6, 4-3-2 |
| Modal strength | Modal semantic category | 4-3, 4-3-1, **4-3-1-1**, 4-3-1-1-1, 4-3-1-1-2, 4-3-1-1-3, 4-3-1-3, 4-3-1-6, 4-3-2 |
| Modal verbs/auxiliaries | Strategy | **3-1-3-3**, 3-3-1-3, 4-3-1, 4-3-1-1-3, 4-3-1-2, 4-3-1-3, 4-3-1-4, 4-3-1-5, **4-3-1-6**, 4-3-2 |
| Modality | Semantic category | 1, 2-1, 2-2, 2-2-5, 3-1-1, 3-1-3-3, 3-3-1, 3-3-1-2, 3-3-1-3, 3-3-3, 4-2-2-1, 4-2-2-4, **4-3**, 4-3-1, 4-3-1-1, 4-3-1-1-1, 4-3-1-1-2, 4-3-1-1-3, 4-3-1-2, 4-3-1-3, 4-3-1-4, 4-3-1-5, 4-3-1-6, 4-3-2 |
| Mode | UMR attribute | 2-1, 2-2-5, **3-3-2** |
| Modification | Information packaging | 2-2, 2-2-1, 2-2-4, 2-2-5, **3-1-1**, 3-1-1-2, 3-1-1-3, 3-2-1-3, 3-2-2, 3-2-2-2, 3-2-2-3, 4-2 |
| *Modstr* | Modal annotation value | 4-2-2-1, 4-3, 4-3-1, **4-3-1-1**, 4-3-1-1-1, 4-3-1-1-2, 4-3-1-1-3, 4-3-1-2, 4-3-1-3, 4-3-1-4, 4-3-1-5, 4-3-1-6 |
| *Month* | Temporal annotation relation | 2-2-4, **3-2-2-1** |
| Motion | Event type | 3-1-1-4, **3-1-3-4, 3-2-1-1** |
| Multi-word expression | UMR annotation complication | 1, 2-1, 2-2-2, 3-1-3, **3-1-3-6** |
| *Name* | Non-participant role relation | 2-1, **3-2-2-4** |
| Named entity | Category of UMR objects | 1, 2-1, **3-1-2**, 3-1-3-1, 3-2-2-4, 3-3-5, 4-1 |
| *Neg* | Modal annotation value | **4-3-1-1**, 4-3-1-1-1, 4-3-1-1-3, 4-3-1-6, 4-3-2 |
| Negation | Modal semantic category | 2-1, 2-2, 3-1-3-2, 3-1-5, 3-1-6, **3-3-3, 4-3-1-1**, 4-3-1-1-1, 4-3-1-4, 4-3-1-5, 4-3-1-6, 4-3-2 |
| Negative circumstantial | Discourse relation | **3-1-6** |
| *Neut* | Modal annotation value | 1, **4-3-1-1**, 4-3-1-1-1, 4-3-1-1-3, 4-3-1-3, 4-3-1-6, 4-3-2 |
| *NeutNeg* | Modal annotation value | **4-3-1-1**, 4-3-1-1-1, 4-3-1-1-3, 4-3-1-6, 4-3-2 |
| Neutral support | Modal semantic category | 1, **4-3-1-1**, 4-3-1-1-3, 4-3-2 |
| Node | Category of UMR objects | 2-1, **2-2**, 2-2-1, 2-2-3, 2-2-5, 3-2-1-3, 3-2-2-4, 3-2-2-6, 3-3-5, 4-1-1, 4-1-2, 4-2, 4-2-1, 4-2-1-1, 4-2-1-2, 4-2-2-1, 4-3, 4-3-1, 4-3-2 |
| Nominal modification | Modification semantic category | 3-1-1, **3-2-1-3**, **3-2-2-2** |
| *Non-1st person* | Person semantic category, person annotation value | **3-3-5** |
| *Non-3rd person* | Person semantic category, person annotation value | **3-3-5** |
| Non-exhaustive disjunction | Discourse relation | **3-1-6** |
| Non-finite complement | Strategy | **3-1-1-2** |
| *Non-full* | Modal semantic category, modal annotation value | **4-3-1-1**, 4-3-1-4 |
| *Non-incremental accomplishment* | Aspectual semantic category, aspect annotation value | 3-3-1, **3-3-1-5** |
| *Non-neutral* | Modal semantic category, modal annotation value | **4-3-1-1** |
| Non-participant role relation | Category of UMR relations | 2-2-4, **3-2-2** |
| Non-result path expression | UMR annotation diagnostic | **3-3-1-5** |
| *Non-singular* | Number semantic category, Number annotation value | **3-3-5** |
| Non-verbal clauses | Semantic category | 2-2-1, 2-2-3, 3-1-1-3, **3-1-3-5**, 3-2-1-1-1, 3-2-1-2, 3-2-1-3, 3-3-1-3 |
| Noun | Part of Speech | 2-2, 2-2-1, **3-3-1**, 3-1-3-1, 3-2-1-3, 3-2-2-2 |
| Noun incorporation | Strategy | **3-1-3-1** |
| NP | Strategy | 3-1-3-1, 3-1-3-4, 3-1-3-5, 3-2-1-3, 3-2-2, **3-2-2-2** |
| Number | Semantic category | 2-1, 2-2-5, 3-1-3-1, **3-3-5** |
| Numbered/lexicalized participant roles | Participant role category | 2-1, 2-2-1, 3-1-3-5, 3-2-1, 3-2-1-1-1, **3-2-1-2**, 3-2-1-2-1, 3-2-1-3, 3-2-2 |
| Object concept | Semantic category | **3-1-1**, 3-1-1-2, 3-1-1-3, 3-1-3-5, 3-2-1, 3-2-1-1, 3-2-1-1-1, 3-2-1-3, 3-2-2-2, 3-2-2-3, 3-2-2-5, 3-2-2-6, 3-3-2, 3-3-5, 4-1-1 |
| Obligation | Modal semantic category | 2-1, **4-3-1-6**, 4-3-2 |
| Optative | Modal semantic category | **3-1-3-3** |
| *OpX* | Non-participant role relation | **3-2-2-4**, 4-2 |
| *Ord* | Non-participant role relation | **3-2-2-5** |
| Ordinal | Quantification semantic category | **3-2-2-5** |
| *Other* | Non-participant role relation | 2-2-4, 3-2-1-1, **3-2-2-6** |
| *Overlap* | Temporal annotation value | 1, **4-2-2-1**, 4-2-2-2 |
| Partial support | Modal semantic category | **4-3-1-1**, 4-3-1-1-1, 4-3-1-1-2, 4-3-1-1-3, 4-3-2 |
| Participant identification | UMR annotation practice | 2-2-1, **3-1-3-1**, 3-1-3-5, 3-2-1, 3-2-1-1, 3-2-1-1-1, 3-2-1-1-2, 3-2-1-2 |
| Participant nominalization | Strategy | **3-2-1-3** |
| Participant roles | Semantic category | 2-1, 2-2-1, 3-1-1, 3-1-3-1, 3-1-3-2, 3-1-6, **3-2-1**, 3-2-1-1, 3-2-1-1-1, 3-2-1-1-2, 3-2-1-2, 3-2-1-2-1, 3-2-1-3, 4-3, 4-3-1, 4-3-1-4 |
| Participle | Strategy | **3-1-1**, 3-1-1-2, 3-2-1-3 |
| *Part-of* | Non-participant role relation | **3-2-2-2** |
| Part-whole relations | Semantic category | **3-2-2-2** |
| Passive | Valency-changing category | 3-2-1, **3-2-1-1-2** |
| *PAST_REF* | Temporal annotation value | **4-2-1-1**, 4-2-1-2 |
| *Path* | Non-participant role relation | **3-2-2-3** |
| *Paucal* | Number semantic category, Number annotation value | 2-1, **3-3-5** |
| *Perfective* | Aspectual semantic category, aspect annotation value | 3-3-1, **3-3-1-5** |
| *Performance* | Aspectual semantic category, aspect annotation value | 2-1, 2-2-5, 3-3-1, **3-3-1-5** |
| Permissive | Modal semantic category | 4-3, **4-3-1-1-3**, 4-3-1-6, 4-3-2 |
| *Person* | Named entity type | 1, 2-1, **3-1-2**, 3-1-3-1, 3-2-1-3, 3-3-5, 4-1-1 |
| Person | Semantic category | 2-1, 2-2-5, 3-1-3-1, **3-3-5** |
| Phasal aspect | Aspectual semantic category | **3-1-3-3** |
| *Place* | Participant role | **3-2-1-1** |
| *Plural* | Number semantic category, Number annotation value | 2-1, 3-2-1-1, **3-3-5** |
| *Point state* | Aspectual semantic category, aspect annotation value | 3-3-1, **3-3-1-3**, 3-3-1-5 |
| Polarity | Modal semantic category | 2-1, 2-2-5, 3-1-6, **3-3-3**, 4-3, 4-3-1, **4-3-1-1**, 4-3-1-1-1 |
| *Polite* | Non-participant role relation | **3-2-2-6** |
| Positive circumstantial | Discourse relation | **3-1-6** |
| *Poss* | Non-participant role relation | **3-2-2-2** |
| Possession | Semantic category | 2-2-3, **3-1-1-3**, 3-1-3-5, 3-2-1-1, 3-2-1-1-1, 3-2-1-1-2, **3-2-2-2** |
| Possibility | Modal semantic category | 2-1, **4-3-1-1** |
| Posterior | Discourse relation | **3-1-6** |
| Pragmatic valency alternation | Valency-changing category | 3-2-1, **3-2-1-1-2** |
| Predicate | Category of UMR objects | 1, 2-1, 2-2, **2-2-1**, 2-2-3, 2-2-5, 3-3-1, 3-1-1-1, 3-1-1-3, 3-1-3, 3-1-3-1, 3-1-3-2, 3-1-3-3, 3-1-3-4, 3-1-3-5, 3-1-4, 3-1-5, 3-2-1, 3-2-1-1, 3-2-1-1-1, 3-2-1-2, 3-2-1-2-1, 3-2-1-3, 3-2-2, 3-3-1-3, 4-2, 4-2-2-3, 4-3-1-3, 4-3-1-6, 4-3-2 |
| Predicate-argument structure | Semantic category | 1, 2-1, 2-2, **2-2-1**, 3-1-3, 3-1-3-1, 3-1-3-5, **3-2-1**, 3-2-1-1, 3-2-1-1-1, 3-2-1-2, 3-2-1-2-1, 3-2-1-3 |
| Predication | Information packaging | 2-2, **3-1-1**, 3-1-1-1, 3-1-1-3, 3-1-3-5, 3-2-1-1-1, 3-1-3-3, 4-2-2-3 |
| Predicative location | Non-verbal clause category | **3-1-1-3**, 3-1-3-5, 3-2-1-1-1 |
| Predicative possession | Non-verbal clause category | **3-1-1-3**, 3-1-3-5, 3-2-1-1-1 |
| Predicativization/predicativized argument | Strategy | **3-1-3-5**, 3-2-1-1-1 |
| *Present_ref* | Temporal annotation value | **4-2-1-1**, 4-2-1-2 |
| *Process* | Aspectual semantic category, aspect annotation value | 2-1, 3-3-1, 3-3-1-1 |
| Pronominal affixes | Strategy | **3-1-3-1**, 3-1-3-5, **3-3-5** |
| Pronoun | Part of Speech | 2-1, **3-1-3-1, 4-1**, 4-1-1 |
| PropBank | Annotation scheme | **2-2-1**, 3-2-1, 3-2-1-2, 3-2-1-3 |
| Property concept | Semantic category | **3-1-1**, 3-1-1-3, 3-1-3-5, 3-1-6, 3-2-1-1-1, 3-3-1-3, 3-3-2, 3-3-6 |
| Property predication | Non-verbal clause category | **3-1-1-3**, 3-1-3-5, 3-2-1-1-1 |
| *Prt* | Modal annotation value | **4-3-1-1**, 4-3-1-1-1, 4-3-1-1-2, 4-3-1-1-3, 4-3-1-6, 4-3-2 |
| *PrtNeg* | Modal annotation value | **4-3-1-1**, 4-3-1-1-1, 4-3-1-1-3, 4-3-1-6, 4-3-2 |
| Purpose | Discourse relation | **3-1-6**, 4-2-2-4, 4-3-1, 4-3-1-4, 4-3-2 |
| *Purpose* | Participant role | 3-1-6, **3-2-1-1**, 4-3-1, **4-3-1-4** |
| *Quant* | Quantification annotation value | 2-1, 2-2-5, **3-2-2-5, 3-3-4** |
| Quantification | Semantic category | 1, 2-1, 2-2, 2-2-5, **3-1-5**, 3-2-2-2, **3-2-2-5**, 3-3-1-3, **3-3-4**, 4-2-1-2 |
| *Quarter* | Temporal annotation relation | **3-2-2-1** |
| *Quot* | Modal annotation value | 4-3, 4-3-1, **4-3-1-3** |
| *Range* | Non-participant role relation | 2-1, **3-2-2-5** |
| *Recipient* | Participant role | **3-2-1-1**, 3-2-1-1-2 |
| Reciprocal | Valency-changing category | 3-2-1, **3-2-1-1-2** |
| Ref-number | UMR attribute | 2-1, 2-2-5, **3-3-5** |
| Ref-person | UMR attribute | 2-1, 2-2-5, **3-3-5** |
| Reference | Information packaging | 2-2, 2-2-1, 2-2-4, 2-2-5, **3-1-1**, 3-1-1-2, 3-1-1-3, 3-2-1-3, 3-2-2, 3-2-2-2, 3-2-2-3, 4-2 |
| Reference time | Temporal annotation value | 1, 3-1-1-2, **4-2-1-2** |
| Referring expression | Information packaging | 2-2, 2-2-4, 3-2-1-3, 3-2-2-2, 3-3-1-1 |
| Reflexive | Valency-changing category | 3-1-3-2, **3-2-1-1-2** |
| Relation | Category of UMR objects | 1, 2-1, **2-2**, 2-2-1, 2-2-4, 2-2-5, 3-1-3-3, 3-1-6, **3-2**, 3-2-1-1, 3-2-1-3, 3-2-2, 3-2-2-1, 3-2-2-2, 3-2-2-3, 3-2-2-4, 3-2-2-5, 3-2-2-6, 4-1-1, 4-1-2, 4-2, 4-2-1, 4-2-1-1, 4-2-2-1, 4-2-2-2, 4-2-2-3, 4-2-2-4, 4-3-1, 4-3-1-1-2, 4-3-1-2, 4-3-1-3, 4-3-1-4, 4-3-1-5 |
| Relative clause | Strategy | 3-1-1, 3-1-1-2, **3-2-1-3** |
| Relative time expression | Temporal semantic category | 4-2, **4-2-1-2** |
| Reported event | Event type | 4-2-2-1, 4-3, 4-3-1, 4-3-1-1, **4-3-1-3** |
| Reported evidence | Evidential semantic category | **4-3-1-1** |
| Reported event | Event type | 4-2-2-1, 4-3-1, **4-3-1-3** |
| *Reversible directed achievement* | Aspectual semantic category, aspect annotation value | 3-3-1, **3-3-1-5** |
| *Reversible state* | Aspectual semantic category, aspect annotation value | 3-3-1, **3-3-1-3** |
| Road map | UMR annotation practice | 3-2-1, 3-2-1-1-1, 3-2-1-1-2, 3-2-1-3, 4-3 |
| *ROOT* | Temporal, modal annotation value | **4-2-1**, 4-2-1-2 |
| *Same-entity* | Coreference annotation value | **4-1-1** |
| *Same-event* | Coreference annotation value | **4-1-2** |
| Sanapaná | Language | 2-2-1, 2-2-2, 2-2-3, 3-1-3-2, 3-1-3-4, 3-3-5, 3-3-6 |
| *Scale* | Non-participant role relation | **3-2-2-5** |
| Scope | Semantic category | 2-1, 2-2-5, 3-1-3-2, **3-1-5**, 3-3-1-3, 4-3-1, 4-3-1-1-3, 4-3-1-2, 4-3-1-3 |
| *Season* | Temporal annotation relation | **3-2-2-1** |
| Second-hand evidence | Evidential semantic category | **4-3-1-1** |
| Semantic type | Semantic category | **3-1-1**, 3-1-1-2, 3-1-1-3 |
| Semantic valency alternation | Valency-changing category | 3-2-1, **3-2-1-1-2** |
| *Semelfactive* | Aspectual semantic category, aspect annotation value | 3-3-1, **3-3-1-5** |
| Semi-modals | Modal semantic category | **3-1-3-3** |
| Sense disambiguation | UMR annotation practice | 2-1, 2-2-1, **3-1-4** |
| Sentence-level representation | UMR annotation practice | 1, 2-1, 2-2, 2-2-5, **3**, 3-1-6, 3-3-3, 4-2, 4-3-1, 4-3-1-4, 4-3-1-5 |
| Serial verb construction | Strategy | **2-2** |
| Shipibo-konibo | Language | **3-2-1-1-2** |
| Simultaneous | Discourse relation | **3-1-6** |
| *Singular* | Number semantic category, Number annotation value | 2-1, **3-3-5** |
| *Source* | Participant role | **3-2-1-1** |
| Stage 0 annotation | UMR annotation practice | 3-2-1, 3-2-1-1, 3-2-1-1-1, 3-2-1-1-2, 3-2-1-2, 3-2-1-3, 4-3, 4-3-1, 4-3-1-2, 4-3-1-6 |
| Stage 1 annotation | UMR annotation practice | 3-2-1, 3-2-1-1-1, 3-2-1-2, 3-2-1-2-1, 4-3 |
| *Start* | Participant role | **3-2-1-1** |
| *State* | Aspectual semantic category, aspect annotation value | 2-1, 2-2-1, 2-2-5, 3-1-1, 3-1-1-3, 3-3-1, 3-3-1-1, **3-3-1-3**, 3-3-1-5, 4-2-2-1 |
| *Stimulus* | Participant role | **3-2-1-1** |
| *Stimulus-of* | Participant role | **3-2-1-3** |
| Subevent | Coreference, temporal semantic category | 4-1-2, 4-2-2-1, **4-2-2-2** |
| *Subset-of* | Coreference annotation value | **4-1-1, 4-1-2** |
| Substitution | Discourse relation | **3-1-6** |
| *Temp* | Temporal annotation value | 4-2-1, **4-2-1-1** |
| *Temporal* | Participant role | 2-1, **3-1-6, 3-2-1-1**, 4-2 |
| Temporal dependencies | Category of UMR objects | 1, 2-1, 3-1-3-3, **4-2**, 4-2-1, 4-2-1-1, 4-2-1-2, 4-2-2-1 |
| Temporal superstructure | UMR annotation procedure | 4-2, **4-2-1**, 4-2-1-1, 4-2-1-2, 4-2-1-3, 4-2-2-1 |
| Terminative | Aspectual semantic category | **3-3-1-5** |
| *Theme* | Participant role | 2-2-1, 3-1-3-1, **3-2-1-1**, 3-2-1-1-2 |
| Thetic location | Non-verbal clause category | **3-1-1-3**, 3-1-3-5, 3-2-1-1-1 |
| Thetic possession | Non-verbal clause category | 2-2-3, **3-1-1-3**, 3-1-3-5, 3-2-1-1-1 |
| *Thing* | Named entity type | **3-1-3-1, 3-3-5** |
| Time expression | Temporal semantic category | 4-2, 4-2-1, 4-2-1-1, **4-2-1-2**, 4-2-1-3, 4-2-2-1 |
| TimeML | Annotation scheme | **3-1-1** |
| *Timezone* | Temporal annotation relation | **3-2-2-1** |
| *Topic* | Non-participant role relation | 2-2-4, **3-2-2-2** |
| Torau | Language | 3-2-1 |
| Transfer | Event type | **3-2-1-1, 3-2-1-1-2** |
| *Trial* | Number semantic category, Number annotation value | **3-3-5** |
| Typifying modifier | Modification semantic category, Number annotation value | 2-2-4, **3-2-2-2** |
| *Undergoer* | Participant role | 2-2-1, 3-1-3-1, **3-2-1-1**, 3-2-1-1-2, 3-3-5 |
| *Undergoer-of* | Participant role | **3-2-1-3** |
| *Undirected activity* | Aspectual semantic category, aspect annotation value | 3-3-1, **3-3-1-4**, 3-3-1-5 |
| *Undirected endeavor* | Aspectual semantic category, aspect annotation value | 3-3-1, **3-3-1-5** |
| Unexpected co-occurrence | Discourse relation | **3-1-6** |
| Uniform Meaning Representation (UMR) | Annotation scheme | **1**, 2-1, 2-2, 2-2-1, 2-2-2, 2-2-3, 2-2-4, 2-2-5, 3-1-1, 3-1-1-1, 3-1-1-3, 3-1-1-4, 3-1-3, 3-1-3-1, 3-1-3-2, 3-1-3-3, 3-1-3-4, 3-1-3-5, 3-1-4, 3-1-5, 3-1-6, 3-2-1, 3-2-1-1, 3-2-1-1-1, 3-2-1-3, 3-2-2, 3-2-2-2, 3-2-2-6, 3-3, 3-3-1-3, 3-3-2, 3-3-3, 3-3-5, 3-3-6, 4-1, 4-1-1, 4-1-2, 4-2, 4-3, 4-3-1-1 |
| *Unit* | Non-participant role relation | **3-2-2-5** |
| Unity under modalization | UMR annotation diagnostic | **3-1-3-3** |
| Unity under negation | UMR annotation diagnostic | **3-1-3-2** |
| Unlocatable time expression | Temporal semantic category | **4-2-1-2** |
| Vague time expression | Temporal semantic category | **4-2-1-2** |
| Valency-changing operation | Semantic category | **3-1-3-2**, 3-2-1, **3-2-1-1-2**, 3-2-1-2-1 |
| Valency-increasing applicative | Valency-changing category | **3-2-1-1-2** |
| Valency-rearranging applicative | Valency-changing category | **3-2-1-1-2** |
| *Value* | Non-participant role relation | 2-1, 2-2-5, **3-2-2-5** |
| Venitive | Associated motion semantic category | **3-1-3-4** |
| Verb | Part of Speech | 2-2-1, 2-2-2, 2-2-3, **3-1-1**, 3-1-1-1, 3-1-1-2, 3-1-3-1, 3-1-3-2, 3-1-3-4, 3-1-3-5, 3-1-6, 3-2-1-1, 3-2-1-1-2, 3-1-3-3, 3-3-5, 4-3-1-6 |
| Verbal argument indexation | Strategy | **3-1-3-1, 3-3-5** |
| Verbal predicate | Strategy | **3-1-3-5** |
| *Weekday* | Temporal annotation relation | **3-2-2-1** |
| *Wiki* | Non-participant role relation | **3-2-2-4** |
| Wish | Modal semantic category | **3-1-3-3, 4-3-1-6**, 4-3-2 |
| Word senses | Category of UMR objects | 1, 2-1, 2-2-1, **3-1-4** |
| Yabem | Language | 3-2-1-1-1 |
| *Year* | Temporal annotation relation | 2-2-4, **3-2-2-1** |
| *Year2* | Temporal annotation relation | **3-2-2-1** |

[Back to Table of Contents](#toc)
