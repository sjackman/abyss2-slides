---
pagetitle: "ABySS 2.0: Resource-efficient assembly of large genomes using a Bloom filter"
author: "Shaun D Jackman"
date: "2018-04-19"
history: true
slideNumber: true
---

## ABySS 2.0

### Resource-efficient assembly of large genomes using a Bloom filter

**Shaun D Jackman** [\@sjackman][]

Benjamin P Vandervalk, Hamid Mohamadi, Justin Chu, Sarah Yeo, S Austin Hammond, Golnaz Jahesh, Hamza Khan, Lauren Coombe, Rene L Warren, Inanc Birol

| RECOMB-Seq 2018-04-19
| <https://sjackman.ca/abyss2-slides>
| Funded by Genome Canada &middot; Genome BC &middot; NIH &middot; NSERC
| [![Creative Commons Attribution License](images/cc-by.png)][cc-by]

[\@sjackman]: http://twitter.com/sjackman
[cc-by]: http://creativecommons.org/licenses/by/4.0/

## Shaun Jackman

| [Birol Bioinformatics Technology Lab](http://www.birollab.ca)
| [BC Cancer Genome Sciences Centre](http://bcgsc.ca) &middot; Vancouver, Canada
| [\@sjackman][] &middot; [github.com/sjackman](https://github.com/sjackman) &middot; [sjackman.ca](http://sjackman.ca)
| ![Shaun's head shot](images/sjackman.jpg)

## Short Read Genome Assembly

| ABySS 1.0 (2009) was the first to assemble
| a human genome from short reads (42 bp!)

[![ABySS 1.0 paper](images/abyss-paper.png)](https://doi.org/10.1101/gr.089532.108)

<http://bit.ly/abyss1-paper> &middot; [doi:btnjx2](http://doi.org/btnjx2)

## ABySS 1.0

- de Bruijn graph assembler
- Stored *k*-mers in a hash table
- Distributed the hash table over many machines
- Used MPI to aggregate sufficient memory
- Assembles large genomes

## ABySS 1.0

|             | Human    | Spruce
|-------------|----------|----------
| Genome size | 3 Gbp    | 20 Gbp
| RAM         | 418 GB   | 4.3 TB
| CPU cores   | 64       | 1,380
| Wall time   | 14 hours | 12 days
| Year        | 2017     | 2013
| Short DOI   | [doi:f9x8qp](https://doi.org/f9x8qp) | [doi:f4zzrr](https://doi.org/f4zzrr)

## Challenges

- High memory usage
- Interprocess communication is slow
- Intermachine communication is really slow

## Solution

- | A memory-efficient data structure
  | reduces memory usage
- | Fitting entire graph in a single machine
  | eliminates intermachine communication
- | OpenMP rather than MPI
  | eliminates interprocess communication

## ABySS 2.0

| ABySS 2.0 (2017) reduces the memory
| usage of ABySS by ten fold.

[![ABySS 2.0 paper](images/abyss2-paper.png)](https://doi.org/10.1101/gr.214346.116)

<http://bit.ly/abyss2-paper> &middot; [doi:f9x8qp](https://doi.org/f9x8qp)

----------------------------------------

![Memory efficient de Bruijn graph using a Bloom filter<br>Memory usage is independent of *k*](images/data-structures.png){height=550px}

----------------------------------------

![Navigating a Bloom filter de Bruijn graph<br>Introduced by Minia (Chikhi *et al.* 2012)](images/bloom-dbg-nav.png)

----------------------------------------

![Sequencing errors and Bloom filter false positives](images/error-correction.png)

----------------------------------------

![Solid reads are extended using the Bloom filter de Bruijn graph to assemble unitigs](images/abyss2-read-extension.png){.plain}

----------------------------------------

![ABySS 2.0 reduces memory usage by 10 fold vs ABySS 1.0 for human genome assembly (GIAB HG004 NA24143)](images/abyss2.mem-vs-time.png){height=550px}

## Spruce genome assemblies

| ABySS              | 1.3.5    | 2.0.0
|--------------------|----------|----------
| Spruce species     | Interior | Sitka
| Machines           | 115      | 1
| RAM (GB)           | 4,300    | 500
| CPU cores          | 1,380    | 64
| CPU time\* (years) | 6.0      | 3.2
| Wall time\* (days) | 1.6      | 18
| Year               | 2013     | 2017
| Short DOI          | [doi:f4zzrr](https://doi.org/f4zzrr) | NA

<small>\* Time of unitig assembly without scaffolding</small>

----------------------------------------

![Contiguity and correctness are comparable](images/scaffold-NGA50-to-NG50.png){height=600px}

----------------------------------------

![41.9 Mbp NG50 scaffolded with BioNano optical mapping](images/ideogram.png){height=600px}

## Conclusion

- | ABySS 2.0 reduces memory usage by 10 fold
  | from 418 GB for ABySS 1.0
  | to 34 GB for ABySS 2.0
  | for a human genome assembly
- | High-throughput short-read sequencing
  | combined with large molecule scaffolding
  | such as 10X Genomics, BioNano, Hi-C
  | permits cost effective assembly of large genomes

fin
================================================================================

## Shaun Jackman

[\@sjackman][] &middot; [github.com/sjackman](https://github.com/sjackman) &middot; [sjackman.ca](http://sjackman.ca)

Benjamin P Vandervalk, Hamid Mohamadi, Justin Chu, Sarah Yeo, S Austin Hammond, Golnaz Jahesh, Hamza Khan, Lauren Coombe, Rene L Warren, Inanc Birol

| **ABySS 2.0**
| <https://github.com/bcgsc/abyss>
| **ABySS 2.0 Paper**
| <http://bit.ly/abyss2-paper> &middot; [doi:f9x8qp](https://doi.org/f9x8qp)
| **Slides**
| <http://sjackman.ca/abyss2-slides>
| <https://github.com/sjackman/abyss2-slides>
| Funded by Genome Canada &middot; Genome BC &middot; NIH &middot; NSERC

Supplemental Slides
================================================================================

----------------------------------------

![ABySS 2.0 assembly algorithm](images/assembly-algorithm.png){.plain}

----------------------------------------

![Assembler comparison](images/assembler-comparison.png){height=600px}

----------------------------------------

![Genome coverage and identity](images/coverage-identity.png)

----------------------------------------

![Jupiter plot of scaffolds mapped to the reference genome](images/abyss2_bionano_arcs.png){height=600px}
