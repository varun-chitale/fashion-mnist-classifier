# fashion-mnist-classifier
Classifying images from Zalando's fashion-mnist dataset using minimum labeled samples and a threshold accuracy
---

Hi!
Here’s the problem statement I chose:

---
### Task 3 (DS/ML)

In most real-world applications, labelled data is scarce. Suppose you are given
the Fashion-MNIST dataset (https://github.com/zalandoresearch/fashion-mnist), but without any labels
in the training set. The labels are held in a database, which you may query to
reveal the label of any particular image it contains. Your task is to build a classifier to
>90% accuracy on the test set, using the smallest number of queries to this
>database. 

You may use any combination of techniques you find suitable
(supervised, self-supervised, unsupervised). However, using other datasets or
pre-trained models is not allowed. 

---

## Solution

## Optimization Update:

I had to use only 10% of the data for getting 90% accuracy. That is 6000 samples.
I decided to use only **5999** ;)

Here are the steps that got the final accuracy of **90.13%**

1. Retraind autoencoder on 200 epochs -> improved embeddings for the images.
2. Reduced validation sets in both models -> gave more training data.
3. Changed model arch(layers, #neurons) for the classifier model -> more improvements
4. Set the initial layers in classifer to trainable -> more improvements
5. Tweaked #epochs for model two -> no use in wasting time, is there?
6. Optimised params(batch size, optimizer, activation functions) -> more improvements

Et voila, accuracy threshold reached.

In case the above wouldn't have worked, I would have:
1. Hand selected samples based on classification report. More samples for shitty classes and vice versa.
2. Data augmentation: this would've required retraining the autoenc which takes a lot of time.
3. Replaced the classifier altogether -> also needs time.

Closing thoughts:
1. This was a fun assignment. More improvements are possiible but they need time, is all.

---
After some literature review, I narrowed my solution down to this basic workflow:
1. Identify features from the training data w/o using labels
2. Use a stacked approach and use minimal labels to classify with the accuracy threshold of 0.9

For #1, I built an auto encoder that seemed to be working really well in understanding the data and generating the best possible latent space with minimal efforts with regards to param/hyper parameter tuning.

For #2, I considered unsupervised approaches like classifying based on clustering algorithms, like k-means. The cluster centroids would be the classes(there are 10 in total). However, this would be the best case scenario. I would have had to work out a lot of things to get the accuracy right, and this model does not give me the leeway to experiment (fast).

Based on some research ([Fashion-MNIST Benchmark (Image Classification) | Papers With Code](https://paperswithcode.com/sota/image-classification-on-fashion-mnist)), the best models have the accuracy of 96.91, so this wouldn’t have been an easy task.

I chose to train a neural net classfier on top of the auto encoder and see the number of samples it took to get to the accuracy threshold. The results are surprising (in a good way). The notebook contains additional details of the approach. 

Basic flow looked like this:
1. Train an auto-encoder to learn the image data (we don’t use labels here)
2. Pack a new network with encoder layer from #1 and a simple classfier model on top.
3. Iterate with different number of samples for #2 to find the best possible “n” that gives the needed accuracy.
4. Discuss/visualize more details.

The results for #3 can be viewed [here](./results.txt), as well as in the main [notebook](./notebook.ipynb).

### Notes:
1. I included the models trained by me so that you don’t have to train again. You can simply load the relevant model and execute the cells you wish to test.
2. In #2 of the above code, a lot of experimentation can be done, I chose a model and went ahead with it. DeepNets are known to work better for certain kinds of use-cases: this one is the prime example. I’m sure some simpler models can also produce comparable results.
