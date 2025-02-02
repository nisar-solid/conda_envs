# conda_envs

Setup InSAR data processing codes on Linux / macOS.

NOTE: Archive this repo because its content has been merged into `nisar-solid/ATBD/docs/installation.md`.

### 1. Install conda

```bash
mkdir -p ~/tools; cd ~/tools

# download, install and setup (mini/ana)conda
# for Linux, use Miniconda3-latest-Linux-x86_64.sh
# for macOS, opt 2: curl https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh -o Miniconda3-latest-MacOSX-x86_64.sh
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh
chmod +x Miniconda3-latest-MacOSX-x86_64.sh
./Miniconda3-latest-MacOSX-x86_64.sh -b -p ~/tools/miniconda3
~/tools/miniconda3/bin/conda init bash
```

Close and restart the shell for changes to take effect.

```
conda config --add channels conda-forge
conda install wget git tree --yes
```

### 2. Install ATBD, ISCE-2, ARIA-tools and MintPy to `insar` environment

#### Download source code

```bash
cd ~/tools
mkdir isce2; cd isce2
mkdir build install src; cd src
git clone https://github.com/isce-framework/isce2.git

cd ~/tools
git clone https://github.com/nisar-solid/conda_envs.git
git clone https://github.com/nisar-solid/ATBD.git
git clone https://github.com/aria-tools/ARIA-tools.git
git clone https://github.com/insarlab/MintPy.git
git clone https://github.com/insarlab/PySolid.git
git clone https://github.com/yunjunz/PyAPS.git
```

#### Create `insar` environment and install pre-requisites

```bash
# create new environment
conda create --name insar
conda activate insar

# install dependencies with conda
conda install --yes --file ATBD/docs/requirements.txt --file MintPy/docs/conda.txt --file ARIA-tools/requirements.txt isce2 

# install dependencies not available from conda
ln -s ${CONDA_PREFIX}/bin/cython ${CONDA_PREFIX}/bin/cython3
$CONDA_PREFIX/bin/pip install git+https://github.com/tylere/pykml.git
$CONDA_PREFIX/bin/pip install ipynb        # import functions from ipynb files

# compile PySolid
cd ~/tools/PySolid/pysolid
f2py -c -m solid solid.for
```

#### Setup

Create an alias `load_insar` in `~/.bash_profile` file for easy activation, _e.g._:

```bash
alias load_insar='conda activate insar; source ~/tools/conda_envs/insar/config.rc'
```

#### Test the installation

Run the following to test the installation:

```bash
load_insar
topsApp.py -h
ariaDownload.py -h
smallbaselineApp.py -v
```
