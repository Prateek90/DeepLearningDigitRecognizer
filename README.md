# DeepLearningDigitRecognizer

**MNIST Data-Set**

The MNIST database is a subset of NIST database. It contains 60,000 training images and 10,000 images for testing.
The images present in MNIST dataset are size normalized, and the resulting images contain gray levels so these 
images can be used for training and testing with minimum preprocessing. The images are of 1 x 32 x 32. The 60,000 
training images can be broken down to 50,000 training images and 10,000 validation images as per the choice of the programmer

**Model Architecture**

The model being used to classify digits mainly consist of Feature Extractor followed by Linear Classifier

Image --> Feature Extractor --> Linear classifier --> Output

**Feature Extractor**

Generally Feature extractor can have many Convolution Modules, but as number of convolution modules grow so 
does number of trainable parameters, so number of modules should be chosen with care.

**Convolution Module:**

Image --> Convolution Layer --> Non-Linear Layer --> Pool Layer

Convolution layer is responsible for identifying different features of an input image like their can be 
identification of curves ,edges etc. In convolution layer neurons are connected to a local region of an
input image, each neuron will compute the dot product between their weights and the input region they
are connected to in an input space. The depth/number of filters(filter bank) in a convolution layer is an
hyper-parameter which should be chosen carefully.

The output volume from the Convolution layer is passed to Non-Linear layer that applies element-wise
activation function which converts the input from convolution layer into non-linear space by applying
non-linear activation function to it. This layer does not change the dimensions of the input from
convolution layer.

Pool layer works on the output from non-linear layer, it reduces the spatial size of representation of
images. This layer is responsible for reducing the number of parameters and computation in the
network which if not reduced can lead to overfitting.

**NOTE:**In our network we have applied two such Convolution modules, the first convolution module
operates directly on the input image and applies filters to it ,the second convolution module applies
filters to the output volume of the first convolution module ,application of second convolution module 
further refines the features extracted by the previous module and passes them to the linear classifier


**Linear Classifier**

Convolution phase is followed by linear phase in which output from the convolution phase is processed through 
Linear classifier. This linear classifier uses Error function to calculate error between actual output and 
obtained output, the output is calculated by applying an activation function on the values obtained from linear 
layer. Linear layer has set of trainable parameters that are trained using back-propagation algorithm, the 
weights obtained are used to classify the Input into different classes. The output from the linear layer indicates 
that to which category of the output classes does the input belong.

**Input to the Linear layer:**

The input to the linear layer comes from convolution layer and both layers are fully connected but the input 
dimensions are different are in 3D form, so they need to be reshaped in 2D matrix form before being processed 
through the linear layer.

**Loss function & activation function used in Digit Recognizer**

Loss function is responsible for determining the error between the actual output and the predicted output. The 
goal of the entire network is to minimize the loss function.

**Loss Function :** In our network we are using negative log likely-hood error function to determine error. 
**Activation Function :** The predicted output is obtained by applying softmax activation function to the
output from linear layer.

**ReLU()**

 We are using rectified Linear unit as our Non-linear function because ReLU function has range of  [0.infinity] , so 
 it can be used to model positive real numbers,apart from this benefit it also has the added advantage that the 
 gradient of ReLU does not vanish as we increase the input value.
 
**Drop-Out Layer**

We applied Drop-Out layer in our network after second convolution module,drop-out funtionn helps our network to 
generalize better by making some activations to zero with equal probablity while training .

**MODEL**

Neuron Combination                                   :       (64,64,128)
(Fist conv.Layer,Second Conv Layer,Linear Layer)

Receptive field of first conv.Layer Function,stride  :        (5 X 5 , 1)

Nonlinear Layer Function                             :        ReLU()

Pool Layer Receptive field,Stride                    :        (2 X 2 , 2)

Receptive field of second conv. Layer,Stride         :        (5 X 5 , 1)

Nonlinear layer Function                             :        ReLU()

Pool Layer Receptive field,Stride                    :        (2 x 2 , 2)

Accuracy on test Data                                :        99.24%
