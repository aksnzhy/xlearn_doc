Large-Scale Machine Learning
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This page shows how to use xLearn to solve large-scale machine learning problems. 
In recent years, challenges arise with the fast-growing data. For "big-data", we focus
on datasets with potentially trillions of training examples, which cannot fit into the 
memory of a single machine. Motivated by this, we design xLearn to solve large-scale 
machine learning problems. First, xLearn can handle very large data (TB) on a single PC 
by using *out-of-core* learning. In addition, xLearn can scale beyond billions of example
across many machines to support distributed learning by using the *parameter server* framework.

Out-of-Core Learning
--------------------------------

*Out-of-core* leanring refers to the machine learning algorithms working with data cannot fit into 
the memory of a single machine, but that can easily fit into some data storage such as local hard disk
or web repository. Your available RAM, the core memory on your single machine, may indeed range from a few 
gigabytes (sometimes 2 GB, more commonly 4 GB, but we assume that you have 2 GB at maximum) up to 256 GB on 
large server machines. Large servers are like the ones you can get on cloud computing services such as Amazon 
Elastic Compute Cloud (EC2), whereas your storage capabilities can easily exceed terabytes of capacity using 
just an external drive (most likely about 1 TB but it can reach up to 4 TB).

Actually, the ability to learn incrementally from a mini-batch of instances is key to *out-if-core* learning as
it gurantees that at any given time there will be only a small amount of data in the main memory. Choose a good
size for the mini-batch that balances relevancy and memory footprint could involve some tuning.

.. image:: ./images/out-of-core.png
    :width: 500   

Distributed Learning
--------------------------------

The distributed training guide is coming soon.