# **CADIn** - Chromosomal Amplification and Delition Inference
###### *Coqueiro-dos-Santos, A.*
#
### What means CADIn?
CADIn is a softwares free (open source) that permit to search allelic differences in NGS (next generation sequences) data. This tool estimate ploidy level  for each chromosomes in individuo. For this, it calculate the allelic frequency based in single nucleotide variants and, furthermore, analyse depth reads in regions annotated with good coverage, like: genes, CDSs, exon and so on.

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

There are two packages (ggplot2 and outliers). Both are instaled from the CADIn.
They can be installed before. For this, open the R (software).
```
install.packages("<insert package name here>")
```

