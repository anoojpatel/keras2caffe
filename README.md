# Keras2Caffe

This is a script that takes Keras models and builds caffe models
from the common Keras layers into caffe NetSpecs, and into prototext files.
This allows you to pipe directly into your favorite Caffe framework of choice.

Be aware that Keras has much more flexible functionality and thus will miss
lots of goodies such as Lambda functions, some acitvaiton functions, and some 
of the pooling, text preprocessing, recurrent, and noise layers. For those you
can try your luck with [custom python layers](https://stackoverflow.com/questions/33778225/building-custom-caffe-layer-in-python) or [custom c++ layers](https://github.com/BVLC/caffe/wiki/Development).

This is build with a very simple structure of parsing layer by layer, and the 
same goes for caffe weights.

### Why
For anyone who needs to use Caffe for some reason.
This was a script I wrote while at IBM Watson, in Spark.tc for Keras2DML
to run Common pretrained keras models to run on large clusters. This was partly used to piggy back off Caffe2DML. Definitely recommend checking out [SystemML](https://github.com/apache/systemml) if you want to train models on clusters and 
distributed machine learning concepts in general. 

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

What things you need to install the software and how to install them

```
sudo apt-get install caffe
pip install tensorflow keras
```
 Eventually I will add Caffe.proto to generate files so you don't get bloated
 from the caffe dependency.
 
### Installing

A step by step series of examples that tell you have to get a development env running

Import the script to use the functions

```
import keras2caffe
```

## Things That Work and What Needs To

Currently the layers that work are:
* Dense
* Dropout
* Add, Multiply, Maximum, and Concat
* Conv2D, MaxPooling2D, Conv2DTranspose(Does not map anything that doesn't exist in Caffe, such as regulaizers, and intiallizers)
* All activations in Caffe except Threshold, bias, and Scale
* All Losses in Caffe, including both combined activation and loss layers

Things that I need to add
* LSTM (Map as much as possible with keras parameters)
* Crop, AveragePooling, and Embedding

If I missed anything, make sure to inform me so I can add it, or merge pull requests.

REMINDER: You can't get one to one models, so don't expect everything to work perfectly!

## Authors

* **Anooj Patel** - *Initial work* - [PurpleBooth](https://github.com/FuturizeHandgun)


## License

This project is licensed under the MIT License 

## Acknowledgments

* Mike
* Caffe for making it a game to find valid documentation for pycaffe
