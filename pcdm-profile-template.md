---
title: PCDM Newspaper Model
author:
- Joshua A. Westgard
date: 2017-03-29
profile:
    project: PCDM Profiles
    namespaces:
        pcdm: http://pcdm.org/models#
---

# PCDM Newspaper Model

This is a draft profile for modeling newspaper content using the [Portland Common Data Model](http://pcdm.org/) (PCDM). The profile is based on the template created by anarchivist and shared via https://gist.github.com/anarchivist/981d25acfc1b92ac93a7cf2a9049b4c8/.

**NOTES:**
* The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).
* All profiles MAY refer to other ontologies or models other than PCDM.
* All profiles following this template MUST comply with Github-flavored Markdown.
    * All sections MAY have one or more notes associated with them, indicated by the phrase `**NOTES:**` followed by a Markdown list.
* Appropriate sections MAY contain examples of resource definition in RDF.
    * All examples MUST be provided as Turtle and SHOULD be marked up with a code-fenced block indicating the format is Turtle (see examples below).
    * The indentation of the code-fenced blocks below is understood to be non-normative.
* All profiles MAY include Jekyll YAML frontmatter at the top.
    * If including YAML frontmatter, it is RECOMMENDED to include a `profile` key with a YAML mapping containing `organization` and `project` keys as appropriate.
    * The `profile` key MAY have a `namespaces` key, which contains a mapping associating namespace prefixes with their base URIs.

Example:

```markdown
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
```

# Profile or model name

The shorthand, natural language noun used to define to identify the profile or model.

**NOTES:**
* All profiles MUST have a model name.
* All profile names SHOULD be in a plural form (e.g., prefer `Books` over `Book`)
* Profile names MAY contain information about the project or organization.

Example:

```markdown
# Widgets (Pacifica Doodad interoperabilty)
```

## Introduction 

Include here an overview of the intent of the model. If there is detailed information on use cases, push that to a separate "Use Cases" section.

**NOTES:** 
* All model documents MUST have an introduction.
* Information on the project, initiative, or organization for which the profile was created SHOULD be included.

Example:

```markdown
## Introduction

This model describes the use of Widgets, the class of objects that includes
jawns, thingamabobs, doodads, and sprockets, in the context of the
[Pacifica Complex Doodad Markup](http://example.org/pcdm/interop) interoperability project. 

**NOTES:**

* Widgets SHOULD NOT be used to model Frippery. 
```

## Use Cases

An itemized grouping or list of use cases that the model is intended to support. 

**NOTES**:

* When adding detailed use cases, provide subheadings for each use case.

Example:

```markdown
## Use Cases

* Documenting gadgets around your repository, and how Agents use them.
* The Internet of Things
```

## Model

Documentation on the properties and classes used in the model or profile.

**NOTES**: 
* The documentation SHOULD include a drawing of the model.

### Identified classes and properties

All relevant classes and predicates should appear as subsections under the Model section.

**NOTES:** 
* The documentation MUST include an itemized list of the most relevant classes to the model.
    * If a given documented class is a subclass of another class, it SHOULD be identified as such. 
    * Documentation for a subclass of a given class MAY skip including predicate definitions unless their recommendation varies from the subclass's superclass.
    * If a class definition defines a new class (i.e., rather than using a class from an existing ontology), the documentation for that class MAY include a brief example implementation.
    * If an implementation is provided, it MUST be provided in Turtle.
    * The documentation for a given class MAY include any entailment information for additional context based on the use of specific predicates associated with an instance of that class. It is intended that this entailment information is primarily for human understanding of the model or profile.
* The documentation MAY include an itemized list of predicates for each documented class.
    * If including a list of itemized predicates for a class, the list SHOULD contain those properties defined as MUST and SHOULD for instances of the identified classes.
    * The documentation MAY include predicates defined as MAY for those instances.
    * The documentation for each predicate MAY include obligation information for each predicate
    * If an expected type value is given for a predicate, a class identifier MUST be understood as referencing an instance of the class. If that referenced class is documented in the model, its name should be linked to the relevant model document. 
    * If the expected value of a given predicate is a class itself, it MUST be identified using the text `(class)`.

Example:

```markdown
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

```

## Usage

Include here documentation of how to use instances of the classes defined in a profile, such as defining new instances, subclasses, etc., and how to refer to instances. 

**NOTES:**
* Including a Usage section is RECOMMENDED. 
* The Usage section SHOULD contain a subsection on defining instances. Within that subsection, information on how to define new subclasses of that model SHOULD be provided if subclasses can be defined. 
* The Usage section SHOULD contain a subsection on referring to instances from instances of other classes in a related model. The subsection MAY included links to other documentation for other models if appropriate.
* The Usage section MAY contain a further subsection on implementation notes, e.g. for information on LDP projection.

Example:

```markdown
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

```

