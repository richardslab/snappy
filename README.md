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

Snappy takes as it's first argument one of the following subcommands:

`match`: Matches rsids by exact lookup.
`update`: Updates unmatched rsids to latest rsids from dbSNP.
`match`: Run match again to see if updates found additional exact matches.
`position`: Match remaining unmatched rsids in query to SNPs in target that are reported by position (eg 1_123456.* or 1:123456.*).
`proxy`: Match remaining umatched rsids to target rdis using LD to 1000 Genomes EUR, selecting the highest r2, if multiple, then the nearest.

Here is an example usage scenario:

    snappy init query.txt target.txt | snappy match | snappy update | snappy match | snappy position | snappy proxy  > snappy.out

Snappy can pass output to itself using unix pipe (|), so you can run one or more of the above analyses in the order you prefer.

The first step is always snappy init query.txt target.txt, where query.txt is a file with rsids, usually lead variants from a GWAS (example MR exposure GWAS).

The target.txt file is a 2nd list of rsids, usually the complete list of rsids from a 2nd GWAS (example MR outcome GWAS).

Example output:

    QueryID     TargetId         r2        Dist   MatchType
    rs10030035  rs10030035       1         0      match
    rs10030217  rs10030217       1         0      match
    rs10033900  rs10033900       1         0      match
    rs10038416  5_147593231_A_G  1         0      position
    rs1005283   rs1005283        1         0      match
    rs1007914   rs2093989        0.979852  12322  proxy




