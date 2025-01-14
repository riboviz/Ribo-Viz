# Install prerequisites

## About these instructions

These instructions were written for and tested on Ubuntu 18.04 LTS bionic.

Other Linux flavours will require different commands to be run. Similarly, for other operating systems.

Other versions of the prerequisites may also be usable.

Only minimal installation instructions are given for each prerequisite. See the documentation for each prerequisite for full instructions.

Under Linux, installing some of these tools requires you to have `sudo` access to install and configure software (or a local system administrator to do this for you).

## Python

Web site: [python](https://www.python.org/)

If you already have Python you can skip this step. If you don't have Python then we recommend [Miniconda](https://conda.io/miniconda.html) Python.

Either Python 2.7+ or Python 3.6+ can be used.

### Miniconda Python 2.7

```bash
wget https://repo.continuum.io/miniconda/Miniconda2-latest-Linux-x86_64.sh -O miniconda2.sh
bash miniconda2.sh -b -p $HOME/miniconda2
```

Set environment and check:

```bash
source $HOME/miniconda2/bin/activate
```
```bash
python -V
```
```
Python 2.7.15 :: Anaconda, Inc.
```

### Miniconda Python 3.6

```bash
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O miniconda3.sh
bash miniconda3.sh -b -p $HOME/miniconda3
```

Set environment and check:

```bash
source $HOME/miniconda3/bin/activate
```
```bash
python -V
```
```
Python 3.6.5 :: Anaconda, Inc.
```

## Cutadapt

Web sites:

* [GitHub](https://github.com/marcelm/cutadapt)
* [readthedocs](https://cutadapt.readthedocs.io/)

Install:

```bash
conda install -y -c bioconda cutadapt 
```

Check:

```bash
conda list | grep cutadapt
```
```
cutadapt                  1.16 ...
```

```bash
cutadapt --v
```
```
1.16
```

## pysam

Web sites:

* [GitHub](https://github.com/pysam-developers/pysam/)
* [readthedocs](https://pysam.readthedocs.io/)

Install:

```bash
conda install -y -c bioconda pysam
```

Check:

```bash:
conda list | grep pysam
```
```
pysam                     0.14.1 ...
```

pysam needs to be consistent with htslib/samtools. pysdam 0.14.1 wraps htslib/samtools versions 1.7.0 (see pysam [release notes](http://pysam.readthedocs.io/en/latest/release.html).

## samtools 1.7

Web site: [Samtools](http://www.htslib.org/)

**Note:** the version installed must be compatible with pysam above.

Install:

```bash
sudo apt-get install samtools
```

Check:

```bash
samtools --version
```
```
samtools 1.7
Using htslib 1.7-2
Copyright (C) 2018 Genome Research Ltd.
```

## bedtools

Web site: [bedtools](http://bedtools.readthedocs.io/en/latest/)

Install:

```bash
sudo apt-get install bedtools
```

Check:

```bash
bedtools -version
```
```
bedtools v2.26.0
```

## Hisat2

Web site: [Hisat2](https://ccb.jhu.edu/software/hisat2/index.shtml)

Install:

```bash
wget ftp://ftp.ccb.jhu.edu/pub/infphilo/hisat2/downloads/hisat2-2.1.0-Linux_x86_64.zip
unzip hisat2-2.1.0-Linux_x86_64.zip 
ls hisat2-2.1.0/
```

Update `PATH` and check:

```bash
export PATH=~/hisat2-2.1.0:$PATH
hisat2 --version
```
```
/home/ubuntu/hisat2-2.1.0/hisat2-align-s version 2.1.0
64-bit
Built on login-node03
Wed Jun  7 15:53:42 EDT 2017
Compiler: gcc version 4.8.2 (GCC) 
Options: -O3 -m64 -msse2 -funroll-loops -g3 -DPOPCNT_CAPABILITY
Sizeof {int, long, long long, void*, size_t, off_t}: {4, 8, 8, 8, 8, 8}
```

## Bowtie

Web site: [Bowtie](http://bowtie-bio.sourceforge.net/index.shtml)

**Note:** We are working to add back a Bowtie alignment option.

Install:

```bash
wget https://sourceforge.net/projects/bowtie-bio/files/bowtie/1.2.2/bowtie-1.2.2-linux-x86_64.zip/download -O bowtie.zip
unzip bowtie.zip
ls bowtie-1.2.2-linux-x86_64/
```

Update `PATH` and check:

```bash
export PATH=~/bowtie-1.2.2-linux-x86_64/:$PATH
bowtie --version
```
```
/home/ubuntu/bowtie-1.2.2-linux-x86_64/bowtie-align-s version 1.2.2
64-bit
Built on 462e5beae518
Mon Dec 11 19:27:01 UTC 2017
Compiler: gcc version 4.8.2 20140120 (Red Hat 4.8.2-15) (GCC) 
Options: -O3 -m64  -Wl,--hash-style=both -DWITH_TBB -DPOPCNT_CAPABILITY -g -O2 -fvisibility=hidden -I/hbb_exe/include   -g -O2 -fvisibility=hidden -I/hbb_exe/include  
Sizeof {int, long, long long, void*, size_t, off_t}: {4, 8, 8, 8, 8, 8}
```

## hdf5tools

Web site: [HDF5](https://portal.hdfgroup.org/display/HDF5)

Install:

```
sudo apt-get install hdf5-tools
```

## Create `setenv.sh`

```bash
#!/usr/bin/env bash
export PATH=~/hisat2-2.1.0:$PATH
export PATH=~/bowtie-1.2.2-linux-x86_64/:$PATH
```

## R 2.14.0+

Web sites:

* [The R Project for Statistical Computing](https://www.r-project.org/)
* [The Comprehensive R Archive Network](https://cran.r-project.org/) (CRAN).

**Note:** Release 2.14.0 or later is required as it includes the [parallel](https://stat.ethz.ch/R-manual/R-devel/library/parallel/html/00Index.html) package.

Edit `/etc/apt/sources.list` and add:

```
deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/
```

Install:

```bash
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9
sudo apt-get update
sudo apt-get install r-base
sudo apt-get install r-base-dev
```

Check:

```bash
R --version
```
```
R version 3.5.1 (2018-07-02) -- "Feather Spray"
```

## Rsamtools

Web site: [Rsamtools](https://bioconductor.org/packages/release/bioc/html/Rsamtools.html)

Install in R:

```R
source("https://bioconductor.org/biocLite.R")
biocLite("Rsamtools")
```

**Troubleshooting: installation path not writeable**

The following warning can be ignored:

```
installation path not writeable, unable to update packages: foreign
```

See [Question: unable to update packages: foreign, Matrix](https://support.bioconductor.org/p/96834/) for an explanation:

> That's not an error! You just got an informative message saying that two of the base R packages couldn't be updated...
> All of your Bioconductor packages end up in the first dir, which is writeable by you, and the base and core packages go in the second dir, which is only writeable by an administrator. You shouldn't be running R as an administrator, like ever, so it's common for you to get the message that you saw. If you really care to update the core packages, you can run R as an administrator, do biocLite, and then restart as a lower-permissioned user after the update.

You can check that it is available e.g.:

```bash
ls ~/R/x86_64-pc-linux-gnu-library/3.5/Rsamtools/
```
```
DESCRIPTION  libs  LICENSE  Meta  NAMESPACE  NEWS
```

**Troubleshooting: Cannot allocate memory**

```
Error in system2(file.path(R.home("bin"), "R"), c(if (nzchar(arch)) paste0("--arch=",  : 
  cannot popen ' '/usr/lib/R/bin/R' --no-save --slave 2>&1 < '/tmp/Rtmpw3pOH7/file12471113d0d2b'', probable reason 'Cannot allocate memory'
* removing "/home/ubuntu/R/x86_64-pc-linux-gnu-library/3.5/Rsamtools"
Warning in q("no", status = status, runLast = FALSE) :
  system call failed: Cannot allocate memory

The downloaded source packages are in
	"/tmp/RtmpOEVbaL/downloaded_packages"
installation path not writeable, unable to update packages: foreign
Warning message:
In install.packages(pkgs = doing, lib = lib, ...) :
  installation of package �Rsamtools� had non-zero exit status
```

You may need to assign more memory to R or your machine.

## rhdf5

Web site: [rhdf5](https://bioconductor.org/packages/release/bioc/html/rhdf5.html)

Install in R:

```R
biocLite("rhdf5")
```

**Troubleshooting: installation path not writeable**

See "Troubleshooting: installation path not writeable" for Rsamtools above.

## rtracklayer

Web site: [rtracklayer](https://bioconductor.org/packages/release/bioc/html/rtracklayer.html)

Install required packages:

```bash
sudo apt-get install -y libxml2-dev
sudo apt-get install -y libcurl4-openssl-dev
```

Install in R:

```R
biocLite("rtracklayer")
```

**Troubleshooting: installation path not writeable**

See "Troubleshooting: installation path not writeable" for Rsamtools above.

**Troubleshooting: installation of package "XML" had non-zero exit status**

If you get:

```
1: In install.packages(pkgs = doing, lib = lib, ...) :
  installation of package "XML" had non-zero exit status
```

Then check you installed the `libxml2-dev` package.

**Troubleshooting: installation of package "RCurl"|"GenomeInfoDb"|"GenomicRanges" had non-zero exit status**

If you get:

```
1: In install.packages(pkgs = doing, lib = lib, ...) :
  installation of package "RCurl" had non-zero exit status
2: In install.packages(pkgs = doing, lib = lib, ...) :
  installation of package "GenomeInfoDb" had non-zero exit status
3: In install.packages(pkgs = doing, lib = lib, ...) :
  installation of package "GenomicRanges" had non-zero exit status
```

Then check you installed the `libcurl4-openssl-dev` package.

## RcppRoll

Web site: [RcppRoll](https://cran.r-project.org/web/packages/RcppRoll/index.html)

Install in R:

```R
install.packages("RcppRoll")
```

## optparse

Web site: [optparse](https://cran.r-project.org/web/packages/optparse/index.html)

Install in R:

```R
install.packages("optparse")
```

## tidyr

Web site: [tidyr](https://cran.r-project.org/web/packages/tidyr/index.html)

Install in R:

```R
install.packages("tidyr")
```

## ggplot2

Web site: [ggplot2](https://cran.r-project.org/web/packages/ggplot2/index.html)

Install in R:

```R
install.packages("ggplot2")
```

## shiny

Web site: [shiny](https://cran.r-project.org/web/packages/shiny/index.html)

Install in R:

```R
install.packages("shiny")
```

## plotly

Web site: [plotly](https://plot.ly)

Install required packages:

```bash
sudo apt-get install -y libssl-dev
sudo apt-get install -y libcurl4-openssl-dev
```

Install in R:

```R
install.packages("plotly")
```


**Troubleshooting: ERROR: dependency "httr" is not available for package "plotly"""

If you get:

```
ERROR: dependency "httr" is not available for package "plotly"
```

Then check you installed the `libssl-dev` and `libcurl4-openssl-dev` packages.

## Check names and versions of Python packages

Run:

```bash
conda list
```
```
cutadapt                  1.16 ...

pysam                     0.14.1 ...
```

## Check names and versions of R packages

From [list user installed packages](https://www.r-bloggers.com/list-of-user-installed-r-packages-and-their-versions/):

Run in R:

```R
ip <- as.data.frame(installed.packages()[,c(1,3:4)])
rownames(ip) <- NULL
ip <- ip[is.na(ip$Priority),1:2,drop=FALSE]
print(ip, row.names=FALSE)
```
```
    Package   Version
              ggplot2     3.0.0
...
             optparse     1.6.0
...
               plotly     4.8.0
...
             RcppRoll     0.3.0
...
                rhdf5    2.24.0
...
            Rsamtools    1.32.2
          rtracklayer    1.40.4
...
                shiny     1.1.0
...
                tidyr     0.8.1
...
```
