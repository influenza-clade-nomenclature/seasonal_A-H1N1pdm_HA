# Clade and subclade nomenclature for the HA segment of seasonal A/H1N1pdm influenza viruses

This repository defines clades and subclades of the hemagglutinin segment of seasonal A/H1N1pdm influenza viruses.
These clades don't necessarily correspond to groups of viruses with distinct phenotypes but are meant to facilitate discussion of viral genetic diversity.
In particular subclades are used to capture the frequency dynamics of co-circulating viral variants that often don't have distinct properties.


## Designations

Each subclade is defined by a machine readable `yaml` file in the subdirectory `subclades`.
The yaml-files have the following structure:
```
name: C.1
unaliased_name: A.2.1
parent: C
representatives: []
defining_mutations:
- locus: HA1
  position: 185
  state: T
- locus: HA1
  position: 188
  state: E
- locus: HA1
  position: 53
  state: Q
- locus: HA1
  position: 307
  state: R
clade: 5a.2a
```
The field `clade` is set to `none` when no clade corresponds to the branch demarcating the subclade.

The defining mutations are relative using nucleotide and HA coordinates defined in
```
##gff-version 3
##sequence-region CY121680.1 1 1752
CY121680.1      feature mat_peptide    21      71      .       +       .       name="SigPep"
CY121680.1      feature mat_peptide    72      1052    .       +       .       name="HA1"
CY121680.1      feature mat_peptide    1053    1718    .       +       .       name="HA2"
```
Note that these defining mutations are not exhaustive. They represent a genotypic constellation sufficient to distinguish the clade from its parent.

## [Subclade summary](.auto-generated/subclades.md)

## [Clade--Subclade correspondence](.auto-generated/subclades.md#clade----subclade-correspondence)

## Subclade short names (aliases)
The subclade names are designed with a systematic way to shorten their names inspired by the pango-lineage system for SARS-CoV-2.
The initial part of the hierarchical names can be collapsed into a single letter (and possibly eventually double letters).
These aliases are defined in [config/aliases.json](config/aliases.json).


## Configuration
Parameters and mutation weights for the automated subclade suggestion algorithm can be found in the directory `config`.

## Update auto-generated files
After adding new clades, run the following commands to update the files generated from the individual yamls.
```
# generate the markdown summary of the clade definitions
python ../helper-scripts/generate_markdown_summary.py --input-dir subclades --lineage h1n1pdm --segment ha

# generate the tsv file with clade-defining info that can be used to annotate clades in augur
python ../helper-scripts/construct_tsv.py --input-dir subclades --output-tsv .auto-generated/subclades.tsv
python ../helper-scripts/construct_tsv.py --input-dir subclades subclade-proposals --output-tsv .auto-generated/subclade-proposals.tsv
python ../helper-scripts/construct_tsv.py --input-dir clades --aux-input-dir subclades --flat-output --use-short-name --output-tsv .auto-generated/clades.tsv
python ../helper-scripts/construct_tsv.py --input-dir clades --aux-input-dir subclades --flat-output --output-tsv .auto-generated/clades-long.tsv
# To add the result to the repo, do:

git add .auto-generated/subclades.tsv .auto-generated/subclade-proposals.tsv .auto-generated/clades.tsv .auto-generated/clades-long.tsv .auto-generated/subclades.md
git commit -m "update auto-generated files"
```

