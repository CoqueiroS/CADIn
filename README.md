# **CADIn**
### Chromosomal Amplification and Delition Inference
###### Coqueiro-dos-Santos, A.

Dependences

Perl 
BCFTools (version 1.9)
BEDTools (2.26 or superior)
SAMTools (version 1.9)
R (version 3.4 or superior)

Perl Modules
Statistics::R

Instalation

BEDTools and R (instalation)

To CentOS 7 / Fedora / Red Hat
BEDTools -> sudo yum install BEDTools
R -> sudo yum install R
If not found run 'sudo yum install epel-release' before

To Ubuntu 18.04

BEDTools
sudo apt-get install bedtools

R
sudo apt-get install r-base

BCFTools
sudo apt-get install bcftools

SAMTools
sudo apt-get install samtools

Install Dependences

BCFTools and SAMTools (version 1.9)
Page: http://www.htslib.org/download/
bcftools -> https://github.com/samtools/bcftools/releases/download/1.9/bcftools-1.9.tar.bz2
samtools -> https://github.com/samtools/samtools/releases/download/1.9/samtools-1.9.tar.bz2

wget link
tar -xvf *tools-1.9.tar.bz2

cd samtools-1.x    # and similarly for bcftools
./configure --prefix=/where/to/install
make
make install

export PATH=/where/to/install/bin:$PATH
