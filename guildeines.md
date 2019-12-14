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
'''                   
                    




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


