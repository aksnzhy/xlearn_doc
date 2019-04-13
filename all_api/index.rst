xLearn API List
^^^^^^^^^^^^^^^^^^^^^^^^^^^

This page gives the xLearn API List for the command line, Python package, and R package.

xLearn Command Line Usage
------------------------------

For Training: ::

    xlearn_train <train_file_path> [OPTIONS]

Options: ::

  -s <type> : Type of machine learning model (default 0)
     for classification task:
         0 -- linear model (GLM)
         1 -- factorization machines (FM)
         2 -- field-aware factorization machines (FFM)
     for regression task:
         3 -- linear model (GLM)
         4 -- factorization machines (FM)
         5 -- field-aware factorization machines (FFM)
                                                                           
  -x <metric>          :  The metric can be 'acc', 'prec', 'recall', 'f1', 'auc' for classification, and
                          'mae', 'mape', 'rmsd (rmse)' for regression. On defaurt, xLearn will not print
                          any evaluation metric information (only print loss value).                                           
                                                                                                     
  -p <opt_method>      :  Choose the optimization method, including 'sgd', adagrad', and 'ftrl'. On default,
                          xLearn uses the 'adagrad' optimization method.
                                                                                                
  -v <validate_file>   :  Path of the validation data. This option will be empty by default. In this way, 
                          xLearn will not perform validation process.
                                                                                             
  -m <model_file>      :  Path of the model dump file. On default, the model file name is 'train_file' + '.model'. 
                          If we set this value to 'none', the xLearn will not dump the model checkpoint.

  -pre <pre-model>     :  Path of the pre-trained model. This can be used for online learning. 

  -t <txt_model_file>  :  Path of the TEXT model checkpoint file. On default, we do not set this option
                          and xLearn will not dump the TEXT model.
                                                                            
  -l <log_file>        :  Path of the log file. xLearn uses '/tmp/xlearn_log.*' by default.
                                                                                      
  -k <number_of_K>     :  Number of the latent factor used by FM and FFM tasks. Using 4 by default.
                          Note that, we will get the same model size when setting k to 1 and 4.
                          This is because we use SSE instruction and the memory need to be aligned.
                          So even you assign k = 1, we still fill some dummy zeros from k = 2 to 4.
                                                                                         
  -r <learning_rate>   :  Learning rate for optimization method. Using 0.2 by default.
                          xLearn can use adaptive gradient descent (AdaGrad) for optimization problem,
                          if you choose AdaGrad method, the learning rate will be changed adaptively.
                                                                                    
  -b <lambda_for_regu> :  Lambda for L2 regular. Using 0.00002 by default. We can disable the
                          regular term by setting this value to zero.

  -alpha               :  Hyper parameters used by ftrl.
                                       
  -beta                :  Hyper parameters used by ftrl.
                                       
  -lambda_1            :  Hyper parameters used by ftrl.
                                       
  -lambda_2            :  Hyper parameters used by ftrl.     

  -u <model_scale>     :  Hyper parameter used for initialize model parameters. Using 0.66 by default.
                                                                                 
  -e <epoch_number>    :  Number of epoch for training process. Using 10 by default. Note that xLearn will perform 
                          early-stopping by default, so this value is just a upper bound.
                                                                                       
  -f <fold_number>     :  Number of folds for cross-validation (If we set --cv option). Using 5 by default.    

  -nthread <thread_number> :  Number of thread for multiple thread lock-free learning (Hogwild!).

  -block <block_size>  :  Block size for on-disk training.

  -sw <stop_window>    :  Size of stop window for early-stopping. Using 2 by default. 

  -seed <random_seed>  :  Random Seed to shuffle data set.
                                                                                     
  --disk               :  Open on-disk training for large-scale machine learning problems.
                                                                   
  --cv                 :  Open cross-validation in training tasks. If we use this option, xLearn will ignore 
                          the validation file (set by -t option). 
                                                                  
  --dis-lock-free      :  Disable lock-free training. Lock-free training can accelerate training but the result 
                          is non-deterministic. Our suggestion is that you can open this flag if the training data 
                          is big and sparse.
                                                                       
  --dis-es             :  Disable early-stopping in training. By default, xLearn will use early-stopping
                          in training process, except for training in cross-validation.
                                                                                         
  --no-norm            :  Disable instance-wise normalization. By default, xLearn will use instance-wise 
                          normalization in both training and prediction processes.

  --no-bin             :  Do not generate bin file for training and test data file.
                                                                 
  --quiet              :  Don't print any evaluation information during the training and just train the 
                          model quietly. It can accelerate the training process.

For Prediction: ::

    xlearn_predict <test_file_path> <model_file_path> [OPTIONS]

Options: ::

  -o <output_file>     :  Path of the output file. On default, this value will be set to 'test_file' + '.out'
                                                      
  -l <log_file_path>   :  Path of the log file. xLearn uses '/tmp/xlearn_log' by default.  

  -nthread <thread number> :  Number of thread for multiple thread lock-free learning (Hogwild!).

  -block <block_size>      :  Block size fot on-disk prediction. 

  --sign                   :  Converting output result to 0 and 1.

  --sigmoid                :  Converting output result to 0 ~ 1 (problebility).

  --disk                   :  On-disk prediction.

  --no-norm                :  Disable instance-wise normalization. By default, xLearn will use instance-wise 
                              normalization in both training and prediction processes.

xLearn Python API
------------------------------

API List: ::

    import xlearn as xl      # Import xlearn package

    xl.hello()               # Say hello to user

    # This part is for data
    # X is feautres data, can be pandas DataFrame or numpy.ndarray,
    # y is label, default None, can be pandas DataFrame\Series, array or list,
    # filed_map is field map of features, default None, can be pandas DataFrame\Series, array or list
    dmatrix = xl.DMatrix(X, y, field_map)  

    model = create_linear()  #  Create linear model.

    model = create_fm()      #  Create factorization machines.

    model = create_ffm()     #  Create field-aware factorizarion machines.

    model.show()             #  Show model information.

    model.fit(param, "model_path")   #  Train model.

    model.cv(param)    # Perform cross-validation.
    
    # Users can choose one of this two
    model.predict("model_path", "output_path")  # Perform prediction, output result to file, return None.
    model.predict("model_path")                 # Perform prediction, return result by numpy.ndarray. 
    
    # Users can choose one of this two
    model.setTrain("data_path")      #  Set training data from file for xLearn.
    model.setTrain(dmatrix)          #  Set training data from DMatrix for xLearn.
    
    # Users can choose one of this two
    # note: this type of validate must be same as train
    # that is, set train from file, must set validate from file
    model.setValidate("data_path")   #  Set validation data from file for xLearn.
    model.setValidate(dmatrix)       #  Set validation data from DMatrix for xLearn.
    
    # Users can choose one of this two
    model.setTest("data_path")       #  Set test data from file for xLearn.
    model.setTest(dmatrix)           #  Set test data from DMatrix for xLearn.

    model.setQuiet()    #  Set xlearn to train model quietly.

    model.setOnDisk()   #  Set xlearn to use on-disk training.

    model.setNoBin()    # Do not generate bin file for training and test data.

    model.setSign()     # Convert prediction to 0 and 1.

    model.setSigmoid()  # Convert prediction to (0, 1).

    model.disableNorm() # Disable instance-wise normalization.

    model.disableLockFree()   # Disable lock-free training.

    model.disableEarlyStop()  # Disable early-stopping.

Parameter List: ::

    task     : {'binary',  # Binary classification
                'reg'}     # Regression

    metric   : {'acc', 'prec', 'recall', 'f1', 'auc',   # for classification
                'mae', 'mape', 'rmse', 'rmsd'}  # for regression

    lr       : float value  # learning rate

    lambda   : float value  # regular lambda

    k        : int value    # latent factor for fm and ffm

    init     : float value  # model initialize

    alpha    : float value  # hyper parameter for ftrl

    beta     : float value  # hyper parameter for ftrl

    lambda_1 : float value  # hyper parameter for ftrl

    lambda_2 : float value  # hyper parameter for ftrl

    nthread  : int value    # the number of CPU cores

    epoch    : int vlaue    # number of epoch

    fold     : int value    # number of fold for cross-validation

    opt      : {'sgd', 'agagrad', 'ftrl'}  # optimization method

    stop_window : Size of stop window for early-stopping.

    block_size : int value  # block size for on-disk training

xLearn R API
------------------------------

xLearn R API page is coming soon.
