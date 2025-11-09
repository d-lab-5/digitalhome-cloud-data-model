# DigitalHome.Cloud Ontology

This folder contains the **core ontology definition** of the [DigitalHome.Cloud](https://digitalhome.cloud) platform —  
the semantic foundation describing real estate, spaces, equipment, and their relationships.

The ontology defines the **vocabulary**, **class hierarchy**, and **object/data properties** used across all DigitalHome.Cloud systems,  
ensuring interoperability between design tools, simulation environments, and runtime data services.

---

## Contents

| File | Purpose |
|------|----------|
| **`dhc-core.schema.ttl`** | The main ontology (schema) defining all core DigitalHome.Cloud concepts and relations, expressed in Turtle (`.ttl`) syntax. |
| **`dhc-brick-alignment.ttl`** | Semantic alignment of DigitalHome.Cloud classes and properties to [Brick Schema](https://brickschema.org/), ensuring compatibility with building automation and energy standards. |
| **`context.jsonld`** | JSON-LD context file providing compact JSON mappings for runtime systems. It allows APIs and applications to serialize ontology-based data in a human-readable JSON form. |
| **`README.md`** | This documentation file describing ontology content, design principles, and usage. |

---

## Design Principles

1. **Human-centric** – Technology supports people and sustainable living.
2. **Modular** – Ontology is divided into domains (core, safety, energy, etc.) for flexibility.
3. **Compatible** – Aligned with open standards like BRICK, RealEstateCore, and IFC.
4. **Versioned** – Each release (e.g., `model-v0.3.0`) is immutable and published as JSON-LD for reference and validation.
5. **Machine-processable** – Fully compliant with OWL/RDF/SHACL semantics for validation and reasoning.

---

## Design-time vs Runtime

| Stage | Format | Location | Description |
|--------|---------|-----------|-------------|
| **Design-time** | `.ttl` (Turtle) | GitHub (`ontology/`) | Human-editable ontology source used for schema development and validation. |
| **Runtime** | `.jsonld` (JSON-LD) | S3 public bucket (`s3://digitalhome-cloud-public/ontology/`) | Machine-readable, lightweight serialization used by Amplify APIs and other DigitalHome.Cloud services. |

Conversion and validation are automated in the CI workflow.  
Each tagged release automatically publishes validated JSON-LD versions to S3 and GitHub Releases.

---

## How It Fits Together

```mermaid
graph TD
    A[d hc-core.schema.ttl<br>Ontology classes & properties] --> B[dhc-brick-alignment.ttl<br>Mapping to Brick Schema]
    A --> C[context.jsonld<br>Runtime JSON-LD context]
    B --> D[shapes/*.ttl<br>SHACL validation packs (e.g. NF C 15-100)]
    C --> E[S3 runtime store<br>Public JSON-LD schema]
