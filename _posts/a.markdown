
install rosetta

https://pypi.org/project/pandas-datareader/
https://pypi.org/project/yahoofinancials/
https://docs.quandl.com/docs/python-installation
https://numba.pydata.org/
https://stackoverflow.com/questions/11618898/pg-config-executable-not-found

https://www.pydanny.com/setting-up-latex-on-mac-os-x.html


https://www.mostlyphysics.net/blog/2021/2/6/scientific-computing-on-an-apple-m1-system


# Install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install conda
wget https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-MacOSX-arm64.sh

chmod u+x Miniforge3-MacOSX-arm64.sh
./Miniforge3-MacOSX-arm64.sh

# You may need to copy settings from .bash_profile to .zshrc for conda to work; see
https://medium.com/@sumitmenon/how-to-get-anaconda-to-work-with-oh-my-zsh-on-mac-os-x-7c1c7247d896:
# Close and reopen terminal!

conda config --set auto_activate_base false # Optional

# Create and activate conda container
conda create --name scicomp python=3.9
source ~/.zshrc
conda activate scicomp

# Install required packages for ASE; pip does not work
conda install matplotlib
conda install scipy=1.5.3
conda install pillow

# Install ASE development version
git clone https://gitlab.com/ase/ase.git
cd ase
pip install .

# Run ASE tests
conda install pytest
pytest --pyargs ase

# Start installing required packages for GPAW
brew install libxc

# Check that the paths match your system!
export C_INCLUDE_PATH=/opt/homebrew/Cellar/libxc/4.3.4_1/include
export LIBRARY_PATH=/opt/homebrew/Cellar/libxc/4.3.4_1/lib
export LD_LIBRARY_PATH=/opt/homebrew/Cellar/libxc/4.3.4_1/lib

brew install fftw

brew install open-mpi

brew install scalapack

export LDFLAGS="-L/opt/homebrew/opt/openblas/lib"
export CPPFLAGS="-I/opt/homebrew/opt/openblas/include"

# Install GPAW development version from Git
git clone https://gitlab.com/gpaw/gpaw.git
cd gpaw
pip install .

# Test GPAW
conda install pytest-xdist
pytest -n 4 --pyargs gpaw # Running tests in parallel on 4 cores.


https://jupyter.org/install

