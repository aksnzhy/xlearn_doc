xLearn Python API Guide
^^^^^^^^^^^^^^^^^^^^^^^^^^^

xLearn supports very easy-to-use python API for users. Once you install the 
xLearn python package successfully, you can try it! Type ``python`` in your
shell and perform the following python code to check your installation: ::

    import xlearn as xl
    xl.hello()

Output ::

  -------------------------------------------------------------------------
           _
          | |
     __  _| |     ___  __ _ _ __ _ __
     \ \/ / |    / _ \/ _` | '__| '_ \
      >  <| |___|  __/ (_| | |  | | | |
     /_/\_\_____/\___|\__,_|_|  |_| |_|

        xLearn   -- 0.10 Version --
  -------------------------------------------------------------------------

Quick Start
----------------------------------------

Here is a simple python demo no how to use xLearn. You can check out the demo data 
(``small_train.txt`` and ``small_test.txt``) from the path ``demo/classification/criteo_ctr``.

.. code-block:: python

   import xlearn as xl

   # Training task
   ffm_model = xl.create_ffm()
   ffm_model.setTrain("./small_train.txt")  
   ffm_model.setValidate("./small_test.txt") 
   param = {'task':'binary', 'lr':0.2, 'lambda':0.002} 
            
   ffm_model.fit(param, "./model.out")  

   # Prediction task
   ffm_model.setTest("./small_test.txt")  
   ffm_model.predict("./model.out", "./output.txt")  

Here, we show a portion of the xLearn's output ::

  Epoch      Train log_loss       Test log_loss     Time cost (sec)
      1            0.593750            0.535847                0.00
      2            0.539226            0.543829                0.00
      3            0.520034            0.531732                0.00
      4            0.505186            0.537418                0.00
      5            0.494089            0.533448                0.00
      6            0.483678            0.534629                0.00
      7            0.470848            0.528086                0.00
      8            0.466330            0.533253                0.00
      9            0.456660            0.535635                0.00
  Early-stopping at epoch 7

In this example, we use FFM to train our model within 9 epoch. We can see that a new
file called ``model.out`` has been generated in current directory. This file stores the 
trainned model checkpoint, and we can use this model file to make prediction in the future

After we perform the python code ::

    ffm_model.predict("./model.out", "./output.txt")      

we can get a new file called ``output.txt`` in current directory. This is output prediction
result. Let's see the first five lines of output by using the following command ::

    head -n 5 ./output.txt

    -1.5927
    -0.560985
    -0.773492
    -0.551364
    -1.22954

These five lines of data is the prediction score calculated for every example in test set. The
negative data represents the negative example and the positive data prepresents the positive example.
You can convert the score to ``(0-1)`` by using ``setSigmoid()`` ::

   # Prediction task
   ffm_model.setTest("./small_test.txt")  
   ffm_model.setSigmoid()
   ffm_model.predict("./model.out", "./output.txt")      

and then we can get the result ::

   head -n 5 ./output.txt

   0.162849
   0.352197
   0.308373
   0.356715
   0.217436

We can also convert the score to binary result ``(0 and 1)`` by using ``setSign()`` API ::

   # Prediction task
   ffm_model.setTest("./small_test.txt")  
   ffm_model.setSign()
   ffm_model.predict("./model.out", "./output.txt")

Output ::

   head -n 5 ./output.txt

   0
   0
   0
   0
   0

Choose Machine Learning Model
----------------------------------------

For now, xLearn can support three different machine learning models, including
LR, FM, and FFM. Users can create different models by using ``create_xxx()`` API.
For example: ::
   
    import xlearn as xl

    ffm_model = xl.create_ffm()
    fm_model = xl.create_fm()
    lr_model = xl.create_lr()


For LR and FM, the input data can be ``CSV`` or ``libsvm`` data format, while for FFM, the 
input data should be the ``libffm`` format. You can give a ``libffm`` file to LR and FM. At 
that time, xLearn will treat this data as ``libsvm`` format. 

Set Dataset
----------------------------------------

Users can set dataset by using ``setTrain()``, ``setTest()``, and ``setValidate()`` dataset.
The ``setTrain()`` and ``setValidate()`` are used for training task, while the ``setTest()`` 
is used for prediction task. If users don't set the validation file, xLearn will not calculate
any evaluation metric. For example: ::

   import xlearn as xl

   # Training task
   ffm_model = xl.create_ffm()
   ffm_model.setTrain("./small_train.txt")  
   param = {'task':'binary', 'lr':0.2, 'lambda':0.002} 
            
   ffm_model.fit(param, "./model.out") 


   Epoch      Train log_loss     Time cost (sec)
       1            0.593791                0.00
       2            0.540819                0.00
       3            0.518385                0.00
       4            0.504790                0.00
       5            0.492556                0.00
       6            0.481522                0.00
       7            0.473634                0.00
       8            0.464028                0.00
       9            0.456445                0.00
      10            0.448745                0.00

Cross Validation
----------------------------------------

Cross-validation, sometimes called rotation estimation, is a model validation technique 
for assessing how the results of a statistical analysis will generalize to an independent 
data set. In xLearn, users can use ``cv()`` API to perform cross-validation. For example: ::

    import xlearn as xl

    # Training task
    ffm_model = xl.create_ffm()
    ffm_model.setTrain("./small_train.txt")  
    param = {'task':'binary', 'lr':0.2, 'lambda':0.002} 
            
    ffm_model.cv(param) 


On default, xLearn uses 5-folds cross validation, and users can set number of fold 
by using the ``fold`` parameter in ``param`` ::

    import xlearn as xl

    # Training task
    ffm_model = xl.create_ffm()
    ffm_model.setTrain("./small_train.txt")  
    param = {'task':'binary', 'lr':0.2, 'lambda':0.002, 'fold':3} 
            
    ffm_model.cv(param)     

In this example, xLearn performs cross-validation in 3 folds.

Choose Optimization Method
----------------------------------------

In xLearn, users can choose different optimization methods by using ``opt`` parameter. For now, 
users can choose ``sgd``, ``adagrad``, and ``ftrl`` method. On default, xLearn uses the ``adagrad`` 
method. For example: ::

   ...

   param = {'task':'binary', 'lr':0.2, 'lambda':0.002, 'opt':'sgd'} 
   # param = {'task':'binary', 'lr':0.2, 'lambda':0.002, 'opt':'adagrad'} 
   # param = {'task':'binary', 'lr':0.2, 'lambda':0.002, 'opt':'ftrl'} 

   ffm_model.fit(param, "./model.out") 

Compared to traditional ``sgd`` method, ``adagrad`` adapts the learning rate to the parameters, performing 
larger updates for infrequent and smaller updates for frequent parameters. For this reason, it is well-suited 
for dealing with sparse data. In addtion, sgd is more sensetive to the learning rate compared with adagrad.

``FTRL`` (Follow-the-Regularized-Leader) is also a famous method that has been widely used in large-scale sparse 
problem. To use FTRL, users need to tune more hyperparameters compared with sgd and adagard.

Hyper-parameter Tuning
----------------------------------------


Set Epoch Number and Early Stopping
----------------------------------------


Lock-Free Training
----------------------------------------


Instance-Wise Normalization
----------------------------------------


Quiet Training
----------------------------------------



 .. toctree::
   :hidden: