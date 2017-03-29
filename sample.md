---
title: Widgets
author: Ben Marcata
date: 2016-10-19
profile:
    organization: Marcata Widgets Pty Ltd
    project: Pacifica Complex Doodad Markup
    namespaces:
        ex: http://example.org/pacifica/models#
---

# Widgets (Pacifica Doodad interoperabilty)

## Introduction

This model describes the use of Widgets, the class of objects that includes
jawns, thingamabobs, doodads, and sprockets, in the context of the [Pacifica Complex Doodad Markup](http://example.org/pcdm/interop) interoperability project. 

**NOTES:**

* Widgets SHOULD NOT be used to model Frippery. 

## Use Cases

* Documenting gadgets around your repository, and how Agents use them.
* The Internet of Things

## Model

![Drawing of model](https://gist.githubusercontent.com/anarchivist/981d25acfc1b92ac93a7cf2a9049b4c8/raw/sample.png)


### `ex:Widget < pcdm:Object`

Entailment with `owl:Thing` (from `ex:bogusPredicate`). 

```turtle
ex:Widget a rdfs:Class ; 
    owl:equivalentClass <http://purl.org/NET/raul#Widget> . 
```

| Field            | Predicate                | Recommendation | Expected Value        | Obligation |
| ---------------- | ------------------------ | -------------- | --------------------- | ---------- |
| *bogosity*       | `ex:bogusPredicate`      | MUST           | Literal               | {0,n}      |
| *part of*        | `dcterms:isPartOf`       | SHOULD         | `ex:WidgetCollection` | {0,n}      |
| *has file*       | `pcdm:hasFile`           | SHOULD         | `pcdm:File`           | {1,1}      |
| *label*          | `rdfs:label`             | MAY            | Literal               | {1,1}      |
| *type*           | `rdf:type`               | MUST           | `ex:Widget` (class)   | {0,n}      |


### `ex:WidgetCollection < pcdm:Collection`

| Field            | Predicate                | Recommendation | Expected Value | Obligation |
| ---------------- | ------------------------ | -------------- | -------------- | ---------- |
| *part of*        | `pcdm:hasRelatedObject`  | SHOULD NOT     |                | {0,0}      |
| *label*          | `rdfs:label`             | SHOULD         | Literal        | {1,1}      |

## Usage

### Defining new Widgets and new Widget Classes 

```turtle
<http://example.com/widgets/widget0> a ex:Widget ;
    ex:bogusPredicate "f00f" ;
    pcdm:hasFile <http://example.com/widgets/widget0/screenshot> .

<http://example.com/ns#MyWidget> a rdfs:Class ;
    rdfs:label "My Widget"@en ;
    rdfs:subclassOf ex:Widget.
```

### References to Widgets

```turtle
<http://example.com/collections/collection0> a ex:WidgetCollection ;
    pcdm:hasMember <http://example.com/widgets/widget0> . 
```