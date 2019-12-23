<p align="center">
  <img src="img/pbmarkdup-logo.png" alt="CCS logo" width="200px"/>
</p>
<h1 align="center">pbmarkdup</h1>
<p align="center">Mark duplicate reads from PacBio sequencing of an amplified library</p>

***

_pbmarkdup_ takes one or multiple sequencing chips of an amplified libray as
HiFi reads and marks or removes duplicates.

## Availability
Latest `pbmarkdup` can be installed via bioconda package `pbmarkdup`.

Please refer to our [official pbbioconda page](https://github.com/PacificBiosciences/pbbioconda)
for information on Installation, Support, License, Copyright, and Disclaimer.

## Latest Version
Version **0.2.0**: [Full changelog here](#changelog)

## Execution
**Input**: HiFi reads from one or multiples movies in PacBio BAM (`.ccs.bam`),
PacBio dataset (`.consensusreadset.bam`), file of file names (`.fofn`),
FASTQ (optionally gzipped), or FASTA (optionally gzipped) format.

**Output**: HiFi reads with duplicates marked in a format inferred from the
file extension: HiFi BAM (`.bam`); FASTQ (`.fastq`); FASTQ (`.fasta`);
bgzipped FASTQ (`.fastq.gz`); bgzipped FASTA (`.fasta.gz`); or SMRT Link XML
(`.consensusreadset.xml`) which also generates a corresponding BAM file.

Run on a full movie:

    pbmarkdup movie.ccs.bam output.bam

Run on multiple movies

    pbmarkdup movie1.fasta movie2.fasta output.fasta

Run on multiple movies and output duplicates in separate file

    pbmarkdup movie1.ccs.bam movie2.fastq uniq.fastq --dup-file dups.fasta

## FAQ

### Why are input files parsed twice?
In order to keep memory footprint to a minimum, we trade reading input files
twice instead of storing everything in memory. The goal was to support
processing multiple movies with a standard server.

### What input / output combinations are allowed

Input as rows, outputs as columns:

| IN/OUT  | BAM | DATASET | FASTQ | FASTA |
| ------- | :-: | :-----: | :---: | :---: |
| BAM     | x   | x       | x     | x     |
| DATASET | x   | x       | x     | x     |
| FASTQ   |     |         | x     | x     |
| FASTA   |     |         |       | x     |

Allowed combination example:

    pbmarkdup movie1.ccs.bam movie2.fastq movie3.fasta out.fasta

Forbidden combination example:

    pbmarkdup movie2.fastq movie3.fasta out.fastq

### Is there a progress report?
Yes. With `--log-level INFO`, _pbmarkdup_ provides status to `stderr`.

## Licenses
PacBio® tool _pbmarkdup_, distributed via Bioconda, is licensed under
[BSD-3-Clause-Clear](https://spdx.org/licenses/BSD-3-Clause-Clear.html).

## Changelog

 * **0.2.0**:
   * Initial release

## DISCLAIMER
THIS WEBSITE AND CONTENT AND ALL SITE-RELATED SERVICES, INCLUDING ANY DATA, ARE PROVIDED "AS IS," WITH ALL FAULTS, WITH NO REPRESENTATIONS OR WARRANTIES OF ANY KIND, EITHER EXPRESS OR IMPLIED, INCLUDING, BUT NOT LIMITED TO, ANY WARRANTIES OF MERCHANTABILITY, SATISFACTORY QUALITY, NON-INFRINGEMENT OR FITNESS FOR A PARTICULAR PURPOSE. YOU ASSUME TOTAL RESPONSIBILITY AND RISK FOR YOUR USE OF THIS SITE, ALL SITE-RELATED SERVICES, AND ANY THIRD PARTY WEBSITES OR APPLICATIONS. NO ORAL OR WRITTEN INFORMATION OR ADVICE SHALL CREATE A WARRANTY OF ANY KIND. ANY REFERENCES TO SPECIFIC PRODUCTS OR SERVICES ON THE WEBSITES DO NOT CONSTITUTE OR IMPLY A RECOMMENDATION OR ENDORSEMENT BY PACIFIC BIOSCIENCES.
