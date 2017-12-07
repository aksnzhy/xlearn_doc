xLearn Command Line Guide
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Once you build xLearn from source code successfully, you will get two executable files 
``xlearn_train`` and ``xlearn_predict`` in your ``build`` directory. Now you can use these 
two executable files to perform training task and prediction task.

Quick Start
----------------------------------------

Make sure that you are in the build path of xLearn, and you will find the demo data 
``small_test.txt`` and ``small_train.txt`` in this directory. Now you can type the following 
command to train a model ::

    ./xlearn_train ./small_train.txt

Here we print a portion of the output ::

    Epoch      Train log_loss     Time cost (sec)
        1            0.567514                0.00
        2            0.516861                0.00
        3            0.489884                0.00
        4            0.469971                0.00
        5            0.452699                0.00
        6            0.437590                0.00
        7            0.425759                0.00
        8            0.415190                0.00
        9            0.405954                0.00
       10            0.396313                0.00

On default, xLearn will use the logistic regression (LR) to train our model for 10 epoch.

We can see that a new file called ``small_train.txt.model`` has been generated in current directory. 
This file stores the trainned model checkpoint, and we can use this model file to make prediction ::

    ./xlearn_predict ./small_test.txt ./small_train.txt.model

Then we can get a new file called ``small_test.txt.out`` in current directory. This is output 
prediction result. Let's see the first five lines of output by using the following command ::
    
    head -n 5 ./small_test.txt.out

    -1.9872
    -0.0707959
    -0.456214
    -0.170811
    -1.28986

The ten lines of data is the score for every example in test set. The negative data represents the 
negative example and positive data represents the positive example. You can convert the score to (0-1) 
by using ``--sigmoid`` option, or you can convert your result to bianry result (0 and 1) by using 
``--sign`` option ::

    ./xlearn_predict ./small_test.txt ./small_train.txt.model --sigmoid
    head -n 5 ./small_test.txt.out

    0.120553
    0.482308
    0.387884
    0.457401
    0.215877

    ./xlearn_predict ./small_test.txt ./small_train.txt.model --sign
    head -n 5 ./small_test.txt.out

    0
    0
    0
    0
    0

Choose Machine Learning Model
----------------------------------------

 .. toctree::
   :hidden: