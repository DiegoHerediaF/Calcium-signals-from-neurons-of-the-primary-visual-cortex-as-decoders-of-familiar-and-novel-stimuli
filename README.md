# Calcium signals from VIP and SST neurons of the primary visual cortex as decoders of familiar and novel visual stimuli 

2022 Neuromatch Academy (NMA) project on AllenSDK database by

- **Nicole A Gonzalez-Rangel**
- **Diego A Heredia-Franco**
- **Alejandra Lopez-Castro**
- **Francisco Millar-Santelices**
- **Sebastian Venegas**
- **Bruno Zorzet**

The following work aims to demonstrate whether, from the recording of the calcium activity of V1 cortex neurons in mice, a computational model capable of predicting the calcium dynamics of a novel or familiar image can be generated.

Discriminating between already recognized and novel visual stimuli and identifying them safe is essential for mammalian survival. How visual stimuli are encoded is therefore  fundamental to understanding how the brain interprets the inputs it receives from the world. During visual processing tasks, neurons in the primary visual cortex (V1) of mice constantly modulate their activity depending on the task and the context in which visual stimulus processing occurs. Among these, populations of VIP and SST neurons are key regulators of pyramidal neuron activity. Although the dynamics of these neural network in V1 cortex are not fully understood, there is evidence that these neurons markedly modify their activity during novel vs familiar image processing, which has been investigated by measuring calcium activity in mice performing familiar vs novel image discrimination tasks. Therefore, the following work aims to demonstrate whether, from the recording of the calcium activity of V1 cortex neurons in mice obtained from the AllenSDK database, a computational model capable of predicting whether the calcium dynamics of a novel or familiar image can be generated. Our methodological plan was based on filtering the database to obtain the VIP and SST neuronal populations of 13 mice tested with the timelines of the recordings and the calcium signal derived from the novel and familiar stimulus. Two depth planes were considered for the first analyses. We then defined the vector of experiments with the type of stimulus and the feature matrix with the fluorescence signal data. In order to model the probability of a discrete outcome given an input variable we used a logistic regression where in computing a training dataset we obtained an accuracy of 67% and in test an accuracy of 64.94%. This means that depending on the calcium signal, it is possible to obtain whether it is a familiar or novel stimulus. Further analysis is needed to support the results. However, so far we can state that our model is a good classifier to deal with this AllenSDK dataset. 
