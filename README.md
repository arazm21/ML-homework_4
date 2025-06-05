# ML-homework_4

this is the final homework of the course, where we had to train a bunch of different models on the fer2013 expression recognition dataset.

i incorporated a bunch of different ideas and i am goin gto explain them.

first, i started with a bunch of very simple convolutional networks, with pooling and relu for the activation layers and to downsample.
i tried many different such models and they mostly had the same problems - they very quickly got to a certain loss and then the validation accuracy would stay still, while the train went up and up. this is an obvious case of overfitting.
the loss would get stuck at around 0.42.

therefore, the next step was to increase the size and complexity of my models. the result was mostly the same, the validation accuracy was just a bit better, up to over 0.53

I had to look for different architectures. the model I named BeefyModel was not very interesting, but it did give me the best results. it consists of a convolutional layer to increase the dimentions in the beginning, after that some residual blocks, and linear leayers with batchnorm in the end.
each residual block consists of convolutional layer -> batch norm -> relu -> conv -> batch norm. after that a residual gets added, and we use an activation function, dropout and return that. this model was far better than the previous ones.
i had this model with several different small variations with size and structure, with variying levels of success. you can see all of them in wandb.

next i tried some more common architectures. resnet was the first one attempted. i believe that because of our pictures being so small, resnet could not pick up on the details, therefore did not yeild great results.
next i tried GoogLeNet. the main quirk is that it uses 4 parallel layers of different kernel sizes, one even improves a pooling with a convolution, and adds it all at the end. the advantage of this is that it manages to detect more different features, but again the simple previous attempts gave slightly more solid results. i got up to over 0.52 without too much overfitting so it was a moderate success.

after that, i attempted a more compicated resnet architecture. i addded a few more linear layers and some more normalisation ways, i got to 0.56 but not much better. looking at the weights, i believe that reducing the learning rate could have resulted in a much better result, as the weights are not very well distibuted, but did not have the time to test that.

i also tried various different flavors of vision transformers. you can find them ind the 3 cells they take up, totaling over 5 attempted architectures.

i really liked the GoogLeNet idea, and wanted to make it work. i got one model from the internet, which was faithful to the original design, but that was no good for this case. i also modified and added auxiliary connections, more normalisation and dropout and got 0.59, which was quite good.

you can see all of them in my wandb experiments

a mistake i was making in the beginning was that I was not upsampling the data, which gave me quite poor results. the first few experiments show that clearly. towards the end, the results become much better as i did implement that. also, at some point along the way i accidentally deleted wandb.watch, so one some occasions the weights may not be visible.
the best result i could achieve was roughly 0.62 validation and 0.65 train.
