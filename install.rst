Installation Guide
^^^^^^^^^^^^^^^^^^^^^^^^^^^

For now, xLearn can support Linux and Mac OSX. We will support Windows in the future.
This page gives instructions on how to build and install the xLearn package from 
source code or using pip. Whatever way you choose, make sure that your OS has already 
installed GCC (or Clang) and CMake.

Install GCC or Clang
---------------------------

If you have already installed your compiler before, you can skip this step.

* On Cygwin, run setup.exe and install gcc and binutils.
* On Debian/Ubuntu Linux, type the command ::

      sudo apt-get install gcc binutils 

  to install GCC, or install Clang by using :: 

      sudo apt-get install clang 

* On FreeBSD, type the following command to install Clang :: 

      sudo pkg_add -r clang 

* On Mac OS X, install XCode gets you Clang.


Install CMake
---------------------------

If you have already installed CMake before, you can skip this step.

To install CMake from binary packages:

* On Cygwin, run setup.exe and install cmake.
* On Debian/Ubuntu Linux, type the command to install cmake ::

      sudo apt-get install cmake

* On FreeBSD, type the command ::
   
      sudo pkg_add -r cmake

On Mac OS X, if you have homebrew, you can use the command :: 

     brew install cmake

or if you have MacPorts, run :: 

     sudo port install cmake

You won't want to have both Homebrew and !MacPorts installed.


Install xLearn from pip
---------------------------

The easiest way to install xLearn by using pip. The following command will download the xLearn 
source code and build it locally. We will update the xLearn source code on pip weekly. ::

    sudo pip install --index-url https://test.pypi.org/simple/ xlearnn 

Now you can type the following code in python shell to check the installation:

>>> import xlearn as xl
>>> xl.hello()

If you want to build the lastest code on github, or you want to use the xLearn command line, 
you can see how to build xLearn from source code as follow.


Install xLearn from source code
----------------------------------

Building xLearn from source code consists tow steps:

* First, build the executable files (**xlearn_train** and **xlearn_predict**) and shared library (**libxlearn.so** for Linux and **libxlearn.dylib** for Mac OSX) from the C++ codes.
* Then, install the python package.

Build C++ code
>>>>>>>>>>>>>>>>

First you need is to clone the code from github ::

  git clone https://github.com/aksnzhy/xlearn.git

and then build xLearn using the folloing commands ::

  cd xlearn; mkdir build
  cd build
  cmake ..
  make

Now you can check your building by using xlearn command line ::

  ./xlearn_train ./small_train.txt -v ./small_test.txt -s 2
  ./xlearn_predict ./small_test.txt ./small_train.txt.model


Install python package
>>>>>>>>>>>>>>>>>>>>>>>>>>

Users can use the install-python.sh script to install python package ::

    cd python-package
    ./install-python.sh

The users can make a test ::

    python test_python.py

.. toctree::
   :maxdepth: 1