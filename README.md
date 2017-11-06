CapsNet-Fashion-MNIST
Capsule Network for classification of MNIST Fashion dataset.

Capsule Network is made on the basis of [this](https://arxiv.org/pdf/1710.09829.pdf) paper by Geoffrey E. Hinton.

The model is trained on Fashin MNIST dataset. Fashion-MNIST is a dataset of Zalando's article images—consisting of a training set of 60,000 examples and a test set of 10,000 examples. Each example is a 28x28 grayscale image, associated with a label from 10 classes. Zalando intends Fashion-MNIST to serve as a direct drop-in replacement for the original MNIST dataset for benchmarking machine learning algorithms. It shares the same image size and structure of training and testing splits.

Download the dataset [here](https://www.kaggle.com/zalando-research/fashionmnist/data)!

```
Layer (type)                     Output Shape          Param #     Connected to                     
====================================================================================================
input_1 (InputLayer)             (None, 28, 28, 1)     0                                            
____________________________________________________________________________________________________
conv1 (Conv2D)                   (None, 20, 20, 256)   20992       input_1[0][0]                    
____________________________________________________________________________________________________
primarycap_conv2d (Conv2D)       (None, 6, 6, 256)     5308672     conv1[0][0]                      
____________________________________________________________________________________________________
primarycap_reshape (Reshape)     (None, 1152, 8)       0           primarycap_conv2d[0][0]          
____________________________________________________________________________________________________
primarycap_squash (Lambda)       (None, 1152, 8)       0           primarycap_reshape[0][0]         
____________________________________________________________________________________________________
digitcaps (CapsuleLayer)         (None, 10, 16)        1486080     primarycap_squash[0][0]          
____________________________________________________________________________________________________
input_2 (InputLayer)             (None, 10)            0                                            
____________________________________________________________________________________________________
mask_1 (Mask)                    (None, 16)            0           digitcaps[0][0]                  
                                                                   input_2[0][0]                    
____________________________________________________________________________________________________
dense_1 (Dense)                  (None, 512)           8704        mask_1[0][0]                     
____________________________________________________________________________________________________
dense_2 (Dense)                  (None, 1024)          525312      dense_1[0][0]                    
____________________________________________________________________________________________________
dense_3 (Dense)                  (None, 784)           803600      dense_2[0][0]                    
____________________________________________________________________________________________________
out_caps (Length)                (None, 10)            0           digitcaps[0][0]                  
____________________________________________________________________________________________________
out_recon (Reshape)              (None, 28, 28, 1)     0           dense_3[0][0]                    
====================================================================================================

```
Network Adapted from [Xifeng Guo](https://github.com/XifengGuo/CapsNet-Keras).
