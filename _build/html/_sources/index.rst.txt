.. xlearn_doc documentation master file, created by
   sphinx-quickstart on Sun Dec  3 18:43:51 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Get Started with xLearn !
^^^^^^^^^^^^^^^^^^^^^^^^^^^

xLearn is a *high-performance*, *easy-to-use*, and *scalable* machine learning package, 
which can be used to solve large-scale machine learning problems, especially for for the 
problems on large-scale sparse data, which is very common in scenes like CTR prediction and 
recommender system. If you are the user of liblinear, libfm, or libffm, now xLearn is your 
another better choice. This is because xLearn handles all of these models in an uniform 
platform and provides better performance and scalability compared to its competitors.

This is a quick start tutorial showing snippets for you to quickly try out xLearn on a small 
demo dataset (Criteo CTR prediction) for a binary classfication task.

Link to the Other Helpful Resources
----------------------------------------

 * See `Installation Guide`__ on how to install xLearn.
 * See `Command Line Guide`__ on how to use xLearn command line. 
 * See `Python API Guide`__ on how to use xLearn Python API.
 * See `Demo Page`__ Learning to use xLearn by Examples.
 * See `Tutorial`__ on tutorials on specific tasks.

Quick Install
----------------------------------

The easiest way to install xLearn is to use pip. The following command will download the xLearn 
source code and build it locally. We will update the xLearn source code on pip weekly. ::

    sudo pip install xlearn

Now you can type the following script in python shell to check whether we install xLearn successfully:

>>> import xlearn as xl
>>> xl.hello()

If you meet any installation problem, or you want to build the lastest code on github, or you want to 
use the xLearn command line instead of the python API, you can see how to build xLearn from source code 
in `Installation Guide`__.

Python Demo
----------------------------------

Here is a simple python demo no how to use xLearn.

.. code-block:: python

   import xlearn as xl

   # create ffm model
   ffm_model = xl.create_ffm()
   # Set training data
   ffm_model.setTrain("./small_train.txt")  
   # Set validation data
   ffm_model.setValidate("./small_test.txt") 
   # set some hyper-parameters
   param = { 'task':'binary', 
             'lr':0.2, 
             'lambda':0.002, 
             'metric':'auc'} 
   # Train model
   ffm_model.fit(param, "./model.out")  

   # Set test data
   ffm_model.setTest("./small_test.txt")  
   # Convert output result to 0~1
   ffm_model.setSigmoid()
   # Predict
   ffm_model.predict("./model.out", "./output.txt")  

This example shows how to use xlearn to solve a simple binary classification task. 
You can find the demo data **small_train.txt** and **small_test.txt** from 
the **demo/classification/criteo_ctr/** directory.

Other Helpful Resources
--------------------------------------------

 .. __: install.html
 .. __: install.html
 .. __: command_line.html
 .. __: python_api.html
 .. __: demo.html
 .. __: tutorial.html

 .. toctree::

   install.rst
   command_line.rst
   python_api.rst
   demo.rst
   tutorial.rst