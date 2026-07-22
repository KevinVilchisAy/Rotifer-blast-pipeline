# Rotifer-blast-pipeline

# Rotifer Immunity Pipeline

A Python bioinformatics pipeline that automates **BLASTp** searches against a rotifer protein database, identifies homologous proteins, and extracts matching protein sequences for one or multiple immunity-related genes.

---

## Overview

This pipeline streamlines the process of comparing protein sequences against a rotifer reference database by automating the following workflow:

1. Perform a BLASTp search using one or more query protein sequences.
2. Identify matching rotifer protein IDs from the BLAST output.
3. Extract the corresponding protein sequences from the reference FASTA database.
4. Generate FASTA files for downstream bioinformatics analyses.

The pipeline supports processing either a single query sequence or an entire directory of query files.

---

## Features

- BLASTp search against a rotifer protein database
- Automatic extraction of homologous protein sequences
- Batch processing of multiple genes
- Supports `.fa`, `.fasta`, and `.txt` FASTA-formatted query files
- Configurable number of BLAST threads and E-value threshold
- Organized output for each processed gene

---

## Pipeline Workflow

```
Query Protein(s)
        │
        ▼
     BLASTp Search
        │
        ▼
 Identify Matching
 Rotifer Protein IDs
        │
        ▼
Extract Protein Sequences
 from Reference FASTA
        │
        ▼
  Output FASTA Files
```

---

## Requirements

- Python 3
- NCBI BLAST+ (blastp)
- A formatted BLAST protein database
- Rotifer reference FASTA file
- `extract_sequences.py`

Python standard libraries used:

- argparse
- subprocess
- os
- sys
- glob

---

## Configuration

Update the configuration variables near the top of the script if your file locations differ.

```python
BLASTP_BIN
ROTIFER_DB
ROTIFER_FASTA
EXTRACT_SCRIPT
```

---

## Usage

### Process a single query sequence

```bash
python3 pipeline_immunity_genes.py -q query.fa
```

---

### Process multiple query sequences

```bash
python3 pipeline_immunity_genes.py \
--query-dir my_genes \
--output-dir results
```

---

### Run in the background

```bash
nohup python3 pipeline_immunity_genes.py \
--query-dir my_genes \
--output-dir results &
```

---

## Input

The pipeline accepts FASTA-formatted protein sequences saved as:

- `.fa`
- `.fasta`
- `.txt`

Example:

```
my_genes/
├── AGO.fa
├── TLR.fa
├── DEFB.txt
└── CAT.fasta
```

---

## Output

For every input gene, the pipeline generates:

```
results/

AGO_ROT_BLAST.out
extracted_AGO.fasta

TLR_ROT_BLAST.out
extracted_TLR.fasta

DEFB_ROT_BLAST.out
extracted_DEFB.fasta
```

Where:

- `*_ROT_BLAST.out` contains the BLAST search results.
- `extracted_*.fasta` contains the homologous rotifer protein sequences.

---

## How It Works

For each query sequence, the pipeline performs the following steps:

1. Executes a BLASTp search against the rotifer protein database.
2. Extracts the unique matching rotifer sequence IDs.
3. Uses the extracted IDs to retrieve complete protein sequences from the reference FASTA database.
4. Writes the extracted sequences to FASTA files for downstream analyses.

---

## Author

Roxana Chavez & Kevin Ayala Vilchis

Undergraduate Research Project
University of Texas at El Paso (UTEP)

---

## License

This project is intended for academic and research use.
