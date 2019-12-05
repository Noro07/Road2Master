# install python MAC

## Step 1: Install OS libraries

```bash
brew cask install xquartz
brew install gtk+3 boost
brew install boost-python3
```

## Step 2: Install Python 3

```bash
brew install python3
brew link python3
```

- check whether Python using homebrew install correctly

> which python3  # it should output /usr/local/bin/python3

- check Python versions

> python3 --version

## Step 3: Install Python libraries

- Install virtual environment

```bash
pip install virtualenv virtualenvwrapper
echo "# Virtual Environment Wrapper"
echo "source /usr/local/bin/virtualenvwrapper.sh" >> ~/.zshrc
source ~/.zshrc
```

- create virtual environment

> mkvirtualenv facecourse-py3 -p python3
> workon facecourse-py3

- now install python libraries within this virtual environment

> pip install numpy scipy matplotlib scikit-image scikit-learn ipython

- quit virtual environment

> deactivate

## Step 4: Install Dlib

### Step 4.1: Compile C++ library

> brew install dlib

### Step 4.2: Compile Python module

> workon facecourse-py3
> pip install dlib
> deactivate

==========================================================

- ERROR 1:

RuntimeError:
************************************************************************************
CMake must be installed to build the following extensions: dlib
************************************************************************************

> pip install cmake

- ERROR 2:

Cannot uninstall 'six'. It is a distutils installed project and thus we cannot accurately determine which files belong to it which would lead to only a partial uninstall.

> pip install tld --ignore-installed six --user
