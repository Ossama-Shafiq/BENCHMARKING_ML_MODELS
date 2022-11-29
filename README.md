# Benchmarking ML models for ADME properties of drugs/druglike compounds

Here we have a notebook containing a function that streamlines benchmarking for random forest (rf), graph neural network (GNN) known as message passing neural network (MPNN) and a transformer.
The Deeplearning library [DeepPurpose](https://deeppurpose.readthedocs.io/en/latest/) is leveraged here for the transformer encoder and MPNN.

By going through the notebook "benchmark_graph_random_forest_and_transformer.ipynb" you can apply the three algorithms to the four available datasets the first three datasets pertaining to absoroption,distribution and metabolism will produce plots and scores such such as AUROC as they are a binary classification task whereas the last dataset on excretion is a regression task so its metric of evaluation is focused on the mean squared error,

Datasets are acquired from [Therapeutics Data Commons(TDC)](https://tdcommons.ai/). For use with the classical random forest extra steps had to be employed - the molecular fingerprints (descriptors) were computed using [padelpy](https://github.com/ecrl/padelpy).

## Datasets from TDC that were utilised
* Absorption - Pgp (P-glycoprotein) Inhibition 
* Distribution - BBB (Blood-Brain Barrier)
* Metabolism - CYP P450 1A2 Inhibition
* Excretion - Clearance, AstraZeneca

## Computing Molecular Descriptors
***
For using padelpy the following points are to be noted:
* Install padelpy following this [link](https://pypi.org/project/padelpy/)
* Java runtime enviroment must be installed [JRE](https://www.java.com/en/download/manual.jsp) 
* a Zip file has been uploaded to this git repo which contains the information for the 12 different molecular fingerprints
* Refer to notebook "prepping_for_finger_print_rf.ipynb" for example of how finger prints were computed also the data was taken from DeepPurpose module and converted to csv then used in this notebook

## DeepPurpose installation
***
Pointers for installing DeepPurpose:
* Please follow this [link](https://deeppurpose.readthedocs.io/en/latest/notes/download.html) to install DeepPurpose 
* DeepPurpose utilises python verions 3.6 and 3.7
* If you face a persistent error from pytorch in regards to DLL error please try this `conda install -c defaults intel-openmp -f`


## Results from running the algorithms on the datasets
***

For Absorption (1218 drugs) rf was the best performing:
* MPNN had an AUROC: 0.66
* Tranformer had an AUROC: 0.79
* rf had an AUROC: 0.82

For Distribution (2030 drugs) rf was the best performing:
* MPNN had an AUROC: 0.70
* Tranformer had an AUROC: 0.80
* rf had an AUROC: 0.84

For Metabolism (12579 drugs) MPNN was the best performing:
* MPNN had an AUROC: 0.84
* Tranformer had an AUROC: 0.68
* rf had an AUROC: 0.66

For Excretion (1213 drugs) Transformer had the best performance: 
* MPNN had an MSE: 2317.86
* Tranformer had an MSE: 2289.21
* rf had an MSE: 2822.81

It seems as the datasets get really large the Transformer and MPNN seem to surpass the random forest model for better predictions. The random forest performs reasonably well with lower sample sizes.

It is suggested that the forest/tree models excel at smaller sample sizes with structured data whereas the deep net models outshine the tree models at larger sample sizes of structured data.
