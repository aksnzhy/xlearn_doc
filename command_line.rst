xLearn Command Line Guide
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Once you built xLearn from source code successfully, you will get two executable files 
``xlearn_train`` and ``xlearn_predict`` in your ``build`` directory. Now you can use these 
two executable files to perform training and prediction task.

Quick Start
----------------------------------------

Make sure that you are in the ``build`` directory of xLearn, and you will find the demo data 
``small_test.txt`` and ``small_train.txt`` in this directory. Now you can type the following 
command to train a model ::

    ./xlearn_train ./small_train.txt

Here, we show a portion of the xLearn's output ::

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

On default, xLearn will use the logistic regression (LR) to train our model within 10 epoch.

We can see that a new file called ``small_train.txt.model`` has been generated in current directory. 
This file stores the trainned model checkpoint, and we can use this model file to make prediction in 
the future ::

    ./xlearn_predict ./small_test.txt ./small_train.txt.model

Then we can get a new file called ``small_test.txt.out`` in current directory. This is output 
prediction result. Let's see the first five lines of output by using the following command ::
    
    head -n 5 ./small_test.txt.out

    -1.9872
    -0.0707959
    -0.456214
    -0.170811
    -1.28986

These five lines of data is the prediction score calculated for every example in test set. The 
negative data represents the negative example and positive data represents the positive example. 
You can convert the score to (0-1) by using ``--sigmoid`` option, or you can convert your result 
to binary result (0 and 1) by using ``--sign`` option ::

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

Users may generate many model files, so you can set the name of the model checkpoint file 
by using ``-m`` option ::

  ./xlearn_train ./small_train.txt -m model_1.bin
  ./xlearn_train ./small_train.txt -s 1 -m model_2.bin   

Also, users can dump the model in txt format by using ``-t`` option. For example: ::

  ./xlearn_train ./small_train.txt -t model.txt

Here, we get a file called ``model.txt`` that stores the trainned model in txt format.
For now, only bias and linear term can be wirtten to the txt file.

User can also set ``-o`` option to specify the output file. For example: ::

  ./xlearn_predict ./small_test.txt ./small_train.txt.model -o output.txt  

Choose Machine Learning Model
----------------------------------------

For now, xLearn can support three different machine learning model, including LR, FM and FFM.
Users can choose different machine learning models by using ``-s`` option ::

  -s <type> : Type of machine learning model (default 0)
     for classification task:
         0 -- linear model (GLM)
         1 -- factorization machines (FM)
         2 -- field-aware factorization machines (FFM)
     for regression task:
         3 -- linear model (GLM)
         4 -- factorization machines (FM)
         5 -- field-aware factorization machines (FFM)

For LR and FM, the input data can be ``CSV`` or ``libsvm`` data format, while for FFM, the 
input data should be the ``libffm`` format. You can give a ``libffm`` file to LR and FM. At that 
time, xLearn will treat this data as ``libsvm`` format. The following command shows how to use different
machine learning model to solve the binary classification problem:  ::

./xlearn_train ./small_train.txt -s 0  # Linear model
./xlearn_train ./small_train.txt -s 1  # Factorization machine (FM)
./xlearn_train ./small_train.txt -s 2  # Field-awre factorization machine (FFM)

Set Validation Dataset
----------------------------------------

A validation dataset is a set of examples used to tune the hyperparameters of a machine learning model. 
In xLearn, users can use ``-v`` option to set the validation data set. For example: ::

    ./xlearn_train ./small_train.txt -v ./small_test.txt    

A portion of xLearn's output: ::

    Epoch      Train log_loss       Test log_loss     Time cost (sec)
        1            0.575049            0.530560                0.00
        2            0.517496            0.537741                0.00
        3            0.488428            0.527205                0.00
        4            0.469010            0.538175                0.00
        5            0.452817            0.537245                0.00
        6            0.438929            0.536588                0.00
        7            0.423491            0.532349                0.00
        8            0.416492            0.541107                0.00
        9            0.404554            0.546218                0.00

Here we can see that, the training loss continuously goes down. While, the validation loss (test loss) goes 
down first, and then goes up. This is because our model has already overfitted current training data set. On 
default, xLearn will calculate the validation loss in each epoch, while users can also set different evaluation
metric by using ``-x`` option. For classification problem, the metric can be : ``acc`` (accuracy), ``prec`` 
(precision), ``f1`` (f1 score), ``auc`` (AUC score). For example: ::

    ./xlearn_train ./small_train.txt -v ./small_test.txt -x acc
    ./xlearn_train ./small_train.txt -v ./small_test.txt -x prec
    ./xlearn_train ./small_train.txt -v ./small_test.txt -x f1
    ./xlearn_train ./small_train.txt -v ./small_test.txt -x auc

For regression problem, the metric can be ``mae``, ``mape``, and ``rmsd`` (rmse). For example: ::

    cd demo/house_price/
    ../../xlearn_train ./house_price_train.txt -s 3 -x rmse --cv
    ../../xlearn_train ./house_price_train.txt -s 3 -x rmsd --cv

Cross Validation
----------------------------------------

Cross-validation, sometimes called rotation estimation, is a model validation technique for assessing 
how the results of a statistical analysis will generalize to an independent data set. In xLearn, users 
can set the ``--cv`` option to use this technique. For example: ::

    ./xlearn_train ./small_train.txt --cv

On default, xLearn uses 5-folds cross validation, and users can set the number of fold by using 
``-f`` option: ::
    
    ./xlearn_train ./small_train.txt -f 3 --cv

Here, we set the number of folds to ``3``. The xLearn will calcluate the avergae validation loss at the end 
of it's output message. ::

    [------------] Average log_loss: 0.549417
    [ ACTION     ] Finish Cross-Validation
    [ ACTION     ] Clear the xLearn environment ...
    [------------] Total time cost: 0.03 (sec)

Choose Optimization Method
----------------------------------------
 
In xLearn, users can choose different optimization methods by using ``-p`` option. For now, users can 
choose ``sgd``, ``adagrad``, and ``ftrl`` method. On default, xLearn uses the ``adagrad`` method. 
For example: ::

    ./xlearn_train ./small_train.txt -p sgd
    ./xlearn_train ./small_train.txt -p adagrad
    ./xlearn_train ./small_train.txt -p ftrl

Compared to traditional ``sgd`` method, ``adagrad`` adapts the learning rate to the parameters, performing
larger updates for infrequent and smaller updates for frequent parameters. For this reason, it is well-suited
for dealing with sparse data. In addtion, sgd is more sensetive to the learning rate compared with adagrad.

``FTRL`` (Follow-the-Regularized-Leader) is also a famous method that has been widely used in large-scale sparse 
problem. To use FTRL, users need to tune more hyperparameters compared with sgd and adagard. 

Hyper-parameter Tuning
----------------------------------------

In machine learning, a ``hyperparameter`` is a parameter whose value is set before the learning process begins. 
By contrast, the value of other parameters are derived via training. Hyperparameter tuning is the problem of choosing
a set of optimal hyperparameters for a learning algorithm. 

First, ``learning rate`` is one of the most important hyperparameter used in machine learning. On default, this 
value is ``0.2``. For example, we can tune this value by using ``-r`` option: ::

    ./xlearn_train ./small_train.txt -v ./small_test.txt -r 0.1
    ./xlearn_train ./small_train.txt -v ./small_test.txt -r 0.5
    ./xlearn_train ./small_train.txt -v ./small_test.txt -r 0.01


We can also use the ``-b`` option to perform regularization. On default, xLearn uses ``L2`` regularization, and 
the regular lambda has been set to ``0.00002``. ::

    ./xlearn_train ./small_train.txt -v ./small_test.txt -r 0.1 -b 0.001
    ./xlearn_train ./small_train.txt -v ./small_test.txt -r 0.1 -b 0.002
    ./xlearn_train ./small_train.txt -v ./small_test.txt -r 0.1 -b 0.01


For FTRL method, we also need to tune anoter four hyperparameters, including ``-alpha``, ``-beta``, ``-lambda_1``, and
``-lambda_2``. For example: ::

    ./xlearn_train ./small_train.txt -o ftrl -alpha 0.002 -beta 0.8 -lambda_1 0.001 -lambda_2 1.0

For fm and ffm, users need to set the size of latent factor by using ``-k`` option. On default, xLearn uses ``4`` for 
this value. ::

    ./xlearn_train ./small_train.txt -s 1 -v ./small_test.txt -k 2
    ./xlearn_train ./small_train.txt -s 1 -v ./small_test.txt -k 4
    ./xlearn_train ./small_train.txt -s 1 -v ./small_test.txt -k 5
    ./xlearn_train ./small_train.txt -s 1 -v ./small_test.txt -k 8

xLearn uses SSE instruction to accerlate vector operation, and hence the time cost for ``k=2`` and ``k=4`` are the same.

For FM and FFM, users can also set the hyperparameter ``-u`` for model initialization. On defualt, this value is 0.66. ::

    ./xlearn_train ./small_train.txt -s 1 -v ./small_test.txt -u 0.80
    ./xlearn_train ./small_train.txt -s 1 -v ./small_test.txt -u 0.40
    ./xlearn_train ./small_train.txt -s 1 -v ./small_test.txt -u 0.10

Set Epoch Number and Early Stopping
----------------------------------------

Users can set the epoch number for training by using ``-e`` option. ::

    ./xlearn_train ./small_train.txt -e 3
    ./xlearn_train ./small_train.txt -e 5
    ./xlearn_train ./small_train.txt -e 10   

While, if you set the validation data, xLearn will performance early-stopping by default. For example: ::
  
    ./xlearn_train ./small_train.txt -s 2 -v ./small_test.txt -e 10

Here, we set epoch number to ``10``, but xLearn stopped at epoch 7, because we get the best model at that epoch 
(you may get different a number on your machine) ::

  [ ACTION     ] Early-stopping at epoch 7
  [ ACTION     ] Start to save model ...

Users can disable early stopping by useing ``--dis-es`` option ::

    ./xlearn_train ./small_train.txt -s 2 -v ./small_test.txt -e 10 --dis-es

At this time, xLearn will perform ``10`` epoch for training.

Lock-Free Training
----------------------------------------

On default, xLearn performs ``Hogwild!`` lock-free training, which takes advantages of multiple core to accelerate
training task. But lock-free training is *non-deterministic*. For example, if we run the following command many times,
we will get different loss value at the last epoch. ::

   ./xlearn_train ./small_train.txt 

   The 1st time: 0.396352
   The 2nd time: 0.396119
   The 3nd time: 0.396187
   ...

Users can disable lock-free training by using ``--dis-lock-free`` ::

  ./xlearn_train ./small_train.txt --dis-lock-free

In thie time, our result are *determinnistic*, and we will get the same loss at the last epoch if we run xLearn many times. ::

   The 1st time: 0.396372
   The 2nd time: 0.396372
   The 3nd time: 0.396372

The disadvantage of ``--dis-lock-free`` is that it is much slower than lock-free training. 

Instance-Wise Normalization
----------------------------------------

For FM and FFM, xLearn uses *instance-wise normalizarion* by default. In some scenes like CTR prediction, this feature is very
useful. But sometimes it hurts convergence. So users can disable instance-wise normalization by using ``--no-norm`` option ::

  ./xlearn_train ./small_train.txt -s 1 -v ./small_test.txt --no-norm

We usually use ``--no-norm`` in regression tasks.

Quiet Training
----------------------------------------

When using ``--quiet`` option, xLearn will not calculate any evaluation information during the training, and 
it just train the model quietly ::

  ./xlearn_train ./small_train.txt --quiet

In this way, xLearn can accelerate its training speed.


 .. toctree::
   :hidden: