# Uniform Meaning Representation (UMR) 0.1 Specification
=======================================================

**November 4, 2019**

-AUTHORS-

**Table of Contents**

* Part 1. Introduction
* Part 2. Sentence-Level Representation
    * Part 2-1. UMR Concepts
      * Part 2-1-1. Named entities  (Bert, Andy)
      * Part 2-1-2. Multiple-word concepts [reflexives,causatives, inchoatives, noun incorporation, identify what counts as light verbs] (Bill et al, Andy)]
      * Part 2-1-3. Multi-concept words (Bill, Andy, James, Martha (reader))[reflexives,causatives, inchoatives, noun incorporation
      * Part 2-1-4. Word senses
    * Part 2-2. UMR relations 
      * Predicate Argument Structure (Bill and Martha)
    * Part 2-3. UMR features 
      * Aspect (could potentially become concepts?)
    * Part 2-4. Quantification, negation (James)
* Part 3. Document-Level Representation
    * Part 3-1. Coreference (Jayeol, Bert) [Should this include event coreference?]
    * Part 3-2. Temporal Dependency (Bert)
    * Part 3-3. Modality Dependency (Meagan, Bill)
* Integrated examples

##  Part 1. Introduction

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
          depends_on (DCT, s1t3/today)
          includes (s1t3/today, s1t2/taste-01)
           )
    :modality(
           :POS (Auth, s1t2/taste-01)
             )
     )
        
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
        includes (s2w/week, s2c4/convict-01)
        includes (s2w/week, s2s/sentence-01)
           )
    :modality(
      POS (Auth, s2c4/convict-01)
      POS (Auth, s2s/sentence-01)
      POS (Auth, s2s2 / spy-01)
             )
     )
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
    :coref(
           same (s1p/person, s3h/he))
    :temporal(
            after (DCT, s3d/deny-01))
    :modality(
            POS (Auth, s3d/deny-01))
            POS (Auth, s3h/he)
            NEG (s3h/he, s3d2/do-02)
     )
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
    :coref(
         Same (s1p/person,s4h2/he))
    :temporal(
         Before (s2c4/convict-01, s4p3/pardon-01))
    :modality(
         POS (Auth, s4p3/pardon-01))
     )
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
    :temporal(
         Before (s4p3/pardon-01, s5f/fly-01))
    :modality(
         POS (Auth, s5f/fly-01))
     )
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
    before (DCT, s6s2/spend-02)
    before (s6s2/spend-02, s6r/return-01))
  :modality
    POS (Auth, s6s2/spend-02)
    POS (Auth, s6r/return-01))
  :coref
    same (s1p/person, s6h2 / he)))
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
  :temporal(
    overlap (s7a/arrest-01, s7r/remission-02)
    after (DCT, s7a/arrest-01))
  :modality
    POS (Auth, s7a/arrest-01)
    POS (Auth, s7r/remission-02)))
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
  :temporal(
    before (DCT, s8e / examine-01))
  :modality(
    POS (AUTH, s8e / examine-01)
    NEU (AUTH, s8c3/come-01)
    POS (AUTH, s8a/await-01))
  :coref(
    Same(s7p / person, s8h/he))) 
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
 :Temporal
   after (DCT, s9s/say-01)
   overlap (s9s/say-01, s9s3/suffer-01))
 :Modality
   POS (Auth, s9s/say-01)
   POS (Auth, s9p3/person)
   POS (s9p3/person, s9s3/suffer-01)))
 ```
The document-level representation indicates the *say-01* event happened before the *say-01* event, and the *suffer-01* event overlaps temporally with the *say-01* event. The modality annotation indicates that from the author's perspective, the *say-01* event definitely happened, and the author indicates that the *suffer-01* event happened according to the spokesperson.  



             
                    




## Part 2. Sentence-Level Representation

### Part 2-1. UMR Concepts
 #### Part 2-1-1. Named entities
 
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
|        |award, law, court-decision, treaty, music-key, musical-note, food-dish, writing-script, variable, program|
|   *Biomedical-entity*| molecular-physical-entity, small-molecule, protein, protein-family, protein-segment, amino-acid, macro-molecular-complex, enzyme, nucleic-acid, pathway, gene, dna-sequence, cell, cell-line, species, taxon, disease, medical-condition|

 #### Part 2-1-2. Multiple-Word concepts
 #### Part 2-1-3. Multi-concept words
 #### Part 2-1-4. Word senses
### Part 2-2. UMR relations 
   #### Predicate Argument Structure
### Part 2-3. UMR features
   #### Aspect
### Part 2-4. Quantification, negation


## Part 3. Document-Level Representation
### Part 3-1. Coreference


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
    :coref(
           same (s1p/person, s3h/he))
    :temporal(
            after (DCT, s3d/deny-01))
    :modality(
            POS (Auth, s3d/deny-01))
            POS (Auth, s3h/he)
            NEG (s3h/he, s3d2/do-02)
     )
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
  :coref (subset (s4h2, s4w)))
```

#### Event coreference
- same-event, subset

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
  :coref (subset (s1a3, s2a))
```

  Meanwhile, Greek authorities announced that they have made two arrests in the case. The first, a 65-year-old man, was reportedly seen torching trees across southern Peloponnese. The second person arrested and charged was a 77-year-old woman who reportedly was seen starting a fire while cooking outside in Zaharo.
  
- Script / subevent?

 Reports suggest that the group of nine were having a **picnic** on Friday when they were abducted in the Saada province of Yemen. A spokesman for the Yemeni Embassy said "The foreigners **ventured** outside the city of Saada without the required police escorts due to the heightened security situation in the area.
 
 
	
 - Event identity


	On Wednesday, two arrests were announced. "We have arrested two people and have detained several more for questioning," said Vasundhara Raje. "
	

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

(s / sentence
  :coref (same-event (s1c, s2c))
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
   :coref (same-event (s2p, s1i)))
```	 



### Part 3-2. Temporal Dependency

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













### Part 3-3. Modal Dependency

The modal annotation takes the form of dependency structures: each event receives an annotation
which indicates which linguistic material it depends on for its temporal
or modal interpretation, and what type of dependency relation holds
between the parent and the child. That is, the nodes in the dependency
structure are linguistic expressions (either events or modal conceivers) and the edges represent modal (epistemic) strength. 

In the modal dependency structure, there are three types of nodes:
events identified in the first pass, modal conceivers (akin to sources),
and the <span>have-condition</span> node for conditional events. The
second pass involves identifying the conceivers in the text, adding the
<span>have-condition</span> node if applicable, and creating the
dependency structure using those nodes and the events identified in the
first pass. This is done in a single pass through the document.

#### Identifying conceivers

##### Author(s)

Every text will have at least one <span>AUTH</span> node, used for the
author(s) of the document. When there are multiple authors (for example,
in a discussion forum, or in a transcript of an interview) each author
will get their own node. It is necessary to add a node for each author
because all of the content in a document is filtered through an author’s
(or speaker’s) perspective.

##### Conceivers other than author(s)

Aside from authors, there are nodes in the modal dependency for
conceivers mentioned in the document; these correspond to sources in
FactBank (). All non-author conceivers are dependent on the author
node(s) because everything in the text is ultimately from the author’s
perspective.

Conceiver nodes are added when another entity’s mental attitude or point
of view towards an event is expressed in the text. Certain types of
predicates inherently involve conceivers/sources: report, knowledge,
belief, opinion, doubt, perception, and inference (). The examples below
in [\[conceivers\]](#conceivers) show some of the types of predicates
that require the introduction of a conceiver node into the modal
dependency structure.

<span id="conceivers" label="conceivers">\[conceivers\]</span>

<span id="Marythinks" label="Marythinks">\[Marythinks\]</span> *Mary
that John **mowed** the
lawn.*  
<span>AUTH</span>  
<span>MARY</span>

<span id="NYTreportedinquiry" label="NYTreportedinquiry">\[NYTreportedinquiry\]</span>
*The New York Times that the impeachment **inquiry** has begun.*  
<span>AUTH</span>  
<span>NEW\_YORK\_TIMES</span>

<span id="perception" label="perception">\[perception\]</span> *John the
cat **eat** breakfast.*  
<span>AUTH</span>  
<span>JOHN</span>

<span id="deonticevent" label="deonticevent">\[deonticevent\]</span>
*Mary to **leave**
early.*  
<span>AUTH</span>  
<span>MARY</span>

<span id="deonticnominal" label="deonticnominal">\[deonticnominal\]</span>
*John really a boat.*  
<span>AUTH</span>  
<span>JOHN</span>

<span id="deonticoblig" label="deonticoblig">\[deonticoblig\]</span>
*The university Mary to **register** by Monday.*  
<span>AUTH</span>  
<span>JOHN</span>

<span id="purpclausecon" label="purpclausecon">\[purpclausecon\]</span>
*Mary is **going** to California **see** the beach.*  
<span>AUTH</span>  
<span>JOHN</span>

As mentioned above, every example (or document) requires the
introduction of an <span>AUTH</span> node. Predicates of belief, as in
[\[Marythinks\]](#Marythinks), also require the addition of a conceiver
node for the believer, here <span>MARY</span>. This is necessary in
order to capture the fact that the modal status of the <span>mow</span>
event is provided by Mary and the author may or may not agree with
Mary’s perspective. Similarly, predicates of reporting, as in
[\[NYTreportedinquiry\]](#NYTreportedinquiry), and perception, as in
[\[perception\]](#perception), require the introduction of conceiver
nodes for the reporter (<span>NEW\_YORK\_TIMES</span>) and the perceiver
(<span>JOHN</span>).

Certain deontic events, such as those in
[\[deonticevent\]](#deonticevent) and
[\[deonticnominal\]](#deonticnominal) also require the addition of a
conceiver node to the dependency structure. Hopes, wishes, desires, and
fears all model the mental content of a conceiver in the text – these
are based on a conceiver’s beliefs or perspective about the world.
Conceiver nodes should be added, even when the complement of the deontic
predicate isn’t an event, as in [\[deonticnominal\]](#deonticnominal).
Obligation deontics, as in [\[deonticoblig\]](#deonticoblig), require
the introduction of a conceiver node for the source of the obligation
(here, <span>JOHN</span>), but not the endpoint of the obligation
(<span>MARY</span>). This is because, in
[\[deonticoblig\]](#deonticoblig), nothing is asserted about Mary’s
beliefs, desires, attitude or perspective.

Purpose clauses, as in [\[purpclausecon\]](#purpclausecon), require the
introduction of a conceiver node for the subject of the sentence; this
is because the author is expressing the intentions of the subject of the
sentence.

As shown by [\[NYTreportedinquiry\]](#NYTreportedinquiry), conceivers
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
as in [\[diffcon\]](#diffcon), and when they’re nested underneath the
same conceiver node, but with a different modal strength value as in
[\[diffstrength\]](#diffstrength). (See §[4.3.2](#conedges) on how to
add conceiver nodes to the dependency structure with modal strength
edges.)

<span id="multconnodes" label="multconnodes">\[multconnodes\]</span>

<span id="diffcon" label="diffcon">\[diffcon\]</span> *John Mary to
**visit** Italy, but I she to **visit** France.*  
<span>AUTH</span>  
<span>JOHN</span>  
<span>MARY\_1</span>  
<span>MARY\_2</span>

<span id="diffstrength" label="diffstrength">\[diffstrength\]</span>
*Mary to **visit** Italy and she to **visit** France as well.*  
<span>AUTH</span>  
<span>MARY\_1</span>  
<span>MARY\_2</span>

In [\[diffcon\]](#diffcon), we need two separate <span>MARY</span>
nodes: one which is dependent on the <span>JOHN</span> node to represent
John’s beliefs about Mary’s beliefs (really, the author’s beliefs about
John’s beliefs about Mary’s beliefs) and one which is nested directly
underneath the <span>AUTH</span> node to represent the author’s beliefs
about Mary’s beliefs. In [\[diffstrength\]](#diffstrength), there are
two separate <span>MARY</span> nodes that correspond to the author’s
different levels of certainty about Mary’s sets of beliefs. One of the
<span>MARY</span> nodes represents Mary’s set of beliefs that the author
is certain of (her desire to visit Italy) and the other
<span>MARY</span> node represents Mary’s beliefs that the author is
unsure of (her desire to visit France).

##### Shared beliefs

Authors may also attribute beliefs to groups of individuals. In these
cases, separate conceiver nodes should be created for each unique group
of individuals; these groups may (or may not) include the author. This
can be seen below in
([\[sharedconceivers\]](#sharedconceivers)).

<span id="sharedconceivers" label="sharedconceivers">\[sharedconceivers\]</span>

*Mary and I that John **left** early. Mary was that John **left**
because they had to **get** pizza later.*  
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

##### Generic and unspecified conceivers

Sometimes, conceivers need to be identified even when they aren’t
explicitly mentioned in the text, as in [\[genericcon\]](#genericcon).

<span id="genericcon" label="genericcon">\[genericcon\]</span>

<span id="prohibit" label="prohibit">\[prohibit\]</span> *My **request**
was .*  
<span>AUTH</span>  
<span>NULL\_HEARER</span>

<span id="report" label="report">\[report\]</span> *It has been that
multiple roads are **closed**.*  
<span>AUTH</span>  
<span>NULL\_REPORTER</span>

This is often the case when predicates that introduce conceivers are
used in passive constructions. Even though there is no span of text that
represents the conceivers, they should still be identified as nodes in
the dependency structure.

Unlike perception events and reporting events, obligation deontics, as
in [\[deonticnocon\]](#deonticnocon), don’t require the introduction of
a null conceiver node.

<span id="deonticnocon" label="deonticnocon">\[deonticnocon\]</span>
*Mary to **register** by Monday.*  
<span>AUTH</span>

When the source of obligation is expressed (as shown above in
[\[deonticoblig\]](#deonticoblig)), a conceiver node is introduced for
the source of the obligation. It is not always clear, however, that an
external source is present when it is not overtly expressed. Therefore,
null conceivers are not identified for obligation deontics.

#### The <span>have-condition</span> node

The <span>have-condition</span> node is a special node that is required
in the modal dependency structure for linguistic material that expresses
hypothetical situations contingent on certain conditions. The canonical
English conditional construction is shown below in
[\[canoncond\]](#canoncond).

<span id="canoncond" label="canoncond">\[canoncond\]</span>

*If it **rains**, Mary will **stay** home.*  
<span>have-condition</span>

Here, the hypothetical situation, Mary staying home, is conditional on
the raining event. The UMR-TAMP annotation does not capture the causal
relation between the <span>rain</span> event and the <span>stay</span>
event; this may be annotated elsewhere in the UMR annotation scheme. The
UMR-TAMP modal annotation captures the fact that both of these events
occur in the same hypothetical scenario – these are not two independent
hypothetical events. The <span>have-condition</span> node acts a parent
to both the <span>rain</span> event and the <span>stay</span> event in
the modal dependency (see §[\[conditionals\]](#conditionals)). This
captures that the events in the conditional construction occupy the same
hypothetical “world” or space and not separate hypothetical
worlds/spaces.

Conditional constructions may take a variety of morphosyntactic forms,
both across languages and within a language. Although the canonical
English conditional construction takes the *if.., then...* form, there
are are other ways to express conditional semantics, such as those in
[\[otherconds\]](#otherconds) below.

<span id="otherconds" label="otherconds">\[otherconds\]</span>

<span id="longas" label="longas">\[longas\]</span> *As long as it
**rains**, Mary will **stay** home.*  
<span>have-condition</span>

<span id="casethat" label="casethat">\[casethat\]</span> *Mary will
**stay** home, in (the) case (that) it **rains**.*  
<span>have-condition</span>

Regardless of the form, the conditional semantics requires the
introduction of the <span>have-condition</span> node.

The <span>have-condition</span> node is also used for different types of
conditionals and constructions related to conditionals. The
<span>have-condition</span> node is also required for counterfactuals,
as in [\[counterfactualrain\]](#counterfactualrain), and concessive
conditionals, as in
[\[concess\]](#concess).

<span id="otherconds" label="otherconds">\[otherconds\]</span>

<span id="counterfactualrain" label="counterfactualrain">\[counterfactualrain\]</span>
*If it had **rained**, Mary would have **stayed** home.*  
<span>have-condition</span>

<span id="concess" label="concess">\[concess\]</span>

*Even if it had **rained**, Mary would have **stayed** home.*  
<span>have-condition</span>

These types of constructions will be annotated differently in terms of
their modal strength values (see §[\[conditionals\]](#conditionals)),
but they all require the introduction of a <span>have-condition</span>
node.

#### Constructing the modal dependency structure

The different types of nodes in the modal dependency structure have been
covered in the previous sections: authors, conceivers,
<span>have-condtion</span>, and the events identified in the first pass.
There is one other node in the dependency structure: a <span>ROOT</span>
node, under which all other nodes are nested.

This section covers the modal strength values that characterize the
edges and guidelines on how to construct the dependency structure. The
different types of nodes are organized within the dependency structure
as shown in Figure [\[exampletree\]](#exampletree).

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

##### Overview of modal edges

As has been stated above, the edges in the modal dependency correspond
to modal strength values. The same edge labels are used at all levels of
the dependency structure, with the exception of the link between the
<span>ROOT</span> and <span>AUTH</span> node(s). This edge label is
always <span>Modal</span>.

Modal strength values correspond to epistemic strength, i.e. the author
or conceiver’s certainty about the occurrence of the event in the real
world, or certainty about another conceiver’s mental content. Based on ,
a typological study of modal systems across languages, and following
FactBank (), the UMR-TAMP annotation distinguishes three levels of modal
strength: Full, Partial, and Neutral, illustrated in
[\[modalvalues\]](#modalvalues).

<span id="modalvalues" label="modalvalues">\[modalvalues\]</span>

<span id="full" label="full">\[full\]</span> Full:  
*The cat already **ate** breakfast.*

<span id="partial" label="partial">\[partial\]</span>

Partial:  
*The cat already **ate** breakfast.*

<span id="neutral" label="neutral">\[neutral\]</span>

Neutral:  
*The cat have already **eaten** breakfast.*

The Full modal value, as in [\[full\]](#full), corresponds to complete
certainty; that is, the conceiver is 100% certain that the event occurs
in the real world. The Neutral modal value, shown in
[\[neutral\]](#neutral), indicates the possibility of the event;
essentially, this corresponds to 50/50 certainty that the event occurs
in the real world. The Partial modal value, as in
[\[partial\]](#partial), falls between the Full and Neutral values; the
conceiver believes that more likely than not, the event occurs in the
real world.

Also following FactBank (), the UMR-TAMP annotation scheme combines the
three-way epistemic strength distinction (Full, Partial, Neutral) with a
binary polarity distinction (Positive, Negative). This results in six
modal strength values shown below in Table
[\[introvalues\]](#introvalues).

| Label                                  | Value                               |
| :------------------------------------- | :---------------------------------- |
| <span class="smallcaps">pos</span>     | full strength, positive polarity    |
| <span class="smallcaps">prt</span>     | partial strength, positive polarity |
| <span class="smallcaps">neut</span>    | neutral strength, positive polarity |
| <span class="smallcaps">neutneg</span> | neutral strength, negative polarity |
| <span class="smallcaps">prtneg</span>  | partial strength, negative polarity |
| <span class="smallcaps">neg</span>     | full strength, negative polarity    |

Epistemic strength labels<span label="introvalues"></span>

The following sections will show how these edge values are applied to
different types of nodes in the modal dependency structure. Throughout
these sections, the format <span>Edge(Child node,Parent node)</span>
will be used to represent the dependency structure.

##### Edges between conceiver nodes

As mentioned above, the edge between the <span>ROOT</span> and the
<span>AUTH</span> is always <span>Modal</span> and does not take one of
the modal strength values shown above in Table
[\[introvalues\]](#introvalues). Every other edge in the modal
dependency, however, is characterized by the modal strength values.

For edges between two conceiver nodes, these values represent the degree
of confidence a conceiver has in modelling the contents of another
conceiver’s set of beliefs. That is, the author (or another conceiver)
may have different levels of confidence about whether or not a
particular individual holds the set of beliefs represented by a
conceiver node. Examples for each of the six possible edges values is
shown below in Table [\[conceiveredge\]](#conceiveredge).

| Annotation                      | Example                          |
| :------------------------------ | :------------------------------- |
| <span>Pos(MARY,AUTH)</span>     | *Mary believes the cat **ate**.* |
| <span>Prt(MARY,AUTH)</span>     | *Mary believes the cat **ate**.* |
| <span>Neut(MARY,AUTH)</span>    | *Mary believe the cat **ate**.*  |
| <span>NeutNeg(MARY,AUTH)</span> | *Mary believe the cat **ate**.*  |
| <span>PrtNeg(MARY,AUTH)</span>  | *Mary believe the cat **ate**.*  |
| <span>Neg(MARY,AUTH)</span>     | *Mary believe the cat **ate**.*  |

Edges between conceiver nodes<span label="conceiveredge"></span>

For example, in *Mary might believe the cat ate*, the author is unsure
whether or not Mary holds the belief about the eating event. Therefore,
there is a <span>Neut</span> relation between the <span>AUTH</span> node
and the <span>MARY</span> conceiver node.

Note that this edge captures the author (or parent conceiver) node’s
certainty about the set of beliefs of the child conceiver node. That is,
it is not capturing the child conceiver’s certainty about the event in
question. Generally, when a predicate that introduces a conceiver is
modalized, the strength indicated by the modal is annotated between the
conceiver nodes, as in [\[deonticcon\]](#deonticcon).

<span id="deonticcon" label="deonticcon">\[deonticcon\]</span>

<span id="think" label="think">\[think\]</span> *Mary thinks the cat
might have **eaten** breakfast.*  
<span>Pos(MARY,AUTH)</span>

<span id="doubt" label="doubt">\[doubt\]</span> *Mary probably doubts
that the cat **ate** breakfast.*  
<span>Prt(MARY,AUTH)</span>

In [\[think\]](#think), Mary is uncertain about the eating event, but
there is a <span>Pos</span> edge between the <span>AUTH</span> and
<span>MARY</span> nodes because the author is sure of Mary’s beliefs
(§[4.3.3](#modaleventedges) covers how to annotate Mary’s uncertainty).
In [\[doubt\]](#doubt), the author only has probable certainty about
Mary’s beliefs, annotated with the <span>Prt</span> edge between the
<span>AUTH</span> and <span>MARY</span> nodes.

##### Edges involving event nodes

The same set of six epistemic strength values are used for edges that
involve events; there are also two additional unspecified values. This
section covers the edges between conceivers and events and between two
events (the parental options for events in the modal dependency
structure are fairly limited by the semantics of the text, but see
section [\[parentnodes\]](#parentnodes) on selecting appropriate parent
nodes). The eight values and their interpretation for events nodes are
shown below. The corresponding FactBank values are shown in parentheses.

> <span>Pos</span>: full positive support; complete certainty that the
> event occurs (CT+)  
> <span>Prt</span>: partial positive support; there is strong, but not
> definitive certainty that the event occurs (CR+)  
> <span>Neut</span>: positive neutral support; there is neutral
> certainty that the event occurs/doesn’t occur; event is expressed
> positively (PS+)  
> <span>NeutNeg</span>: negative neutral support; there is neutral
> certainty that the event occurs/doesn’t occur; negation of event is
> expressed (PS-)  
> <span>PrtNeg</span>: partial negative support; there is strong but not
> definitive certainty that the event does not occur (PR-)  
> <span>Neg</span>: full negative support; complete certainty that the
> event does not occur (CT-)  
> <span>Unsp</span>: The conceiver knows that the event either did or
> did not occur, but is uncertain about the polarity (CTu)  
> <span>NegUnsp</span>: The conceiver does not know what the factual
> status of the event is, or does not commit to it (Uu)

Degree of certainty corresponds most straightforwardly to the degree of
confidence of a conceiver in the occurrence of an episodic event, i.e.
the epistemic/evidential continuum from certainty to possibility and
from direct evidence to second-hand (reported or inferred) evidence. We
use the same values for epistemic/evidential support and deontic
modality. The interpretation of the value - as epistemic/evidential or
deontic - is not reflected in the modal annotation.

###### Non-future events

For non-future (non-deontic) events, the strength values correspond to
the conceiver’s level of certainty towards the occurrence of the event
in the real world. Events presented as fact by a conceiver will be
annotated with <span>Pos</span>, while events for which the conceiver
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
exemplified in ([\[episodic\]](#episodic)).

<span id="episodic" label="episodic">\[episodic\]</span>

<span id="anaphora" label="anaphora">\[anaphora\]</span> *The dog
**barked** last night*.  
<span>Pos(bark,AUTH)</span>

<span id="anaphora" label="anaphora">\[anaphora\]</span> *The dog
**barked** last night.*  
<span>Prt(bark,AUTH)</span>

<span id="anaphora" label="anaphora">\[anaphora\]</span> *The dog have
**barked** last night.*  
<span>Neut(bark,AUTH)</span>

<span id="anaphora" label="anaphora">\[anaphora\]</span> *The dog have
**barked** last night.*  
<span>NeutNeg(bark,AUTH)</span>

<span id="anaphora" label="anaphora">\[anaphora\]</span> *The dog
**bark** last night.*  
<span>PrtNeg(bark,AUTH)</span>

<span id="anaphora" label="anaphora">\[anaphora\]</span> *The dog
**bark** last night.*  
<span>Neg(bark,AUTH)</span>

###### Future events and deontic modality

For events embedded in deontic modals, or presented as (potentially)
happening in the future, modal strength refers to the predictability of
the occurrence of the event in the future, as presented by the
conceiver. Predictive future has full strength (<span>Pos</span> or
<span>Neg</span>); intentions, commands, and purpose clauses correspond
to partial strength (<span>PosPrt</span> or <span>NegPrt</span>); and
desire and permission correspond to neutral (<span>Neut</span> or
<span>NeutNeg</span>) strength. This is illustrated in
([\[futurestrength\]](#futurestrength)).

<span id="futurestrength" label="futurestrength">\[futurestrength\]</span>

<span id="futpos" label="futpos">\[futpos\]</span> *I **go** to Santa
Fe*.  
<span>Pos(go,AUTH)</span>

<span id="futprt" label="futprt">\[futprt\]</span> *I to **go** to Santa
Fe. / You **go** to Santa Fe.* / *I’m getting my car **fixed** **go** to
Santa Fe.*  
<span>Prt(go,AUTH)</span>

<span id="futneut" label="futneut">\[futneut\]</span> *I to **go** to
Santa Fe. / You are to **go** to Santa Fe.*  
<span>Neut(go,AUTH)</span>

The predictive future, as in [\[futpos\]](#futpos), is annotated with
full modal strength because it presents the future event as a certainty
(i.e., it is as certain as is possible for future events). Intentions,
commands, and purpose clauses, as in [\[futprt\]](#futprt), are
annotated with partial modal strength because they present the future
event as less likely than the predictive future, but more likely to
happen than the neutral strength deontics. Finally, desire and
permission, as in [\[futneut\]](#futneut), are annotated as neutral
strength.

Examples like [\[futuretests\]](#futuretests) demonstrate how the
predictive future, intention, and desire present events with different
future likelihoods, based on whether or not they’re compatible with
different strength negatives of the same event.

<span id="futuretests" label="futuretests">\[futuretests\]</span>

<span id="futtestpos" label="futtestpos">\[futtestpos\]</span> *\*I will
go to Santa Fe, but I won’t go.*  
*\*I will go to Santa Fe, but I probably won’t go.*  
*\*I will go to Santa Fe, but I might not go.*

<span id="futtestprt" label="futtestprt">\[futtestprt\]</span> *\*I
intend to go to Santa Fe, but I won’t go.*  
*\*I intend to go to Santa Fe, but I probably won’t go.*  
*I intend to go to Santa Fe, but I might not go.*

<span id="futtestneut" label="futtestneut">\[futtestneut\]</span> *I
want to go to Santa Fe, but I won’t go.*  
*I want to go to Santa Fe, but I probably won’t go.*  
*I want to go to Santa Fe, but I might not go.*

The predictive future, as in [\[futtestpos\]](#futtestpos), can’t
combine with any strength of negative. This is because full positive
strength doesn’t allow for any uncertainty, or any possibility that the
event does not occur. The partial strength future/deontic events, like
intention as in [\[futtestprt\]](#futtestprt), are only compatible with
a neutral strength negative of the same event. Partial strength allows
for the possibility that the event won’t occur in the future, but can’t
occur with the partial (or full) strength negative of the event. Neutral
strength future/deontics, like desires as in
[\[futtestneut\]](#futtestneut), can occur with any strength negative of
the same event, since the event is only presented as a possibility.

As mentioned in §[4.3.2](#conedges) modalized deontic predicates capture
the modal value with the link between the <span>AUTH</span> and the
conceiver node. This means that the link between a conceiver and the
node for the deontic predicate is very often a default <span>Pos</span>
value; see example ([\[defaultpos\]](#defaultpos)).

<span id="defaultpos" label="defaultpos">\[defaultpos\]</span> *Mary
**want** to **visit** France.*  
<span>Neut(MARY,AUTH)</span>  
<span>Pos(want,MARY)</span>  
<span>Neut(visit,want)</span>

This is because the link between a conceiver and the deontic predicate
represents the modal strength of the event with respect to the
conceiver, and not the author. That is, the author is unsure of Mary’s
desires; the author is not asserting that Mary is unsure of her own
desires.

When the conceiver is unsure of their own beliefs, desires, etc., this
is represented with the link between the conceiver and the deontic
predicate, as in ([\[mightwant\]](#mightwant)).

<span id="mightwant" label="mightwant">\[mightwant\]</span>

*Mary that she **want** to **visit** France.*  
<span>Pos(MARY,AUTH)</span>  
<span>Neut(want,MARY)</span>  
<span>Neut(visit,want)</span>

Here, the author is sure of Mary’s beliefs, so there is a
<span>Pos</span> link between the author and Mary’s set of beliefs. But,
Mary herself is unsure of her desire to visit France; therefore, there
is a <span>Neut</span> link between the <span>MARY</span> node and the
<span>want</span> node.

###### Interaction of modal strength and negation

Since the modal edge values combine both epistemic strength and
polarity, the interaction of negation (polarity) and epistemic strength
within a construction requires further annotation guidelines. As is the
case with the UMR-TAMP annotation scheme in general, it is important to
annotate the meaning of the text, regardless of its morphosyntactic
form. For example, certain constructions in English exhibit what is
often called neg-raising, as in [\[negraise1\]](#negraise1).

<span id="negraisethink" label="negraisethink">\[negraisethink\]</span>

<span id="negraise1" label="negraise1">\[negraise1\]</span> *Mary John
**is in** his office.*  
<span>Pos(MARY,AUTH)</span>  
<span>Neg(be-in,MARY)</span>

<span id="negraise2" label="negraise2">\[negraise2\]</span> *Mary John
**isn’t in** his office.*  
<span>Pos(MARY,AUTH)</span>  
<span>Neg(be-in,MARY)</span>

Although the negation in [\[negraise1\]](#negraise1) is syntactically on
*think*, the meaning of [\[negraise1\]](#negraise1) and
[\[negraise2\]](#negraise2) is the same. That is, that Mary has a belief
that John is in not in his office. Therefore, both of these have the
same annotation, with the negation represented between the
<span>MARY</span> node and the <span>be-in</span> node. Further examples
of this can be seen below in [\[negraise\]](#negraise).

<span id="negraise" label="negraise">\[negraise\]</span>

<span id="POS" label="POS">\[POS\]</span> *Mary **want** to **go**. /
Mary **wants** to **go**.*  
<span>Pos(MARY,AUTH)</span>  
<span>Pos(want,MARY)</span>  
<span>NeutNeg(go,want)</span>

<span id="NEUT" label="NEUT">\[NEUT\]</span> *Mary **planning** on
**going**. / Mary is **planning** to **go**.*  
<span>Pos(MARY,AUTH)</span>  
<span>Pos(plan,MARY)</span>  
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
example ([\[combo\]](#combo)) below.

<span id="combo" label="combo">\[combo\]</span>

<span id="POS" label="POS">\[POS\]</span> *Mary to **go**. / Mary
(choose to) **go**.*  
<span>NeutNeg(go,AUTH)</span>

<span id="NEUT" label="NEUT">\[NEUT\]</span> *Mary is to **go**. / Mary
is to **go**.*  
<span>NegPrt(go,AUTH)</span>

*Mary **open** the box. / that Mary **open** the box.*  
<span>NegPrt(open,AUTH)</span>

*He **be in** his office. / that he **is** **in** his office.*  
<span>NeutNeg(be-in,AUTH)</span>

There are also cases where the modal value of the edge is not a
straightforward combination of the modal strength and negation. Examples
of these can be seen below in ([\[notcombo\]](#notcombo)).

<span id="notcombo" label="notcombo">\[notcombo\]</span>

<span id="POS" label="POS">\[POS\]</span> *for Mary **to be** in France
already.*  
<span>Neg(be-in,AUTH)</span>

<span id="NEUT" label="NEUT">\[NEUT\]</span> *You **enter**. / for you
**to enter**.*  
<span>NegPrt(enter,AUTH)</span>

In these cases, the combination of a weak modal (*can, may*) with
negation leads to a stronger negative strength relation (either full or
partial).

###### Selecting parent nodes

For each event annotated for modality, both a modal strength edge value
and a parent node must be selected. In the majority of cases, it is
rather straightforward which node should be selected as the parent of an
event in question.

<span id="clearparent" label="clearparent">\[clearparent\]</span>

<span id="travel" label="travel">\[travel\]</span> *Mary **travelled**
to France.*  
<span>Pos(travel,AUTH)</span>

<span id="grammodal" label="grammodal">\[grammodal\]</span> *Mary might
**travel** this summer.*  
<span>Neut(travel,AUTH)</span>

<span id="purpclause" label="purpclause">\[purpclause\]</span> *Mary
will **travel** to France in order to **see** the Louvre.*  
<span>Pos(travel,AUTH)</span>  
<span>Pos(MARY,AUTH)</span>  
<span>Prt(see,MARY)</span>

<span id="belief" label="belief">\[belief\]</span> *Mary thinks she will
**travel** to France.*  
<span>Pos(MARY, AUTH)</span>  
<span>Pos(travel,MARY)</span>

For the events in examples like [\[travel\]](#travel) and
[\[grammodal\]](#grammodal), <span>AUTH</span> is the parent node of the
event. Grammaticalized modals aren’t annotated as their own nodes,
therefore events under the scope of their modality are annotated
directly underneath the relevant conceiver node, such as the author in
[\[grammodal\]](#grammodal). The events in purpose clauses, as in
[\[purpclause\]](#purpclause), are also represented as direct children
of the conceiver node (here, <span>MARY</span>). Since belief predicates
also aren’t represented as nodes in the annotation, the complements of
belief predicates will be linked directly to the relevant conceiver, as
in ([\[belief\]](#belief)).

There are also cases where there may be a choice between selecting a
conceiver or another event as the parent node. This is specifically the
case when modal predicates are represented as their own events (nodes)
in the annotation, as in ([\[modalevent\]](#modalevent)).

<span id="modalevent" label="modalevent">\[modalevent\]</span>

<span id="wants" label="wants">\[wants\]</span> *Mary **wants** to
**travel** this summer.*  
<span>Pos(MARY,AUTH)</span>  
<span>Pos(want,MARY)</span>  
<span>Neut(travel,want)</span>

<span id="decided" label="decided">\[decided\]</span> *Mary **decided**
to **travel** this summer.*  
<span>Pos(MARY,AUTH)</span>  
<span>Pos(decide,MARY)</span>  
<span>Prt(travel,decide)</span>

<span id="expects" label="expects">\[expects\]</span> *Mary **expects**
to **travel** this summer.*  
<span>Pos(MARY,AUTH)</span>  
<span>Pos(expect,MARY)</span>  
<span>Prt(travel,expect)</span>

<span id="allows" label="allows">\[allows\]</span> *This bar **allows
smoking**.*  
<span>Pos(BAR,AUTH)</span>  
<span>Pos(allow,BAR)</span>  
<span>Neut(smoke,allow)</span>

<span id="allows" label="allows">\[allows\]</span> *We are **required**
to **order** two drinks.*  
<span>Pos(require,AUTH)</span>  
<span>Neut(order,require)</span>

In these cases, it may not be clear whether the node for the modalized
event (e.g., <span>travel</span> in [\[wants\]](#wants)) should be a
direct child of the relevant conceiver (<span>MARY</span>) or the modal
predicate event node (<span>want</span>). In all clauses with modal
predicates, the modalized event (e.g., <span>travel</span>) should be
represented as the child of the modal predicate (e.g.,
<span>want</span>) and not directly underneath the conceiver. This is
the only case (aside from reporting events, covered in
§[\[reportingevents\]](#reportingevents) below) where events will be
the children of other events instead of (a direct child of) the relevant
conceiver. The event is still nested underneath the relevant conceiver,
just not as its direct child.

If multiple events are presented with the same modal strength, they
should be linked to the same parent node with the appropriate modal
strength value; they should not be linked to each
other.

<span id="samespace" label="samespace">\[samespace\]</span>

<span id="mighttravelwork" label="mighttravelwork">\[mighttravelwork\]</span>
*Mary might **travel** and **work** on a paper this
summer.*  
<span>Neut(travel,AUTH)</span>  
<span>Neut(work,AUTH</span>

<span id="wanttravelwork" label="wanttravelwork">\[wanttravelwork\]</span>
*Mary **wants** to **travel** and **work** on a paper this summer*.  
<span>Pos(MARY,AUTH)</span>  
<span>Pos(want,MARY)</span>  
<span>Neut(travel,want)</span>  
<span>Neut(work,want)</span>

In [\[mighttravelwork\]](#mighttravelwork), the author has a neutral
epistemic stance towards both the *travel* and *work* events; these
events are annotated separately as children of the <span>AUTH</span>
node and not directly linked to each other. Similarly, in
[\[wanttravelwork\]](#wanttravelwork), both *travel* and *work* are
Mary’s desires; they are both annotated as children of
<span>want</span> and not linked to each other.

###### Nested modal strengths

The main way in which this annotation differs from FactBank is that it
allows for the nesting of modal strengths; that is, events can be
annotated as the children of other (possibly modalized) events in the
dependency structure. This is especially often the case when dealing
with deontic modals, as in [\[nesting\]](#nesting).

<span id="nesting" label="nesting">\[nesting\]</span>

<span id="mayneed" label="mayneed">\[mayneed\]</span> *I **need** to
**bring** a rain coat*.  
<span>Neut(need-01,AUTH)</span>  
<span>Prt(bring-01,need-01)</span>

<span id="probablywant" label="probablywant">\[probablywant\]</span>
*I’ll **want** to **leave** early*.  
<span>Prt(want,AUTH)</span>  
<span>Neut(leave,want)</span>

In [\[mayneed\]](#mayneed), the partial strength deontic *need* is
embedded within the neutral epistemic modal *may*. In an annotation
scheme which does not allow nesting, it is not clear whether *bring*
should be annotated as neutral or partial strength. Here, however, we
can capture both by annotating *need* as neutral strength depending
directly on the author, and *bring* as partial strength depending on
*need*. This is the reason why the complements of modal predicates are
annotated as children of the modal predicate: by annotating
<span>leave</span> as dependent on <span>want</span>, we can capture the
nested modal strengths in an example like
[\[probablywant\]](#probablywant).

###### Conditionals

Conditional constructions are some of the most complex modal expressions
and therefore require more specific annotation guidelines. As discussed
in [4.2](#havecondnode), conditionals require the addition of a
<span>have-condition</span> node. For hypothetical (i.e., prototypical)
conditionals, the <span>have-condition</span> node is linked to the
relevant conceiver with a <span>Neut</span> edge label; the protasis and
apodosis are linked to the <span>have-condition</span> node with their
appropriate modal strength. Examples are shown in
[\[basicconds\]](#basicconds).

<span id="basicconds" label="basicconds">\[basicconds\]</span>

<span id="posposcond" label="posposcond">\[posposcond\]</span> *If it
**rains**, I’ll **stay** home.*  
<span>Neut(have-condition,AUTH)</span>  
<span>Pos(rain,have-condition)</span>  
<span>Pos(stay,have-condition)</span>

<span id="posneutcond" label="posneutcond">\[posneutcond\]</span> *If it
**rains**, I **stay** home.*  
<span>Neut(have-condition,AUTH)</span>  
<span>Pos(rain,have-condition)</span>  
<span>Neut(stay,have-condition)</span>

<span id="neutnegcond" label="neutnegcond">\[neutnegcond\]</span> *As
long as it **rain**, I’ll **go** to school.*  
<span>Neut(have-condition,AUTH)</span>  
<span>Neg(rain,have-condition)</span>  
<span>Prt(go,have-condition)</span>

<span id="multpros" label="multpros">\[multpros\]</span> *If it **rain**
and if I **find** a ride, I’ll **go** to school and **take** the
test.*  
<span>Neut(have-condition,AUTH)</span>  
<span>Neg(rain,have-condition)</span>  
<span>Pos(find,have-condition)</span>  
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
<span>have-condition</span> node reflects the event’s modal value within
the conditional. In [\[posposcond\]](#posposcond), where there’s no
negation or modals, both events have a <span>Pos</span> relation to the
<span>have-condition</span> node. In [\[posneutcond\]](#posneutcond),
the apodosis includes the modal *might* and therefore there is a
<span>Neut</span> edge between the <span>stay</span> event and the
<span>have-condition</span> node. Example
[\[neutnegcond\]](#neutnegcond) has a negative in the protasis and the
partial strength *probably* in the apodosis. This is annotated with a
<span>Neg</span> edge between <span>rain</span> and
<span>have-condition</span> and a <span>Prt</span> edge between
<span>go</span> and <span>have-condition</span>.

As is shown in [\[multpros\]](#multpros), there may be multiple events
in the protasis and/or apodosis. All events are linked to the
<span>have-condition</span> node with the appropriate modal strength
edge value.

As mentioned in [4.2](#havecondnode), the <span>have-condition</span>
node is also used for counterfactuals, as in
[\[counterfactual\]](#counterfactual), and in concessive conditionals,
as in
[\[concessive\]](#concessive).

<span id="otherconds" label="otherconds">\[otherconds\]</span>

<span id="counterfactual" label="counterfactual">\[counterfactual\]</span>

*If it had **rained**, I would have **stayed** home.*  
<span>Neg(have-condition,AUTH)</span>  
<span>Pos(rain,have-condition)</span>  
<span>Pos(go,have-condition)</span>  
<span id="concessive" label="concessive">\[concessive\]</span> *Even if
it is **raining**, I will **go** to school.*  
<span>Neut(have-condition,AUTH)</span>  
<span>Pos(rain,have-concession)</span>  
<span>Pos(go,have-concession)</span>

The structure of the dependency is the same for counterfactuals and
concessive conditionals as it is for hypothetical conditionals: that is,
the events in the protasis and apodosis are children of the
<span>have-condition</span> node. For counterfactuals, as in
[\[counterfactual\]](#counterfactual), the edge value between the
conceiver and the <span>have-condition</span> node is full negative
(<span>Neg</span>). This is because counterfactuals present the events
in both the protasis and apodosis as (certaintly) not occurring.
Concessive conditionals, as in [\[concessive\]](#concessive), are
annotated with a <span>Neut</span> link between the conceiver and the
<span>have-condition</span> node.

Like hypothetical conditionals, the events in the protasis and apodosis
of counterfactuals and concessive conditionals may be negated or
modalized; there also may be multiple events in the protasis or
apodosis. These are shown in [\[othercondmods\]](#othercondmods).

<span id="othercondmods" label="othercondmods">\[othercondmods\]</span>

<span id="negneutcond" label="negneutcond">\[negneutcond\]</span> *I
have **gone** to school, if it **rained** and if I had **woken** up on
time.*  
<span>Neg(have-condition,AUTH)</span>  
<span>Neut(go,have-condition)</span>  
<span>Neg(rain,have-condition)</span>  
<span>Pos(wake,have-condition)</span>

<span id="concessivenegneut" label="concessivenegneut">\[concessivenegneut\]</span>
*Even if it **raining**, I **go** to school.*  
<span>Neut(have-condition,AUTH)</span>  
<span>Neg(rain,have-condition)</span>  
<span>NeutNeg(go,have-condition)</span>

<span>-2.5ex-1ex -.25ex</span><span>1.25ex
.25ex</span><span>****</span><span>Reporting events</span>
<span id="reportingevents" label="reportingevents">\[reportingevents\]</span>

Reporting or saying events (e.g., *say, tell, shout, report*) also
require special guidelines. These types of events, as in
[\[basicreports\]](#basicreports), express both an event in the
(author’s) ‘real-world’ and the mental content of the agent of the
reporting predicate. This means that the agents of reporting predicates
should be identified as conceivers. The conceiver node represents the
fact that what a person (or a group of people) says is on some level
based on their beliefs - either they report their beliefs accurately, or
they lie, pretend, or otherwise misrepresent their beliefs. Therefore,
the reporting predicate (like <span>say</span> in
[\[Marysaid\]](#Marysaid) and <span>report</span> in
[\[NYTreported\]](#NYTreported)) are annotated as a child of the
<span>AUTH</span> node; the events that are reported are annotated as
children of the reporter conceiver node (<span>MARY</span> in
[\[Marysaid\]](#Marysaid) and <span>NEW\_YORK\_TIMES</span> in
[\[NYTreported\]](#NYTreported).

<span id="basicreports" label="basicreports">\[basicreports\]</span>

<span id="Marysaid" label="Marysaid">\[Marysaid\]</span> *Mary **said**
that she **went** to Santa Fe.*  
<span>Pos(MARY,AUTH)</span>  
<span>Pos(say,AUTH)</span>  
<span>Pos(go,MARY)</span>

<span id="NYTreported" label="NYTreported">\[NYTreported\]</span> *The
New York Times **reported** that Congress **voted** on the bill this
afternoon.*  
<span>Pos(NEW\_YORK\_TIMES,AUTH)</span>  
<span>Pos(report,AUTH)</span>  
<span>Pos(vote,NEW\_YORK\_TIMES)</span>

The annotation of the reporting predicate directly underneath the
<span>AUTH</span> node represents the fact that the reporting event
occurs in the real world. The reported events, however, do not
(necessarily) occur in the real world, but they reflect the mental
content of the agent of the reporting predicate.

When the author is certain that the reporting event occurs, as in
[\[Marysaid\]](#Marysaid) and [\[NYTreported\]](#NYTreported), this is
annotated with a <span>Pos</span> value between the author node and the
reporting event; this is also annotated in the link between the author
node and the conceiver node for the agent of the reporting predicate.
That is, the author’s certainty about the conceiver’s beliefs is based
on the author’s certainty about the occurrence of the reporting event.
With reporting events, the author’s evidence for the conceiver’s beliefs
comes from the reporting event; therefore the edge between the author
node and the reporting event node and the edge between the author node
and the reporting conceiver node will always have the same modal value.

For example, in [\[Marysaid\]](#Marysaid), the author is certain that
the reporting event occurred and therefore the author is certain about
Mary’s set of of beliefs. Note that this annotation doesn’t capture the
author’s certainty about the reported events, i.e. in
[\[Marysaid\]](#Marysaid) the author doesn’t have a perspective on
whether or not Mary actually went to Santa Fe. This faithfully
represents the semantics of reporting constructions; the author doesn’t
express an opinion on the reality of the reported events.

When the author is uncertain about the occurrence of the reporting
event, this is also reflected in both the edge between the author and
the reporting predicate and the edge between the author and the
reporting conceiver; see [\[mightsay\]](#mightsay) and
[\[notsay\]](#notsay).

<span id="reportsuncertain" label="reportsuncertain">\[reportsuncertain\]</span>

<span id="mightsay" label="mightsay">\[mightsay\]</span>

*Mary have **said** that she **went** to Santa Fe.*  
<span>Neut(MARY,AUTH)</span>  
<span>Neut(say,AUTH)</span>  
<span>Pos(go,MARY)</span>

<span id="notsay" label="notsay">\[notsay\]</span> *Mary **say** that
she **went** to Santa Fe.*  
<span>Neg(MARY,AUTH)</span>  
<span>Neg(say,AUTH)</span>  
<span>Pos(go,MARY)</span>

In [\[mightsay\]](#mightsay), the neutral modal strength indicated by
*might* corresponds to both the <span>Neut</span> edge between the
<span>AUTH</span> and <span>MARY</span> nodes and the <span>Neut</span>
edge between the <span>AUTH</span> and <span>say</span> nodes. As
explained above, if the author is uncertain about whether the saying
event occurs, the author must also be uncertain about Mary’s beliefs (as
expressed in the saying event). Similarly, if the author believes that
the saying event did not occur, as in [\[notsay\]](#notsay), there is a
<span>Neg</span> edge between both the <span>AUTH</span> and
<span>MARY</span> nodes and between the <span>AUTH</span> and
<span>say</span> nodes.

Finally, the edge between the reporting event and the reported event(s)
reflects the modal status of the reported events, as in
[\[reportnest\]](#reportnest).

<span id="reportnest" label="reportnest">\[reportnest\]</span>

<span id="sayneut" label="sayneut">\[sayneut\]</span> *Mary **said**
that John have **gone** to Santa Fe.*  
<span>Pos(MARY,AUTH)</span>  
<span>Pos(say,AUTH)</span>  
<span>Neut(go,MARY)</span>

<span id="sayprt" label="sayprt">\[sayprt\]</span> *Mary **said** that
John **go** to Santa Fe.*  
<span>Pos(MARY,AUTH)</span>  
<span>Pos(say,AUTH)</span>  
<span>NegPrt(go,MARY)</span>

In [\[sayneut\]](#sayneut), Mary reports the *go* event with only
neutral certainty; this is reflected in the edge between the
<span>say</span> and <span>go</span> events. In [\[sayprt\]](#sayprt),
Mary reports the *go* event with negative partial certainty; this is
also reflected in the edge between the <span>say</span> and
<span>go</span> events.

#### English constructions and lexical items

This list gives the modal strength value associated with common English
modal constructions (this is certaintly not an exhaustive list). For
modal predicates that are identified as their own event node (e.g.,
deontic predicates), the modal strength value characterizes the link
between the modal predicate node and its child event. For example,
*want* is in the <span>Neut(ral)</span> list, which indicates that there
is a <span>Neut</span> link between the <span>want</span> node and its
complement event node.  
(full positive)

  - Simple assertions: declarative sentences

  - Certainty: *certainly, be sure, definitely, necessarily*

  - Predictive future: *will,* non-intentional *be going to*

  - Factual predicates: *manage to, finished*

(partial positive)

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

(neutral positive)

  - Weak epistemic modals: *may, might/might have, could have*

  - Weak epistemic adverbs/adjectives: *maybe, possibly/be possible
    that*

  - Conditionals

  - Hope/Fear: *hope, fear, worry, dread*

  - Weak deontic modals
    
      - Desire: *want, prefer, would like to*
    
      - Permission: *let, permit, allow*

(neutral negative)

  - Doubt: *doubt, call into question, be dubious that, be skeptical
    that*

  - Combination of (some) <span>Neut</span> lexical items with negation

(partial negative)

  - Strong negative deontics: *forbid, ban, disallow*

  - Negative imperatives

  - Combination of (some) <span>Prt</span> lexical items with negation

(full negative)

  - Negation: *not, never, no* + noun phrase

  - Negative complement taking predicates that entail that the event
    didn’t happen: *deny, prevent, prohibit, block, cease, it is
    impossible that, avoid*

  - Counterfactuals

  - Wishes: *wish*

  
  
 ## Part 4: Integrated examples

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


