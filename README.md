# 23andMe Tools - Convert your 23andMe genotypes to VCF files

This project provides a Java implementation to convert your 23andMe genotype data into compressed VCFs (vcf.gz). VCF files can be useful for **imputation** with the [Michigan Imputation Server](https://imputationserver.sph.umich.edu) or for **mitochondrial haplogroup classification** with [HaploGrep](http://haplogrep.uibk.ac.at).

## Download your data
Your personal genome can be downloaded from [here](https://www.23andme.com/you/download). After entering your secure answer, the complete dataset can be downloaded at once.

## Generate VCF files
The VCF files are generated by combining information from your 23andMe data with the human reference file. This project uses [HTSJDK](https://github.com/samtools/htsjdk) for many tasks. 
The current version of the 23andMe genotyping chip v4 (> Nov 2013) uses the GRCh37 reference (aka g1k, v37) ```human_g1k_v37.fasta```.

```bash
git clone https://github.com/seppinho/23andme-tools.git
cd 23andme-tools
mvn install
java -jar vcf-tools-0.1.jar vcf-generator --in <your-genome.txt> --ref </path/to/human_g1k_v37.fasta> 
--out <vcf-destination-folder> [--exclude <chromosomes to exclude] [--split false]

```
The human_g1k_v37.fasta reference is not included in this repository. By setting ```--ref v37``` it will be downloaded automatically.

## Usage Examples

### Default Command
This command downloads the fasta reference and writes each chromosome (chr1-22,X,Y,MT) to a seperate vcf.gz file. Add ```--split false``` to write one VCF file. 

```bash
java -jar vcf-tools-0.1.jar vcf-generator --in /path/to/23andMe-genome.txt 
--ref v37 --out /path/to/vcfDir 
```

### Generating VCFs for Michigan Imputation Server

```bash
java -jar vcf-tools-0.1.jar vcf-generator --in /path/to/23andMe-genome.txt 
--ref /path/to/human_g1k_v37.fasta --out /path/to/vcfDir --exclude X,Y,MT
```
