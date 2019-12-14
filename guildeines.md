# Uniform Meaning Representation (UMR) 0.0.1 Specification
=======================================================

**November 4, 2019**

-AUTHORS-

**Table of Contents**

* Part 1. Introduction
* Part 2. Sentence-Level Representation
    * Part 2-1. Predicate Argument Structure
    * Part 2-2. Aspect
    * Part 2-3. Quantification
    * Part 2-4. Named Entities
    * Part 2-5. Multiple Word Expressions
* Part 3. Document-Level Representation
    * Part 3-1. Coreference
    * Part 3-2. Temporal Dependency
    * Part 3-3. Modality Dependency

##  Part 1. Introduction

The **Uniform Meaning Representation** (UMR) project aims to design a meaning representation that facilitates
the computational interpretation of a text. UMR combines a *sentence-level* representation that is adapted 
from **Abstract Meaning Representation** (AMR), which focuses on *predicte-argument structures*, *word senses*, *named entities*, *multi-word expressions*, *aspect*, and *quantification*, and a document-level representation
that focuses on *coreference*, *temporal* and *modal* relations.


Edmund Pope tasted freedom today for the first time in more than eight months.

```
(t2 / taste-01
  :ARG0 (p / person :wiki "Edmond_Pope"
         :name (n2 / name :op1 "Edmund" :op2 "Pope"))
  :ARG1 (f / free-04
         :ARG1 p)
  :time (t3 / today)
  :ord (o3 / ordinal-entity :value 1
        :range (m / more-than
                :op1 (t / temporal-quantity :quant 8
                    :unit (m2 / month)))))
                    
(temporal-dependencies
    :depends_on (DCT, today)
    :includes (today, taste)
 modal-dependencies
    :POS (Auth, taste))
```
  
```
 Pope is the American businessman who was convicted last week on spying charges and sentenced to 20 years in a Russian prison.

(b2 / businessman
      :mod (c5 / country :wiki "United_States"
            :name (n6 / name :op1 "America"))
      :domain (p / person :wiki "Edmond_Pope"
            :name (n5 / name :op1 "Pope"))
      :ARG1-of (c4 / convict-01
            :ARG2 (c / charge-05
                  :ARG1 b2
                  :ARG2 (s2 / spy-01 :ARG0 p))
            :time (w / week
                  :mod (l / last)))
      :ARG1-of (s / sentence-01
            :ARG2 (p2 / prison
                  :mod (c3 / country :wiki "Russia"
                        :name (n4 / name :op1 "Russia"))
                  :duration (t3 / temporal-quantity :quant 20
                        :unit (y2 / year)))
            :ARG3 s2))
 
( (Temporal
    :includes (last week, convict)
    :includes (last week, sentence))
  (Modal
    :POS (Auth, convict)
    :POS (Auth, sentence)))
```

```
He denied any wrongdoing.
(d / deny-01
      :ARG0 (h / he)
      :ARG1 (t / thing
            :ARG1-of (d2 / do-02
                  :ARG0 h
                  :ARG1-of (w / wrong-02))))

((Temporal    
  :after (DCT, s3|d/deny))
 (Modal
  :POS (Auth, s3|d/deny))
 (Coref
  :same (s1|p/Edmund Pope, s3|h/he)))     
```

```
(p3 / pardon-01
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

  ((Temporal
       :before (convict, pardon))
  (Modal
       :POS (Auth, pardon))
  (Coref
       :same (Edmund Pope, him)))   
```


```
 Pope was flown to the U.S. military base at Ramstein, Germany.
 
(f / fly-01
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

((Temporal
    :before (pardon, flow))
 (Modal
    :POS (Auth, flow)))   
```


```
He will spend the next several days at the medical center there before he returns home with his wife Sherry

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

( (Temporal
    :before (DCT, spend)
    :before (spend, return))
  (Modal
    :POS (Auth, spend)
    :POS (Auth, return))
  (Coref
    :same (Edmund Pope, he)))
```

 ```
   Pope was in remission from a rare form of bone cancer when he was arrested in Russia.

(h / have-mod-91
       :ARG1 (p / person :wiki "Edmond_Pope"
             :name (n3 / name :op1 "Pope"))
       :ARG2 (r / remission-02
             :ARG1 (d / disease :wiki -
                   :name (n / name :op1 "bone" :op2 "cancer")
                   :ARG1-of (r2 / rare-02))
             :time (a / arrest-01
                   :ARG1 p
                   :location (c / country :wiki "Russia"
                         :name (n2 / name :op1 "Russia")))))
```

```
Doctors will examine him for signs that the cancer may have come back while he awaiting trial in a Russian jail.

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
```

```
 A spokeswoman said that Pope was suffering from malnutrition and high blood pressure.
(s / say-01
      :ARG0 (p3 / person
            :ARG0-of (h2 / have-org-role-91
                  :ARG2 (s2 / spokeswoman)))
      :ARG1 (s3 / suffer-01
            :ARG0 (p / person :wiki "Edmond_Pope" :name (n / name :op1 "Pope"))
            :ARG1 (a / and
                  :op1 (m / malnourished-01
                        :ARG1 p)
                  :op2 (p2 / pressure-01
                        :ARG1 (b2 / blood)
                        :ARG1-of (h / high-02))))
((Temporal
   :after (DCT, say)
   :overlap (say, suffer))
 (Modal
   :POS (Auth, say)
   :POS (Auth, spokeswoman)
   :POS (spokeswoman, suffer)))
 ```




             
                    




## Part 2. Sentence-Level Representation

### Part 2-1. Predicate Argument Structure
### Part 2-2. Aspect
### Part 2-3. Quantification
### Part 2-4. Named Entities
### Part 2-5. Multiple Word Expressions

## Part 3. Document-Level Representation
### Part 3-1. Coreference
### Part 3-2. Temporal Dependency
### Part 3-3. Modal Dependency


