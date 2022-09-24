# Calcium signals from VIP and SST neurons of the primary visual cortex as decoders of familiar and novel visual stimuli 

2022 Neuromatch Academy (NMA) project on AllenSDK database by

- **Nicole A Gonzalez R**
- **Diego A Heredia F**
- **Alejandra Lopez C**
- **Francisco Millar S**
- **Sebastian Venegas**
- **Bruno Zorzet**

## Description

Discriminating between already recognized and novel visual stimuli and identifying them safe is essential for mammalian survival. How visual stimuli are encoded is therefore  fundamental to understanding how the brain interprets the inputs it receives from the world. During visual processing tasks, neurons in the primary visual cortex (V1) of mice constantly modulate their activity depending on the task and the context in which visual stimulus processing occurs. Among these, populations of VIP and SST neurons are key regulators of pyramidal neuron activity. Although the dynamics of these neural network in V1 cortex are not fully understood, there is evidence that these neurons markedly modify their activity during novel vs familiar image processing, which has been investigated by measuring calcium activity in mice performing familiar vs novel image discrimination tasks. Therefore, the following work aims to demonstrate whether, from the recording of the calcium activity of V1 cortex neurons in mice obtained from the AllenSDK database, a computational model capable of predicting whether the calcium dynamics of a novel or familiar image can be generated.

## Question
- ¿Can the calcium trace of VIP and SST neurons allow to discriminate between familiar and novel stimuli?

- ¿How do calcium signals from VIP, SST neurons combine in the mouse visual cortex allow to differentiate familiar from novel stimuli?

- ¿Which parts of the fluorescence signal are most important for predicting the type of stimulus presented?

## Hypothesis

We hypothesize that the fluorescence values of the VIP, SST neuronal populations are non-linearly related to the type of novel or familiar image presented, and that a  binary logistic regression is an excellent model to classify the outcome of our dependent variable (i.e. the type of image by means of calcium activity data).

## Methods

Our methodological plan was based on filtering the [AllenSDK dataset](https://doi.org/10.1038/s41593-019-0550-9) to obtain the VIP and SST neuronal populations (10666 neurons) of 13 mice, obtaining the time series of calcium fluorescence signals recorded while the mice did a visual adaptation task using either familiar or novel images. Two depth planes were considered for the first analyses, and we took the traces at the stimulus presentation until 0.750 seconds later.

## Model

The calcium activity at a given timestamp was organized in a feature matrix $X$, according its cre line (VIP or SST) and the stimulus presented. Let $Y$ be the type of stimulus (**0**: novel, **1**: familiar), and $X$ be the calcium signal of a given neuronal population after the stimulus is presented, then $Y = f(\Theta X)$, and in order to model the probability of a discrete outcome given an input variable, we used a logistic regression in a training dataset.

## Results

We used cross-validation to calculate the accuracy of the models and compute the probabilities of obtaining this accuracy in a random distribution, so as to determine how reliable they are. For the VIP Model the accuracy is 79.42%, and for the SST Model, the accuracy is 78.29%, both with a probability of less than 0.001 of it being by chance.

![image](https://github.com/DiegoHerediaF/Calcium-signals-from-neurons-of-the-primary-visual-cortex-as-decoders-of-familiar-and-novel-stimuli/blob/3971ee2d0f34e516096c0285265d67a7aa1fe33f/Figures/cross_validation_SST.png)
![image](https://github.com/DiegoHerediaF/Calcium-signals-from-neurons-of-the-primary-visual-cortex-as-decoders-of-familiar-and-novel-stimuli/blob/3971ee2d0f34e516096c0285265d67a7aa1fe33f/Figures/cross_validation_VIP.png)

**Figure 1.** Cross-validation accuracy for SST and VIP neuron populations in the mice primary visual cortex.

Now, to visualize the “importance” assigned by our model to each temporal feature. we plotted the weight values $\Theta$ against the features, see **figure 2**. According to this, the model mainly uses time features close to the stimulus window for both VIP and SST populations, highlighting the temporality of visual processing. It also appears that the VIP and SST weights tend to be inverted with respect to each other. This makes sense considering the network, that is, VIP neurons tend to fire in favor of new stimulus whereas SST fires in response to “older” stimulus. It is also interesting to note that after the stimulus, the weights of both populations tend to progressively decrease, and even change signs. Hence, the initial perturbation seems to have repercussions well beyond its time frame.

![image](https://github.com/DiegoHerediaF/Calcium-signals-from-neurons-of-the-primary-visual-cortex-as-decoders-of-familiar-and-novel-stimuli/blob/3971ee2d0f34e516096c0285265d67a7aa1fe33f/Figures/pesos.png)

**Figure 2.** Weights $\Theta$ associated with each temporal feature and neuronal population, obtained from the logistic regression model.

Finally, just to give a more global perspective of the data we worked with, and as a way to visualize the behavior of the linear part of the model, and have an idea on how this part classifies the two different stimuli before applying the nonlinear part, see **figure 3**, there you can see on the right, for the VIP and SST populations when a novel (in yellow) and a familiar (in purple) stimulus were presented, the cumulative sum of the mean signals, multiplied by the model parameters associated with each time, as a function of the time interval considered.  

These plots are interesting, because it can be observed that, as the time interval increases, the curves separate from each other more for the SST than the VIP neurons; or in other words, the averages of the cumulative sums for the novel and familiar signals fall outside the standard deviation estimated from the data of the other image type presented. So, as a future perspective, it would be interesting to study how the accuracy of the model behaves as the time interval increases (more stimuli are presented), as well as when we take only the time intervals where the stimuli were shown. 

![image](https://github.com/DiegoHerediaF/Calcium-signals-from-neurons-of-the-primary-visual-cortex-as-decoders-of-familiar-and-novel-stimuli/blob/3971ee2d0f34e516096c0285265d67a7aa1fe33f/Figures/cumulative_SST.png)
![image](https://github.com/DiegoHerediaF/Calcium-signals-from-neurons-of-the-primary-visual-cortex-as-decoders-of-familiar-and-novel-stimuli/blob/3971ee2d0f34e516096c0285265d67a7aa1fe33f/Figures/cumulative_VIP.png)

**Figure 3.** Cumulative sum of the mean VIP and SST signals, multiplied by the model parameters associated with each time, as a function of the time interval considered.
