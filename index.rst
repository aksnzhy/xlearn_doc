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

If you want to build the lastest code on github, or you want to use the xLearn command line, 
you can see how to build xLearn from source code from `Installation Guide`__.

Python Demo
----------------------------------

Here is a simple python demo no how to use xLearn. Now type **python** and get started!

>>> import xlearn as xl
>>> ffm_model = xl.create_ffm()  # create ffm model
>>> ffm_model.setTrain("./small_train.txt")  # set training data
>>> ffm_model.setValidate("./small_test.txt") # Validation data
>>> param = { 'task':'binary', 'lr':0.2, 'lambda':0.002, 'metric':'auc'}  # set parameters
>>> ffm_model.fit(param, "./model.out")  # train model
>>> ffm_model.setTest("./small_test.txt")  # set test data
>>> ffm_model.predict("./model.out", "./output.txt")  # predict

This example shows how to use xlearn to solve a simple binary classification task. 
You can find the demo data **small_train.txt** and **small_test.txt** from the **demo/classification/criteo_ctr/**

 .. __: install
 .. __: commandline
 .. __: pythonapi
 .. __: demo
 .. __: tutorial
 .. __: install

.. toctree::
   :maxdepth: 2