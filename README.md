## Table of Contents
1. [Overview](#overview)
2. [Observations and submissions](#submission)

### 01. Overview <a name='overview'></a>
You must do the project individually. In this HW you will design a backdoor detector for BadNets trained on the YouTube Face dataset using the pruning defense discussed in class. Your detector will take as input:
1. B, a backdoored neural network classifier with **N** classes.
2. Dvalid, a validation dataset of clean, labelled images.

What you must output is G a “repaired” BadNet. G has **N+1** classes, and given unseen test input, it must: 
1. Output the correct class if the test input is clean. The correct class will be in **[1,N]**.
2. Output class **N+1** if the input is backdoored.

You will design G using the pruning defense that we discussed in class. That is, you will prune the last convlution layer of BadNet $B$ (the layer just before the FC layers, it should has the pooling layer after) by removing one channel at a time from that layer. Channels should be removed in increasing order of average activation values over the entire validation set. Every time you prune a channel, you will  measure the new validation accuracy of the new pruned badnet. You will stop pruning once the  validation accuracy drops atleast X% below the original accuracy. This will be your new network B'. Now, your goodnet G works as follows. For each test input, you will run it through both B and B'. If the classification outputs are the same, i.e., class i, you will output class i. If they differ you will output **N+1**. Evaluate this defense on:
1. A BadNet, B1, (“sunglasses backdoor”) on YouTube Face for which we have already told you what the backdoor looks like. That is, we give you the validation data, and  also test data with examples of clean and backdoored inputs.

### 02. Observations
The underlying concept was to trim the convolution layer by considering the last average activation from pooling across the entire validation dataset. We therefore need to prune the conv_3 layer. As per the instructions mentioned, we need to save the model when the accuracy drops by at least {2%, 4%, 10%}. The saved models are titled model_X=2.h5, model_X=4.h5 and model_X=10.h5 for a drop in the 2%, 4% and 10% respectively.

The success rate of the attack is 6.954187234779596% when the accuracy decreases by at least 30%. During prune recording, we found our clean_accuracy (98.64899974019225) with an attack success rate of 100% went down to 0.0779423226812159 with 0% respectively. 
In creating a proficient Net, we had to amalgamate two models—the BadNet and the mended model. You can find the code in the kk5051_backdoor.ipynb file.

Observing the results, it becomes evident that the prune defense is not particularly effective in this scenario, as the attack success rate does not decrease significantly. While the attack success rate remains acceptable, it comes at the cost of a substantial reduction in accuracy. My assumption is that the attack method is immune to pruning, and the pruned model retains susceptibility to the poisoned data.



Instructions on running the code - </br>
- Make sure that there is enough memory available for the execution 
- The data set can be available from the link mentioned [here](https://github.com/csaw-hackml/CSAW-HackML-2020/tree/master/lab3) 


   
