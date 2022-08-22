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
