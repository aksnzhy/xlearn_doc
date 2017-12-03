.. xlearn_doc documentation master file, created by
   sphinx-quickstart on Sun Dec  3 18:43:51 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Get Started with xLearn !
^^^^^^^^^^^^^^^^^^^^^^^^^^^

xLearn is a *high-performance*, *easy-to-use*, and *scalable* machine learning package, 
which can be used to solve large-scale machine learning problems. xLearn is especially useful 
for solving large-scale sparse data, which is very common in the scenes like CTR prediction and 
recommender system. If you are the user of liblinear, libfm, or libffm, now xLearn the 
your another better choice. 

This is a quick start tutorial showing snippets for you to quickly try out xLearn on the demo 
dataset on a binary classfication task.

Link to Helpful Other Resources
----------------------------------

 * See `Installation Guide`__ on how to install xLearn.
 * See `Command Line Guide`__ on how to use xLearn command line. 
 * See `Python API Guide`__ on how to use xLearn Python API.
 * See `Demo Page`__ Learning to use xLearn by Examples
 * See `Tutorials`__ on tutorial on specific tasks.

Quick Install
----------------------------------

We can install xLearn by using pip. The follow command will download the xLearn 
source code and build it locally. We will update the xLearn source code on pip weekly. ::

    sudo pip install --index-url https://test.pypi.org/simple/ xlearnn 

You can see the installation details from `Installation Guide`__.

Python Demo
----------------------------------

>>> import xlearn as xl
>>> ffm_model = xl.create_ffm() # Create FFM model
>>> ffm_model.setTrain("./small_train.txt") # Training set
>>> ffm_model.setValidate("./small_test.txt") # Validation set
>>> param = { 'task':'binary', 'lr':0.2, 'lambda':0.002, 'metric':'auc'} # Set parameter
>>> ffm_model.fit(param, "./model.out") # Train model
>>> ffm_model.setTest("./small_test.txt") # Test set
>>> ffm_model.predict("./model.out", "./output.txt") # Predict

This example shows how to use xlearn to solve a binary classification task.

 .. __: install
 .. __: commandline
 .. __: pythonapi
 .. __: demo
 .. __: tutorial
 .. __: install

.. toctree::
   :maxdepth: 2