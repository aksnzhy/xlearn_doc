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
   # Convert output to 0~1
   ffm_model.setSigmoid()
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

In this example, we use FFM to train our model within 9 epoch.

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

Set Validation Dataset
----------------------------------------


Cross Validation
----------------------------------------


Choose Optimization Method
----------------------------------------


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