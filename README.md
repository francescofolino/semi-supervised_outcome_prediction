# Readme

This repository contains the Python code for replicating the experimental study presented in [1], where an approach to the discovery of DNN-based process-outcome predictors was proposed in the challenging scenario where only small amounts of labeled process traces are available. The code was applied to the preprocessed process logs employed in [2] and made available [here](https://github.com/irhete/stability-predictive-monitoring).  

For the sake of usability, the code has been split into two packages: *source_code_SSOP-MTL.zip* and *source_code_SSOP-PT.zip*. 

The rest of this document is meant to serve as a quick user guide for running the code over each of the logs considered in [1]. At the end of each run, two kinds of artifacts are produced for a discovery method: (i) the outcome-prediction model discovered by the method for different views of the log (these views differ in the fraction of visible outcome-class labels), and (ii) a CSV file reporting the accuracy scores obtained by the discovered model on different log views.

## How to run an experiment on a given log
The procedure for replicating an experiment depends on which specific discovery method is being used. In order to reduce friction in the usage of our code, some convenient Python calls are provided. To see hints on how to correctly use the command lines below, you may simply invoke any of them with the option `--help`.  

### Method *SSOP-MTL*
1. Use the code included in package *source_code_SSOP-MTL*.
2. Put one of the logs (in the zip archive *event_logs.zip*) into your local folder `/logdata`; let `name_log` be the name of the selected log.
3. Execute the command line 

	> `python3 BuildLog_main.py -log name_log`

	 to build the tensors for the log with name `name_log`; the tensors will be saved into the local folder `/output_files/input_tensors`.
4. Execute the command line: 

	> `python3 BuildPredictionModel_main.py -log name_log`

	 to discover a prediction model for the log named `name_log`; the prediction model will be saved (as a “.h5” file) in folder `/output_files/models/prediction_models`, while its accuracy scores will end up into the local folder `/results/predictive_models` in the form of CSV file.

### Methods *SSOP-PT* and *BASE-FE*
1. Use the code included in package *source_code_SSOP-PT*;
2. Put one of the logs (in the zip archive *event_logs.zip*) into your local folder `/logdata`; let `name_log` be the name of the selected log.
3. Execute the command line: 

	> `python3 BuildLog_main.py -log name_log`

	 to build the tensors  for the log named `name_log`; the tensors will be saved into the local folder `/output_files/input_tensors`.
5. Execute the command line: 

	> `python3 BuildSourceModel_main.py -log name_log`

	 to train a preliminary "source" outcome-prediction model for both methods *SSOP-PT* and *BASE-FE* over the log named `name_log`; the model will be saved (as a “.h5” file) in the local folder `/output_files/models/source_models`;
6. Execute the command line: 

	> `python3 BuildPredictionModel_main.py -log name_log`

	 to train a "fine-tuned" outcome-prediction model for both *SSOP-PT* and *BASE-FE* over the log named `name_log`; these models will be saved (as a “.h5” file) in the local folder `/output_files/models/prediction_models`, while its accuracy scores will end up into the local folder `/results/predictive_models`in the form of a CSV file.

### Method *BASE-S* (baseline)
1. Use the code included in the package *source_code_SSOP-PT*;
2. Put one of the logs (in the zip archive *event_logs.zip*) into your local folder `/logdata`; let `name_log` be the name of the selected log.
3. Execute the command line: 

	> `python3 BuildLog_main.py -log name_log`

	 to build the tensors for the log named `name_log`; the tensors will be saved in the local folder `/output_files/input_tensors`.
4. Execute the command line: 

	> `python3 BuildBaseline_main.py -log name_log` 

	to train an outcome-prediction model (in a fully-supervised way) over the log named `name_log`; the model will be saved (as a “.h5” file) in the local folder `/output_files/models/baseline_models`, while its accuracy scores will end up into the local folder `/results/baselines` in the form of a CSV file.

## References
[1] Francesco Folino, Gianluigi Folino, Massimo Guarascio, Luigi Pontieri. *Semi-Supervised Discovery of DNN-based Outcome Predictors from Scarcely-Labelled Process Logs*. **Business & Information Systems Engineering** (2022)

[2] I. Teinemaa, M. Dumas, A. Leontjeva, and F. M. Maggi. *Temporal stability in predictive process monitoring*. Data Min. Knowl. Discov., 32(5):1306–1338 (2018)
