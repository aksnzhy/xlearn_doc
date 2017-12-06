Installation Guide
^^^^^^^^^^^^^^^^^^^^^^^^^^^

For now, xLearn can support Linux and Mac OSX. We will support it on Windows in 
the near future. This page gives instructions on how to build and install the xLearn 
package using pip, or from source code. Whatever way you choose, make sure that your 
OS has already installed ``GCC`` (or ``Clang``) and ``CMake``, and your compiler need 
to support ``C++11``. If you have not installed them, please see `this page`__ on how to 
install GCC and CMake.

Install xLearn from pip
---------------------------

The easiest way to install xLearn is to use ``pip``. The following command will download the xLearn 
source code from pip and build it locally. We will update the xLearn source code on pip weekly. ::

    sudo pip install xlearn

The installation process will take a while to complete. And then you can type the following script 
in python shell to check whether the xLearn has been installed successfully:

>>> import xlearn as xl
>>> xl.hello()

If you want to build the lastest code from github, or you want to use the xLearn command line 
instead of the python API, you can see how to build xLearn from source code as follow.


Install xLearn from source code
----------------------------------

Building xLearn from source code consists tow steps:

1. First, build the executable files (``learn_train`` and ``xlearn_predict``) and shared library (``libxlearn.so`` 
for Linux and ``libxlearn.dylib`` for Mac OSX) from the C++ code.

2. Then, install the python package.

Fortunately, we write a script ``build.sh`` to do all the things for users.

First you need is to clone the code from github ::

  git clone https://github.com/aksnzhy/xlearn.git

and then build xLearn using the folloing commands ::

  cd xlearn
  ./build.sh

Test
----------------------------------

Now you can check your building by using xlearn command line ::

  cd build
  ./run_example.sh


You can also test the python package by using ::

  cd python-package/test
  python test_python.py

.. __: install_cmake.html

 .. toctree::
   :hidden:

   install_cmake.rst