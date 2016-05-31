# Conda: an environment and package manager

Why use conda?

- Manage independent environments with isolated dependencies
- Install libraries and programs reproducibly by version number
- Distribute pre-built binaries for complex programs like BLAST
- Maybe the only sane way to use Python+numpy/scipy on Windows

What do we get over pip and virtualenv?

- Many non-Python programs and libraries (R, Perl, C, C++, Ruby)
- Binary distributions: no compiling
- No admin priviledges required for installs
- Reproduce and copy environments easily
- Easy way to use the latest versions of Python 2 and 3

## Demonstration

*Install gnarly Python libraries*:
```sh
# Binary installs on all platforms!
conda install numpy
python -m numpy
```

*Installing complex non-Python programs:*

```sh
# Need to blast some stuff?
blastn -help
# Darn, it isn't installed. Time to ask our sysadmin, or...
conda install blast
blastn -help
# Hooray! It works! What about this funky program that uses Java?
conda install -c bioconda trimmomatic
trimmomatic
```

*Creating environments:*

```sh
# Make a new environment called `my_env` that uses Python3 and has BioPython
conda create -n myenv -c bioconda python=3 biopython
# Activate it, just like virtualenvwrapper
source activate myenv
# Install some stuff post-facto
conda install -n myenv -c bioconda bowtie2
# Done with this environment for now!
source deactivate
```

*Sharing environments:*

```sh
# On your machine
conda env export -n myenv > myenv.yaml
less myenv.yaml
# Somewhere else...
conda env create -f myenv.yaml
source activate myenv
```

*Using custom channels:*

```sh
conda install -c eclarke idba
```

## Installation

Conda comes in two forms: `Anaconda`, which installs a large suite of scientific 
software by default, or `miniconda`, a minimalist install that only installs the
basics. I prefer `miniconda`. Download here: http://conda.pydata.org/miniconda.html

By default, it is installed to a folder (e.g. `$HOME/miniconda3`) in your home 
directory. By adding the `miniconda3/bin` folder to your path, you can work with
all the conda tools easily. At no point do you need admin privileges.

To uninstall, simply remove the folder from your home directory. Nothing else is
changed on your system.

```sh
# Example for linux:
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
```
