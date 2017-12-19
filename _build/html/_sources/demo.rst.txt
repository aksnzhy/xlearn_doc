xLearn Demo
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Copyright of the dataset belongs to the original copyright holder.

Criteo CTR Prediction
---------------------------

Predict click-through rates on display ads (`Link`__)

Display advertising is a billion dollar effort and one of the central uses of machine learning on the Internet. 
However, its data and methods are usually kept under lock and key. In this research competition, CriteoLabs is 
sharing a week’s worth of data for you to develop models predicting ad click-through rate (CTR). Given a user 
and the page he is visiting, what is the probability that he will click on a given ad?

You can find the data used in this demo in the path ``/demo/classification/criteo_ctr/``.

The follow code is the Python demo:

.. code-block:: python

   import xlearn as xl

   # Training task
   ffm_model = xl.create_ffm()
   ffm_model.setTrain("./small_train.txt")  
   ffm_model.setValidate("./small_test.txt") 
   param = {'task':'binary', 'lr':0.2, 
            'lambda':0.002, 'metric':'auc'} 

   ffm_model.fit(param, "./model.out")  

   # Prediction task
   ffm_model.setTest("./small_test.txt")  
   # Convert output to 0~1
   ffm_model.setSigmoid()
   ffm_model.predict("./model.out", "./output.txt")  

Mushroom Classification
---------------------------

This dataset comes from UCI Machine Learning Repositpry (`Link`__)

This data set includes descriptions of hypothetical samples corresponding to 23 species of gilled mushrooms in 
the Agaricus and Lepiota Family (pp. 500-525). Each species is identified as definitely edible, definitely poisonous, 
or of unknown edibility and not recommended. This latter class was combined with the poisonous one. The Guide clearly 
states that there is no simple rule for determining the edibility of a mushroom; no rule like *leaflets three, let it be*
for Poisonous Oak and Ivy.

You can find a small portion of data used in this demo in the path ``/demo/classification/mushroom/``.

The follow code is the Python demo:

.. code-block:: python

   import xlearn as xl

   # Training task
   linear_model = xl.create_linear()
   linear_model.setTrain("./agaricus_train.txt")
   linear_model.setValidate("./agaricus_test.txt")
   param = {'task':'binary', 'lr':0.2, 
            'lambda':0.002, 'metric':'acc', 
            'opt':'sgd'}

   linear_model.fit(param, './model.out')

   # Prediction task
   linear_model.setTest("./agaricus_test.txt")
   # Convert output to 0-1
   linear_model.setSigmoid()
   linear_model.predict("./model.out", "./output.txt")

Predict Survival in Titanic
-----------------------------

This challenge comes from the Kaggle. In this challenge, we ask you to complete the analysis of what sorts of people 
were likely to survive. In particular, we ask you to apply the tools of machine learning to predict which passengers 
survived the tragedy. (`Link`__)

You can find the data used in this demo in the path ``/demo/classification/titanic/``.

The follow code is the Python demo:

.. code-block:: python

   import xlearn as xl

   # Training task
   fm_model = xl.create_fm()
   fm_model.setTrain("./titanic_train.txt")
   param = {'task':'binary', 'lr':0.2, 
            'lambda':0.002, 'metric':'acc'}

   # Cross-validation
   fm_model.cv(param)

House Price Prediction
-----------------------------

This challenge comes from the Kaggle. The Ames Housing dataset was compiled by Dean De Cock for use in data science education. 
It's an incredible alternative for data scientists looking for a modernized and expanded version of the often cited Boston 
Housing dataset. (`Link`__)

You can find the data used in this demo in the path ``/demo/regression/house_price/``.

More Demo in xLearn is coming soon.

.. __: https://www.kaggle.com/c/criteo-display-ad-challenge
.. __: https://archive.ics.uci.edu/ml/datasets/Mushroom
.. __: https://www.kaggle.com/c/titanic
.. __: https://www.kaggle.com/c/house-prices-advanced-regression-techniques

 .. toctree::
   :hidden: