# **CADIn** - Chromosomal Amplification and Delition Inference
###### *Coqueiro-dos-Santos, A.*
#
### What does CADIn do?
Description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description description.

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
#### BCFTools and SAMTools (version 1.9)
**Main page:** `` http://www.htslib.org/download/ ``

**Links to softwares**
>[BCFTools v1.9](https://github.com/samtools/bcftools/releases/download/1.9/bcftools-1.9.tar.bz2)

>[Samtools v1.9](https://github.com/samtools/samtools/releases/download/1.9/samtools-1.9.tar.bz2)

**Install tools**

Download by terminal
```
wget <put here the link>
```
Decompress
```
tar -xvf *tools-1.9.tar.bz2
```
Configure and install
```
cd samtools-1.x    # and similarly for bcftools
./configure --prefix=/where/to/install
make
make install
```
Preparing to use
```
export PATH=/where/to/install/bin:$PATH
```


