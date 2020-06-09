# Snappy: A flexible SNP proxy finder

## Features

* Find SNP proxies using multiple methods: exact match, position lookup, and linkage disequilibrium.
* Updates dbSNP identifiers.
* Compatible with Unix/Linux pipe operator (`|`).

## Limitations

* Does not resolve duplicate dbSNP identifiers, such as those on the sex chromosomes.
* Analysis is restricted to autosomal chromosomes.
* Default human genome build is hg19 (can be modified in source).

## Requirements

* Unix/Linux tool chain: `grep`, `awk`,`bash`, etc.
* `sqlite3`.
* `curl` & `wget`.
* `perl`.
* `plink` and genotype reference panel in PLINK binary format, one file per chromosome ([1-22].(bed|bim|fam).

## Installation

1. Make executable, `chmod +x snappy`.
2. Copy `snappy` script to program directory that is included in `$PATH`, eg. `/usr/local/bin` or `~/bin/`.
3. Build dbSNP database: `snappy build_dbsnp`. This step will take up to 3-5 hours to complete.

NOTE: If you move `snappy` to another location, move `snp150.db` (generated in step 3) to the same location.

## Usage

TBD