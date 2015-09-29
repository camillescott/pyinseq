# pyinseq

# Description

Python package to map transposon insertion sequencing (INSeq) data in bacteria

# Installation

**Dependencies**
[bowtie](http://bowtie-bio.sourceforge.net/index.shtml) - Latest version tested here is bowtie 1.1.1.

**Download**
Download and open the zip file for the pyinseq package (or git clone).

**Config**
Edit the `config.py` file with the path to your bowtie installation and any other relevant changes.

# Running the software

In general, place all input files in the `pyinseq/` directory. Each time the software is run an experiment directory is created that contains the analysis files for that experiment.

`$ python2.7 pyinseq.py -i reads.fastq -s samples.txt -g genome.gb -e exp01`

`python2.7` - Python 2.7 required
`pyinseq.py` - main script
`-i` / `--input` - concatenated genbank file for all contigs for the genome
`-e` / `--experiment` - all results files will be created in the subfolder of this name
`-i` / `--input` - Illumina reads file in FASTQ format
`-s` / `--samples` - sample list where each line is the `sample_name`tab`barcode(4bp)`

Run with example data:

`$ python2.7 pyinseq.py -i example01.fastq -s example01.txt -g ES114v2.gb -e example01`

# Example data sets included

**example01 : Artificial data to test math with a limited dataset**
Genome: Vibrio fischeri ES114 genome (2 chromsomes, 1 plasmid).
Reads: [TEST DATA COMING SOON. HOPEFULLY TONIGHT]

# Current status

**Highest priority right now -- getting test data sets ready.**

# Project purpose

Reproduce the functionality in [Andy Goodman's INSeq Perl pipeline](http://www.nature.com/nprot/journal/v6/n12/extref/nprot.2011.417-S2.zip) (15 MB .zip download) in Python to serve as a platform for additional functionality for normalization, plotting, sample management, and data analysis.

Immediate next steps will include multiple quality checks on the run and distinguishing the directionality of the transposon for a new transposon being built.


# Implemented

1. Read in FASTQ files instead of SCARF. (Note that David Cronin implemented this previously for us in Perl but in a manner that is now yielding multiple errors.)
2. Demultiplex into separate files per barcode - will facilitate data deposition and analysis when samples from multiple experiments are run in the same Illumina run.
  - *This has since been removed from the main branch for speed but can be added back in as needed (perhaps with optimized software). It was not necessary to analyze samples from only a single run but will be necessary to analyze samples from separate runs.*
3. Run bowtie seemlessly from within the software instead of requiring complicated index setup. Improves upon the previous software by reading a GenBank file, generating appropriately names files for Bowtie, calling bowtie-build to build indexes, and then calling bowtie for mapping. Additionally the .ftt files generated mimic the .ptt file format but additionally include RNA genes.
4. Normalization. Do CPM normalization to mimic previous analysis. [**check math here**]
4. Map number of hits per gene.
5. Summarize analysis results in a single table (for all chromosomes/plasmids; and for all samples under analysis).

# Next steps/wish list

5. Add back in demultiplexing and general method to organize samples in folders.
6. Ability to analyze Left & Right transposon ends separately.
  - Some code for this is already in to note L/R side on the identifier line but it has not been used.
7. Count TA sites per gene and normalize gene size per number of TA sites.
7. LOESS normalization to correct for more hits at origin and fewer hits at terminus.
8. Statistical analysis of results (method TBD; consider DESeq2 and other RNA-seq methods).
9. Plotting of results (specific plots TBD); likely an analysis of essential and conditionally essential genes. Consider assigning samples.
10. Detailed reporting and logging (e.g., fraction of reads that mapped successfully; variation from other samples))
11. Overall optimization

See the [Roadmap file](roadmap.md) for info on specific items to be implemented, including bugs in this version.

# License

BSD license as detailed in the [license file](LICENSE.md).
