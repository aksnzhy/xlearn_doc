Get Started with xLearn !
----------------------------------------

xLearn is a high-performance, easy-to-use, and scalable machine learning package, 
which can be used to solve large-scale machine learning problems, especially for the problems 
on large-scale sparse data, which is very common in scenes like CTR prediction and recommender 
system. If you are the user of liblinear, libfm, or libffm, now xLearn is your another better 
choice. This is because xLearn handles all of these models in a uniform platform and provides 
better performance and scalability compared to its competitors.

This is a quick start tutorial showing snippets for you to quickly try out xLearn on a small 
demo dataset (Criteo CTR prediction) for a binary classification task.

Link to the Other Helpful Resources
----------------------------------------

 * See `Installation Guide`__ on how to install xLearn.
 * See `Command Line Guide`__ on how to use xLearn command line. 
 * See `Python API Guide`__ on how to use xLearn Python API.
 * See `R API Guide`__ on how to use xLearn R API.
 * See `Demo Page`__ Learning to use xLearn by Examples.
 * See `Tutorial`__ on tutorials on specific tasks.

Quick Install
----------------------------------

The easiest way to install xLearn Python package is to use ``pip``. The following command will 
download the xLearn source code and install python package it locally. ::

    sudo pip install xlearn

The installation process will take a while to complete. And then you can type the following 
script in your python shell to check whether the xLearn has been installed successfully:

>>> import xlearn as xl
>>> xl.hello()

You will see: ::

  -------------------------------------------------------------------------
           _
          | |
     __  _| |     ___  __ _ _ __ _ __
     \ \/ / |    / _ \/ _` | '__| '_ \
      >  <| |___|  __/ (_| | |  | | | |
     /_/\_\_____/\___|\__,_|_|  |_| |_|

        xLearn   -- 0.44 Version --
  -------------------------------------------------------------------------

If you meet any installation problem, or you want to build the lastest code from github, or you want to 
use the xLearn command line instead of the python API, you can see how to build xLearn from source code 
in `Installation Guide`__.

Python Demo
----------------------------------

Here is a simple Python demo no how to use xLearn:

.. code-block:: python

    import xlearn as xl

    # Training task
    ffm_model = xl.create_ffm() # Use field-aware factorization machine
    ffm_model.setTrain("./small_train.txt")  # Training data
    ffm_model.setValidate("./small_test.txt")  # Validation data

    # param:
    #  0. binary classification
    #  1. learning rate: 0.2
    #  2. regular lambda: 0.002
    #  3. evaluation metric: accuracy
    param = {'task':'binary', 'lr':0.2, 
             'lambda':0.002, 'metric':'acc'}

    # Start to train
    # The trained model will be stored in model.out
    ffm_model.fit(param, './model.out')

    # Prediction task
    ffm_model.setTest("./small_test.txt")  # Test data
    ffm_model.setSigmoid()  # Convert output to 0-1

    # Start to predict
    # The output result will be stored in output.txt
    ffm_model.predict("./model.out", "./output.txt")

This example shows how to use *field-aware factorizations machine (ffm)* to solve a 
simple binary classification task. You can check out the demo data 
(``small_train.txt`` and ``small_test.txt``) from the path ``demo/classification/criteo_ctr``.

 .. __: install.html
 .. __: command_line.html
 .. __: python_api.html
 .. __: r_api.html
 .. __: demo.html
 .. __: tutorial.html
 .. __: install.html

 .. toctree::
   :hidden:

   start.rst
   install.rst
   command_line.rst
   python_api.rst
   r_api.rst
   xlearn_api.rst
   large_scale.rst
   demo.rst
   tutorial.rst