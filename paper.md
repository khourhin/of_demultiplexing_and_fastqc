---
title: "Of demultiplexing and quality control"
tags:
  - snakemake
  - Illumina
  - fastqc
  - demultiplexing
  - singularity
authors:
 - name: Etienne Kornobis
   affiliation: "1,2"
 - name: Laure Lemee
   affiliation: "2"
 - name: Thomas Cokelaer
   orcid: 0000-0001-6286-1138
   affiliation: "1,2"
affiliations:
 - name: "Hub de Bioinformatique et Biostatistique – Département Biologie Computationnelle, Institut Pasteur, USR 3756 CNRS, Paris, France"
   index: 1
 - name: "Plate-forme Technologique Biomics – Centre de Ressources et Recherches Technologiques (C2RT), Institut Pasteur, Paris, France"
   index: 2



date: 2 August 2020
bibliography: paper.bib
---

# Overview
The field of genomics has reached a mature stage where complete human sequencing
can be performed routinely. The recent pendemic of the SARS-CoV virus has also shown
the power of sequencing: in a few months, thousands of genomes have
been sequenced and evolution of the virus could be studied as it spred the
world. This is achievable thanks to major advances in sequencing technologies in
the last few decades [@Goodwin2016] but also the emergence of bioinformatics tools and
pipelines that are more and more accessible and open to the scientific
community. Sequencing technologies currently span short and long-read technologies. The first one is mostly based on the Illumina Sequencers while the second are based on Pacbio and Nanopore technologies. Irrespective of the technology used, the data useful for subsequent analysis is in the form of FastQ files. Surprinsingly, those files are text-files storing the sequences that have been generated together with their quality at each position. The simplicity of such format led to a plethora or more or less complex analysis tools used in the field of bioinformatics.

The short-read technology is currently led by Illumina; amongst the Illumina sequencers a few of
them (e.g. NextSeq) do not provide the FastQ files automatically. Instead, raw data are provided.
Therefore, a so-called base-calling is required before any further analysis. This is achieved with a
tool provided by Illumina named **blc2fastq** [@bcl2fastq], which will be discussed
hereafter. Whether you generate the FastQ files or already have them, the next step consists in
checking the quality of the sequences.

Most research and production facilities that are involved in Sequencing
perform quality control (QC) of the different samples using the FastQC tool [@Andrews2010].
QCs may not be done by the facility or one may receive only the FastQ files from
their collaborators.


Most production facilities already have their own pipeline with FastQC or
home-made fastqc tools. Yet, most researchers discovering genomics (students,
postdoc, etc) would face common issues: where to find the tools, how to
demultiplex the data (if needed), how to get simple plot that summarizes the
fastqc results of tens or hundreds of samples, what are the main sanity checks
to perform, how to run the tools on a cluster, etc

Here we present a pair of Snakemake [@Koster2012] pipelines available in the
sequana project [@Cokelaer2017]. The first one is caled **sequana\_fastqc** and
the second one **sequana\_demultiplex**. They are used in production within
a sequencing platform and can be used by non-expert users. They have the same
API and can be run either locally or on a SLURM cluster. 

# Statement of need

The pipelines are designed to be used by any persons involved in Sequencing
platform. It is used in production by engineers, lab personnel, researchers. The
main interest is that it provide fastqc for each samples, summarizing the
results with MultiQC plugins, and provide a single HTML entry point. 


# Installation, usage, reproducibilty

One of the key feature of the two pipelines presented here abobe is to allow an
easy an quick deployment of the tools, especially after bug fixes or new
features implementation. 

The first step consists in installation the Sequana library. This can be achieve
in two ways. First, since Sequana is a Python library, one can simply install it
using the standard procedure. All releases are available on pypi.org, therefore
the main library can be installed using 

```shell
   pip install sequana
```

Second, since sequana is available on Bioconda [@Gruning2018]


    sequana_fastqc
    cd fastqc
    sh fastqc.sh


Example on a cluster



**Sequana** is an open source project (https://github.com/sequana/sequana). It is developed with the aim
of simplifying the development of new tools (for developers) and the deployment of the pipelines (for users).
The extended documentation (http://sequana.readthedocs.org) and test suite (on [Travis.org](http://travis-ci.org)) provide a high-quality
software that is routinely tested. **Sequana** is now available on bioconda making the installation easier and faster by taking care of the dependencies (e.g., samtools, bwa, or Python libraries).

Finally, for end-users, we also developed a Graphical interface called **Sequanix** [@sequanix:2017] developed with the PyQt framework (see left panel of the image here below). **Sequanix** standalone exposes all **Sequana** pipelines (Snakemake pipelines) within an easy-to-use interface. Within the graphical interface, the configuration file used by Snakemake are automatically loaded and can be edited by end-users with dedicated widgets. We made the interface generic enough that not only Sequana pipelines can be run interactively but also any Snakemake pipelines.



![caption example.\label{fig:barcodebad}](barcodes_hiseq_bad_lane)

![caption example.\label{fig:barcodegood}](barcodes_hiseq_good.png)

![](summary_hiseq_bad_lane.png)

![](summary_hiseq_good.png)


reproducibility: sequana is on bioconda, the pipelines are on pypi with
release version. The third-party tools are on bioconda (fastqc) and within a
singularity (fastqc and bcl2fastq).

Info general fastqc and demultiplexing:


[Interpreation fastqc/multiqc](biomics.pasteur.fr/drylab/of_demultiplexing_and_fastqc.html)
[demultiplexing](biomics.pasteur.fr/drylab/demultiplexing.html)
[sample sheet](biomics.pasteur.fr/drylab/samplesheet.html)



# Acknowledgments

We acknowledge contributions from ....


# References



