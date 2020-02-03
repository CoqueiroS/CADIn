# **CADIn** - Chromosomal Amplification and Deletion Inference
###### *Citation: Coqueiro-dos-Santos, A. Xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.*

#
### What means CADIn?
CADIn is a software free (open source) and developed to Unix systems (e.i. Linux) that permit to search allelic differences in NGS (next-generation sequences) data. This tool estimate ploidy level for each chromosome in sample. For this, it calculates the allelic frequency based in single nucleotide variants and, furthermore, analyze depth reads in regions annotated with good coverage as genes, CDSs, exon and so on.

## Dependences
- Perl
- BCFTools (version 1.7)
- SAMTools (version 1.7)
- R (version 3.4 or superior)

Perl Modules
- Statistics::R

## Installing dependencies

### Debian / Mint / Ubuntu
**BCFTools**
>sudo apt-get install bcftools

**SAMTools**
>sudo apt-get install samtools

**R**
>sudo apt-get install r-base

### CentOS / Fedora / Red Hat
**BCFTools**
>sudo dnf install bcftools

**SAMTools**
>sudo dnf install samtools

**R**
>sudo dnf install R
>or
>sudo yum install R

###### *If not found run `'sudo yum install epel-release'` before*

###### *The package manager `(yum)` used in this distros has SAMTools software, but an old version.*

###### *We recommend install BCFTools and SAMTools via terminal, `describe below`.*

### Others (Via Terminal)
You can try to install the software BCFTools and SAMTools by command line, once the systems can have old versions or don't has it.
#### BCFTools and SAMTools (version 1.9)
**Main page:** ``htslib.org``

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

**R**

**Main page:** `` r-project.org ``
>[R v3.6](https://cloud.r-project.org/src/base/R-3/R-3.6.1.tar.gz)

*Installing: `For this software, you use the same steps explained above (BCFTools and SAMTools).`*

#### Modules and Packages
**Statistics::R**

**Main page:** `` metacpan.org/pod/Statistics::R ``

Usually, modules are automatically detected. However, if not you need to install from the terminal.
```
sudo cpan install Statistics::R
```
**R - Packages**

There are two packages (`ggplot2` and `outliers`). Both are installed from the CADIn, but they can be installed before. For this, open the R (software).
```
install.packages("<insert package name here>")
```
## Working with CADIn
### Preparing
Making user-friendly
1. Makes executable
```
cd CADIn/
chmod +x ./CADIn
```
2. Easy access
```
alias CADIn='/<path to CADIn>/./CADIn'
or
export PATH=/<CADIn directory>/:$PATH
```
*`You need to specify the complete path to CADIn.`*
### Running
To run is necessary 3 files.
- BAM format file or directory with BAM file(s).
- FASTA format file where reads were mapped. File used as reference for BAM file(s).
- GFF format file referent the reference genome.

**Basic command-line**
```
CADIn -i FILE.bam -r REFERENCE.fasta -a ANNOTATION.gff
```

### Results
The standard output of the CADIn is divided in 4 folders.

- **genescov/**
	- Read coverage in selected regions of the annotation file.

- **vcf/**
	- File in variant call format (VCF) with all single-nucleotide variants found on chromosome(s).

- **statistical/**
	- *combineCoverage.csv*
		- Tabular file with coverage data. It has the coverage proportion of the annotated region and its depth.
	- *frequencySNPs.csv*
		- Frequency of the heterozygous single nucleotide variants by chromosome.
	- *normalized.Cov.csv*
		- Table with normalized depth values by Grubb's test.
	- *wilcoxon_rank.Cov.csv*
		- Statistical information of the Mann-Whitney-Wilcoxon tests.
	- *coverage/*
		- Folder where are saved Boxplots pictures referent the aneuploids analysis for each sample and chromosome.
	- *frequency/*
		- Folder where are saved all Barplot graphics with the frequency count of the heterozygous single nucleotide variants.

### Arguments
**General paramenters**
```
--- Parameters ---------------------
	-i  BAM file(s).
	-r  Fasta file containing reference sequence.
	-a  GFF file containing annotation information.
--- Advanced Options ---------------
	-q  Filter input(s) by mapping quality [INT] (default -q 30).
	-f  Annotated region to be filtered ('gene', 'CDS', 'mRNA', 'tRNA', 'etc') (default -f gene).
	-s  Directory to save the temporary files (default -s /tmp).
	-t  Number of threads to SAMTOOLS run [INT] (default -t 1).
	-o  Name for your output files (default -o result_CADIn).
--- Type of analysis ---------------
	-v  Variant calling analysis (1), or not (0) (default -v 1).
	-d  Minimum number of reads to confirm each variant [INT] (default -d 5) (require '-v 1').
	-k  Minimum SNP quality for each variant [INT] (default -k 10) (require '-v 1').
	-c  Genome/genes coverage analysis (1), or not (0) (default -c 1).
	-x  Minimum covered length accepted in regions for calculating genome coverage (default -x 50) (require '-c 1').
	-l  Minimum covered length accepted for the regions to be used for statistical analysis (default -l 50) (require '-c 1').
	-n  Minimum number of regions accepted to validate chromosome aneuploidy. Number checked after Grubbs test (default -n 5) (require '-c 1').
--- Statistical Parameters ---------
	-u  Determine if statistical analysis (1), or not (0), will be performed (default -u 1).
	-m  Calculate using mean (0) or median (1) [INT] (default -m 1).
	-g  Graphics generate with R: yes (1) or not (0) (default -g 1) (require '-u 1').
------------------------------------
```
**Main Input Files**

At least three files are needed for CADIn to work, BAM, FASTA and GFF files. The `-i` works with only one BAM files, but if specify a directory all BAM files are used to analysis. When the directory is used as input `-i` the software detects all files named as “.bam” in path. FASTA file `-r` is the same reference used in the mapping of the BAM data. Already GFF file `-a` need be correspondent to the reference (FASTA file), in other words, all identification (column 1) must be identical to sequence Fasta identification in reference file.

*Essential Arguments*
```
CADIn -i FILE.bam -r REFERENCE.fasta -a ANNOTATION.gff
```

**Mapping Quality**

The flag `-q` is used to filter reads for quality. CADIn filters with mapping quality 30 in standard mode. In case, when the input already have been filtered by mapping quality, you can put `-q 0`, this is help to reduce process time.

*Previous filtered by mapping quality*
```
CADIn -i FILE.bam -r REFERENCE.fasta -a ANNOTATION.gff -q 0
```

*Filtering by mapping quality*
```
CADIn -i FILE.bam -r REFERENCE.fasta -a ANNOTATION.gff -q 20
```

**Annotated regions**

GFF file has different information about annotation. Although this information was important only one can be used for analyses. We recommend those regions the best covers the chromosome/genome. Due this was put `-f gene` like standard.

*Calculate coverage using CDS regions*
```
CADIn -i FILE.bam -r REFERENCE.fasta -a ANNOTATION.gff -f CDS
```

**Temporary directory**

CADIn will be to create a directory in the same path where it's installed. However, you can find problems with permission or low space to save the temporary files. So, thought the flag `-s` the directory can be altered.

*Save temporary files in HOME path*
```
CADIn -i FILE.bam -r REFERENCE.fasta -a ANNOTATION.gff -s $HOME/test/tmp/
```

**Directory with results**

The software has the standard output directory `result_CADIn/`. With `-o` will be created a new directory to save the results. In case when input is similar this flag can help not overwriting the results.

*Change output directory*
```
CADIn -i FILE.bam -r REFERENCE.fasta -a ANNOTATION.gff -o test_Nov_2019/
```

**Selecting analysis**

The variant calling and depth coverage analysis can be done separately. The flag `-v` and `-c` when it’s equals 0, the CADIn doesn't evaluate variant calling or depth coverage, respectively, and will have no statistical and graphics referent that one. If both are 0 no analysis will be realized.

*Only variant calling analysis*
```
CADIn -i FILE.bam -r REFERENCE.fasta -a ANNOTATION.gff -c 0
```

*Only coverage analysis*
```
CADIn -i FILE.bam -r REFERENCE.fasta -a ANNOTATION.gff -v 0
```

You may also prefer to use only variant calling or coverage data without to generate statistics `-u` or graphics `-g` results. But, if the statistical results `-u` isn't generated, the graphics won't be either.

*No statistical analysis and graphics*
```
CADIn -i FILE.bam -r REFERENCE.fasta -a ANNOTATION.gff -u 0
```

*Only statistical analysis without to generate graphics*
```
CADIn -i FILE.bam -r REFERENCE.fasta -a ANNOTATION.gff -g 0
```

*Only statistical analysis of the variant calling data*
```
CADIn -i FILE.bam -r REFERENCE.fasta -a ANNOTATION.gff -c 0 -g 0
```

*Only coverage analysis and no statistics*
```
CADIn -i FILE.bam -r REFERENCE.fasta -a ANNOTATION.gff -v 0 -u 0
```

## Citation
*Citation: Coqueiro-dos-Santos, A. Xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.*
## Licence
>[GNU General Public License v3.0](https://github.com/coqueiro-dos-santos/CADIn/blob/master/LICENSE.txt)
## Author
- **Name:** Anderson Coqueiro-dos-Santos
- **E-mail:** andersoncoqueiro8@gmail.com
- **Github:** [github.com/coqueiro-dos-santos](https://github.com/coqueiro-dos-santos)
- **Mendeley:** [mendeley.com/profiles/anderson-coqueiro-dos-santos2](https://www.mendeley.com/profiles/anderson-coqueiro-dos-santos2/)
- **Linkedin:** [linkedin.com/in/anderson-coqueiro-dos-santos-248789170](https://www.linkedin.com/in/anderson-coqueiro-dos-santos-248789170/)
- **Lattes:** [lattes.cnpq.br/7550107239214921](http://lattes.cnpq.br/7550107239214921)
