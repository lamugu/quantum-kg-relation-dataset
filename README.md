# Quantum Computing Knowledge Graph Relation Dataset

A sentence-level relation extraction dataset for quantum computing, built from
759 peer-reviewed papers.

## Overview

| | |
|---|---|
| Papers | 759 |
| Triples | 17,280 |
| Relation types | 9 |
| Entities | 15,262 |
| Entity taxonomy | 8 categories × 64 subcategories |
| Training split | 19,844 / 2,871 / 2,635 (train/dev/test) |

## Task

Given a sentence and two entities occurring in it, classify the semantic
relation between the entity pair into one of nine relation types, or
`NO_RELATION` when no relation is expressed.

## Relation Types

| Relation | Meaning | Example |
|---|---|---|
| `APPLIED_TO` | X is used as a method on Y | `quantum monte carlo method` → `quantum computer` |
| `PART_OF` | X is a component of Y | `qubit` → `quantum computer` |
| `LIMITED_BY` | X's capability is constrained by Y | `quantum computer` → `noise` |
| `BASED_ON` | X is built upon Y | `quantum algorithm` → `quantum mechanics` |
| `IMPLEMENTED_ON` | X is realised on platform Y | `Toffoli gate` → `superconducting qubit` |
| `ENABLES` | X makes Y possible | `quantum error correction` → `fault tolerance` |
| `COMPARES_WITH` | X and Y are compared | `adiabatic search` → `quantum-walk search` |
| `COMBINES_WITH` | X and Y are coupled or integrated | `resonator` → `qubit` |
| `MITIGATES` | X suppresses Y | `error correction` → `noise` |

## Files

```
triples.json           17,280 relation triples with source sentence and paper id
entity_taxonomy.json   Two-level entity taxonomy (8 categories, 64 subcategories)
re_dataset.json        Train/dev/test split for relation classification
stats.json             Aggregate statistics
```

### `triples.json`

```json
{
  "head": "quantum monte carlo method",
  "relation": "APPLIED_TO",
  "tail": "quantum computer",
  "sentence": "In this paper we apply a quantum Monte Carlo method ...",
  "paper": "WOS_000075073900007",
  "sent_id": "0012"
}
```

### `entity_taxonomy.json`

Note: the taxonomy contains all 15,262 entities that appear in multi-entity
sentences. Entities occurring in a single paper are kept to maximize recall;
low-frequency entries may include surface-form variants.

```json
{
  "DEVICE": {
    "qubit":   [{"name": "superconducting qubit", "papers": 35}, ...],
    "quantum gate": [{"name": "hadamard gate", "papers": 91}, ...]
  }
}
```

### `re_dataset.json`

```json
{
  "labels": ["APPLIED_TO", "PART_OF", ..., "NO_RELATION"],
  "train": [{"sentence": "...", "head": "...", "tail": "...",
             "relation": "APPLIED_TO", "paper": "...", "sent_id": "..."}],
  "dev": [...],
  "test": [...]
}
```

## Entity Taxonomy

| Category | Subcategories |
|---|---|
| DEVICE | qubit, quantum gate, quantum circuit, processor, memory and network, classical hardware, physical component, other |
| PLATFORM | superconducting, trapped ion, neutral atom, photonic and optical, spin and solid-state, architecture and hardware, cloud and software, other |
| ALGORITHM | search and arithmetic, linear algebra and simulation, variational and hybrid, machine learning, classical optimization and annealing, error correction and compilation, quantum walks and graph algorithms, other |
| TECHNIQUE | simulation and numerical methods, compilation and circuit optimization, control and pulse engineering, measurement and benchmarking, error mitigation and correction, machine learning and optimization, encoding and state preparation, other |
| QUANTITY | physical and hardware, fidelity/error/noise, resource and complexity, time and performance, probability and statistical, ML and optimization, entanglement and state measures, other |
| ERROR | noise channels, gate/control/readout, decoherence and relaxation, leakage and loss, systematic and calibration, algorithmic and numerical, hardware and fabrication, other |
| CONCEPT | quantum information and computation, quantum states and operators, mathematical structures, many-body and statistical physics, quantum field and fundamental physics, ML and optimization, chemistry and molecular systems, other |
| APPLICATION | optimization, chemistry/materials/biology, ML and AI, simulation and physics, communication/sensing/cryptography, data and signal processing, finance and logistics, other |

## Data Provenance

Each triple records the source paper identifier and the position of the
sentence within that paper, so every annotation can be traced back to its
original context. Papers are identified by their Web of Science accession
number.

Only single-sentence excerpts and the extracted triples are distributed here.
Full-text articles are not redistributed; readers should obtain them from the
original publisher.

## Citation

```bibtex
@dataset{quantum_kg_re_2026,
  title     = {Quantum Computing Knowledge Graph Relation Dataset},
  year      = {2026},
  note      = {17,280 relation triples from 759 papers}
}
```

## License

Data: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)
