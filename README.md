# **CADIn** - Chromosomal Amplification and Delition Inference
###### *Citation: Coqueiro-dos-Santos, A.*

#
### What means CADIn?
CADIn is a softwares free (open source) and developed to unix systems (e.i. linux) that permit to search allelic differences in NGS (next generation sequences) data. This tool estimate ploidy level  for each chromosomes in individuo. For this, it calculate the allelic frequency based in single nucleotide variants and, furthermore, analyse depth reads in regions annotated with good coverage, like: genes, CDSs, exon and so on.

### Dependences
- Perl
- BCFTools (version 1.9)
- BEDTools (2.26 or superior)
- SAMTools (version 1.9)
- R (version 3.4 or superior)

Perl Modules
- Statistics::R

## Installing dependencies

### Debian / Mint / Ubuntu
**BCFTools**
>sudo apt-get install bcftools

**BEDTools**
>sudo apt-get install bedtools

**SAMTools**
>sudo apt-get install samtools

**R**
>sudo apt-get install r-base

### CentOS / Fedora / Red Hat
**BEDTools**
>sudo yum install BEDTools

**R**
>sudo yum install R

###### *If not found run `'sudo yum install epel-release'` before*

### Othres (Via Terminal)
You can try install the softwares bcftools and samtools by command line, once the systems can have old versions or don't has it.
#### BCFTools and SAMTools (version 1.9)
**Main page:** `` htslib.org ``

**Links to softwares**
>[BCFTools v1.9](https://github.com/samtools/bcftools/releases/download/1.9/bcftools-1.9.tar.bz2)

>[Samtools v1.9](https://github.com/samtools/samtools/releases/download/1.9/samtools-1.9.tar.bz2)

**Install tools**

Download by terminal
```
wget <insert link here>
```
Decompress
```
tar -xvf *tools-1.9.tar.bz2
```
Configure and install
```
cd <directory>
./configure --prefix=/where/to/install
make
make install
```
Preparing to use
```
export PATH=/where/to/install/bin:$PATH
```

#### Othres softwares
**BEDTools**
**Main page:** `` bedtools.readthedocs.io ``
>[BEDTools v2.28](https://github.com/arq5x/bedtools2/releases/download/v2.28.0/bedtools-2.28.0.tar.gz)

**R**
**Main page:** `` r-project.org ``
>[R v3.6](https://cloud.r-project.org/src/base/R-3/R-3.6.1.tar.gz)

*Installing: `For this sofwares you use the same steps explained above (BCFTools and SAMTools).`*

#### Modules and Packages
**Statistics::R**

**Main page:** `` metacpan.org/pod/Statistics::R ``

Usually modules are automatically detected. However, if not you need to install from the terminal.
```
sudo cpan install Statistics::R
```
**R - Packages**

There are two packages (ggplot2 and outliers). Both are instaled from the CADIn. They can be installed before. For this, open the R (software).
```
install.packages("<insert package name here>")
```
## Working with CADIn
### Prepating
Making user-friendly
1. Makes executable
```
cd CADIn/
chmod +x ./CADIn
```
2. Easy acess
```
alias CADIn='/<path to CADIn>/./CADIn'
or
export PATH=/<CADIn directory>/:$PATH
```
*`You need specify the complete path to CADIn.`*
### Runing
To run is necessary 3 files.
- BAM format file or directory with BAM file(s).
- FASTA format file where reads were mapped used like reference for BAM file(s).
- GFF format file referent the reference genome.

**Basic command line**
```
CADIn -i FILE.bam -r REFERENCE.fasta -a ANNOTATION.gff
```
### Results
The standard output of the CADIn is divided in 4 folders.

- **genomecov/**
	- Read coverage at each position on chromosomes.

- **genescov/**
	- Read coverage in selected regions of the annotation file.

- **vcf/**
	- File in variante call format (VCF) with all single nucleotide variants found on chromosome(s).

- **statistical/**
	- *combineCoverage.csv*
		- Tabular file with coverage data. It has the coverage proportion of the annotated region and its depth.
	- *frequencySNPs.csv*
		- Frequency of the heterozygous single nucleotide variants by chromosome.
	- *normalized.Cov.csv*
		- Table with normalized depth values by grubs test.
	- *wilcox.Cov.csv*
		- Statistical informations of the wilcox tests. 
	- *coverage/*
		- Folder where are saved Boxplots pictures referente the aneuploids analysis for each sample and chromosome.
	- *frequency/*
		- Folder where are saved all Barplot graphics with frenquency count of the heterozygous single nucleotide variants.

### Arguments
```
--- Parameters ---------------------
	-i  BAM file(s).
	-r  Fasta file containing reference sequence.
	-a  GFF file containing annotation information.
--- Advanced Options ---------------
	-q  Filter input(s) by mapping quality [INT] (default -q 0).
	-f  Annotated region to be filtered ('gene', 'CDS', 'mRNA', 'tRNA', 'etc') (default -f gene).
	-s  Directory to save the temporary files (default -s /home/coqueiro//tmp).
	-t  Number of threads to SAMTOOLS run [INT] (default -t 1).
	-o  Name for your output files (default -o result_CADIn).
--- Type of analysis ---------------
	-v  Variant calling analysis (1), or not (0) (default -v 1).
	-d  Minimum number of reads to confirm each variant [INT] (default -d 5) (require '-v 1').
	-c  Genome/genes coverage analysis (1), or not (0) (default -c 1).
--- Statistical Parameters ---------
	-u  Determine if statistical analysis (1), or not (0), will be performed (default -u 1).
	-m  Calculate using mean (0) or median (1) [INT] (default -m 1).
	-g  Graphics generate with R: yes (1) or not (0) (default -g 1) (require '-u 1').
------------------------------------
```
## Citation
## Licence
>[GNU General Public License v3.0](https://github.com/coqueiro-dos-santos/CADIn/blob/master/LICENSE.txt)
## Author
Anderson Coqueiro-dos-Santos
E-mail: andersoncoqueiro8@gmail.com
Github: github.com/coqueiro-dos-santos
Mendeley: mendeley.com/profiles/anderson-coqueiro-dos-santos2
University: Federal University of Minas Gerais
Departament: Departamenty of Parasitology
