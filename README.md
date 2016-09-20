[![Build Status](https://travis-ci.org/cmungall/environmental-conditions.svg?branch=master)](https://travis-ci.org/cmungall/environmental-conditions)
[![DOI](https://zenodo.org/badge/13996/cmungall/environmental-conditions.svg)](https://zenodo.org/badge/latestdoi/13996/cmungall/environmental-conditions)

## Environmental conditions, treatments and exposures ontology (ECTO)

The purpose of this ontology is to create compositional classes that
assemble existing OBO ontologies such as ExO, CHEBI and ENVO to make
ready-made precomposed classes for use in describing:

 * experimental treatments of plants and model organisms (e.g. modification of diet, lighting levels, temperature)
 * exposures of humans or any other organisms to stressors through a variety of routes, for purposes of public health, environmental monitoring etc
 * stimuli, natural and experimental
 * any kind of environmental condition or change in condition that can be experienced by an organism or population of organisms on earth

The scope is very general and can include for example plant treatment regimens, as well as human clinical exposures (although these may better be handled by a more specialized ontology)

An example of a class (in manchester syntax) is:

```
Class: ECTO:0000977
 Annotations: rdfs:label "exposure to ultrafine respirable suspended particulate matter via inhalation"
 Annotations: IAO:0000115 "A exposure event involving the interaction of an exposure receptor to ultrafine respirable suspended particulate matter via inhalation."
 Annotations: oio:hasExactSynonym "ultrafine respirable suspended particulate matter exposure, via inhalation"
 EquivalentTo: ExO:0000002 and RO:0002233 some ENVO:01000416 and BFO_0000050 some ExO:0000057 ## 'exposure event' and 'has input' some ultrafine respirable suspended particulate matter and 'part of' some inhalation
```

## Quick Start

There is no public browser yet. Use one of the following files:

 * [subsets/ecto-basic.obo](subsets/ecto-basic.obo) - for OBO-Edit users
 * [ecto.owl](ecto.owl) - open in Protege5

Note to open the OWL in Protege you will need to check out the repo so
that the catalog can be used.

### Relationships to other ontologies

Ontologies used in composition (largely orthogonal):

 * ExO - used as the upper ontology, for based classes such as 'exposure', different routes such as 'ingestion'
 * CHEBI - use for both entities and roles
 * ENVO - environmental materials, processes
 * NPO - radiation
 * RO - relations
 * PATO - qualities
 * UBERON - tissue types (not used yet)
 * NCIT - activities such as smoking
 * SDGIO - social entities
 * PCO - population attributes (e.g. overcrowding)

Similar ontologies (overlapping/non-orthogonal)

 * ZECO - zebrafish specific conditions
 * PECO - pombase specific conditions
 * EO - plant-specific environmental conditions and treatments
 * GO - `response to X` subset shadows many classes here
 * SNOMED - has an exposure subset
 * NCIT - has an exposure subset?
 * XCO - experimental conditions (mammal-centric?)
 * Wikidata - subclasses of hazard (Q1132455)

See below for the merge experiment with these ontologies.

We aim to reuse existing open ontologies as far as possible; for orthogonal ontologies, this is via axiomatization.

Note on ENVO: it may seem that ENVO is an overlapping/non-orthogonal ontology, but following our design patterns here this should be considered orthogonal; analogous to the relationship between an anatomical ontology and a variant/aberrant phenotype ontology.

Another new ontology to note is the UNEP Sustainable Development Goals ontology -- https://github.com/SDG-InterfaceOntology/sdgio/ -- this is being built in a modular fashion using ENVO and is seeding the creation of many useful social classes we will need, e.g. poverty, access to resources, etc.


### Releases

Release files are in top level

 * [obo](ecto.obo)
 * [owl](ecto.owl)

Note: these are only for testing so far, not stable! These should not be considered real releases.

The proposed ID space is very tentative

### Modeling

The model we are using is aligned with the environmental conditions
model in PhenoPackets. We attempt to follow ExO where possible.

We treat exposures as events; in ontological terms, they are types of
`occurrents`. Specifically, they are interactions between a `receptor`
(typically an organism, but could be a population of organisms) and a
`stressor` (an agent or process that has a potential effect on the
receptor). The stressor may interact with the organism through some
kind of environmental medium (e.g. air, water, soil), and may enter
via some route (e.g. permeating the skin or analogous barrier).

In some cases the route may be indirect: passive smoking or drug use
by a mother during pregnancy.

This model permits a variety of pre-composed classes. We defined and
generate these using Dead Simple OWL Design Patterns (DOSDPs)

See [src/patterns](src/patterns) for the list of patterns in use.

The basic idea is that a term like 'increased exposure to arsenic
through ingestion/diet' can be composed using classes from ontologies
such as ExO and CHEBI. We can see this as filling in slots in our
datamodel.

### Annotation Guide

Broadly speaking, this ontology is designed to support both pre and
post composed use cases.

With the pre-composed approach, the curator uses a "ready-made" ECTO
class expressing the combination of values required for different
slots.

With the post-composed approach, ECTO can largely be disposed of, and
instead the description is assembled by the curator by filling in the
required slots like 'stressor'.

The two approaches are compatible. Post-composed descriptions can be
automatically classified against the pre-composed ECTO. Similarly any
description that uses ECTO can be unwound (or 'unfolded') to a
pre-composed description, using the OWL equivalence axioms in the
ontology.

### Ontology Source

Most of the ontology is stored as CSVs in [src/ontology/modules](src/ontology/modules)

See the Makefile for how the ontology is compiled from CSV modules.

See the .omn files for a human-readable set of descriptions

See the README-editors.md file in the src/ontology directory for
instructions on how to edit, maintain or release the ontology.

### Merge Experiment

See [src/mappings](src/mappings) for an exploration of merging multiple exposure ontologies using kboom

The intent is not to use this ontology: rather to help gap fill and understand what is out there.


