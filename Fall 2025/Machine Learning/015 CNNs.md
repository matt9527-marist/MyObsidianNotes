The convolutional operation is given by:
$$H^{[filter]} = W^{[filter]} * X+b^{[filter]}$$
where 𝐗 is a matrix representing the pixels in a (height × 𝑤idth) arrangement.
In an image, this activation is a 2D object given by: $$A^{[filter]} = g(H^{[filter]})$$
and the resulting A is a feature map, one per filter. 

![[Pasted image 20251124160002.png]]

**Finding the Number of Parameters in a Convolutional Layer**
![[Pasted image 20251124160029.png]]
• The convolutional layer in the network shown in the figure above is a 4D tensor.  
• We start with a color figure with 3 input channels (RGB)  
• We assume a feature map of 5 features  
• And a filter of size 𝑚1 × 𝑚2  
• So, there are 𝑚1 × 𝑚2 × 3 × 5 parameters associated with the kernel.  
• Furthermore, there is a bias for each output feature map of the convolutional  
layer.  
• Thus, the size of the bias vector is 5.  
• Pooling layers do not have any (trainable) parameters; therefore, we can write the  
following: 𝑚1 × 𝑚2 × 3 × 5 + 5  

Example CNN Training:
```Python
model = Sequential()

#INPUT
model.add(Input(shape=(28, 28, 1)))

# CONVOLUTIONAL LAYER: Input (28x28x1) , Output (26x26x25)
model.add(Conv2D(filters=25, kernel_size=(3,3), activation='relu',))

# POOLING LAYER:  Input (26x26x25) , Output (13x13x25)
model.add(MaxPool2D(pool_size=(2, 2)))

# CONVOLUTIONAL LAYER:  Input (13x13x25) , Output (11x11x50)
model.add(Conv2D(filters=50, kernel_size=(3,3), activation='relu',))

# POOLING LAYER:  Input (11x11x50) , Output (5x5x50)
model.add(MaxPool2D(pool_size=(2, 2)))

# FLATTEN IMAGES: Input (5x5x50) , Output (1250)
model.add(Flatten())

# 100 NEURONS IN DENSE HIDDEN LAYER: Input (1250) , Output (100)
model.add(Dense(100, activation='relu'))

# LAST LAYER IS THE CLASSIFIER, THUS 10 POSSIBLE CLASSES: : Input (100) , Output (10)
model.add(Dense(10, activation='softmax'))

# https://keras.io/metrics/
model.compile(loss='categorical_crossentropy',
              optimizer='adam',
              metrics=['accuracy']) # we can add in additional metrics https://keras.io/metrics/
```

Further optimizations like regularization, dropout, and batch normalization can be applied to make the model training step more effective:
```python 
model = Sequential()

    model.add(Input(shape=X_train[0].shape,))
    model.add(Conv2D(filters=32, kernel_size=(3,3), activation='relu',padding='same'))
    model.add(BatchNormalization())
    model.add(Conv2D(filters=32, kernel_size=(3,3),activation='relu',padding='same'))
    model.add(BatchNormalization())
    model.add(MaxPool2D(pool_size=(2, 2)))
    model.add(Dropout(0.2))
    #Use this line to check the output shape of the model
    print('Output shape check#1:', model.compute_output_shape(input_shape=tuple([None] + list(X_train[0].shape))))

    model.add(Conv2D(filters=64, kernel_size=(3,3),activation='relu',padding='same'))
    model.add(BatchNormalization())
    model.add(Conv2D(filters=64, kernel_size=(3,3),activation='relu',padding='same'))
    model.add(BatchNormalization())
    model.add(MaxPool2D(pool_size=(2, 2)))
    model.add(Dropout(0.2))
    #Use this line to check the output shape of the model
    print('Output shape check#2:', model.compute_output_shape(input_shape=tuple([None] + list(X_train[0].shape))))

    model.add(Conv2D(filters=128, kernel_size=(3,3),activation='relu',padding='same'))
    model.add(BatchNormalization())
    model.add(Conv2D(filters=128, kernel_size=(3,3),activation='relu',padding='same'))
    model.add(BatchNormalization())
    model.add(MaxPool2D(pool_size=(2, 2)))
    model.add(Dropout(0.2))
    #Use this line to check the output shape of the model
    print('Output shape check#3:', model.compute_output_shape(input_shape=tuple([None] + list(X_train[0].shape))))

    model.add(GlobalMaxPooling2D())
    #Use this line to check the output shape of the model
    print('Output shape after GlobalMaxPooling:', model.compute_output_shape(input_shape=tuple([None] + list(X_train[0].shape))))

    model.add(Flatten())
    model.add(Dropout(0.2))
    model.add(Dense(512, activation='relu'))
    model.add(Dropout(0.2))
    model.add(Dense(num_classes, activation='softmax'))
```

## Pretrained Models and Transfer Learning 
If we have something that is capable of learning images in general, can we use that tool to learn our own images or our particular problem? 

Perhaps we can use the pretrained models of VGG-16 or ResNet-50, lifting their functionality to predict a different set of images? That way, instead of building the full CNN for feature extraction, we can use the ResNet model as our convolutional layer, feeding the output into a dense neural network to give the final results. 

There are many pretrained models offered by Keras and by a major hub called *HuggingFace.* 



