# ddmd_runs
Example data for testing individual stage of DeepDriveMD

## 6000 frames
BBA dataset is used to capture 6000 frames of point clouds, and the repo size of `6000frames` sub-directory is about 234MB.
Training/Inference settings can be adjusted via a yaml configuration file at the time of running a stage script e.g., `train.py` or `lof.py`.

## Intermediate Files for Each Stage

### `molecular_dynamic_runs`
OpenMM simulation output are stored with each task id like `taskXXXX` directory name.
- `.dcd`: trajectory file (will be required to locate a particular frame at the `agent` stage)
- `.h5`: hdf5 file to store training samples i.e., `point_cloud` and `contact_map`. `rmsd` and `fnc` additional info are also stored for the anlaysis. Aggregation stage keeps these info but concatenating them all in a single file pointer.
- `.log`: standard output message of OpenMM
- `.pdb`: reference protein database file

### `machine_learning_runs`
PyTorch output are stored including checkpoints, embeddings, hyperparams and weights.
- `checkpoint`: each epoch saved with date and index in a filename
- `embeddings`: each epoch saved with date and index in a filename
- `loss.json`: loss value
- `*-hparams`: hyperparameters
- `*-weights.pt`: weights
- `virtual-h5-metadata.json`: list of actual h5 files to load and build a single hdf5 dataset pointer

### `agent_runs`
Agent output are stored, for example, `lof.py` finds a new location to resume MD simulation. sklearn.neighbors.LocalOutlierFactor is used to calculate intrinsic_score/extrinsic_score.
`virtual*`: metadata stored to build a single hdf5 dataset pointer

# Environment Setup (TBD)

- `conda install pytorch==1.12.0 torchvision==0.13.0 torchaudio==0.12.0 cudatoolkit=11.3 -c pytorch`
- `conda install -c conda-forge scikit-learn`
- `conda install -c conda-forge hdf5`
- `conda install -c conda-forge mpi4py`
- `conda install -c conda-forge wandb`
- `conda install -c conda-forge matplotlib`
- `pip install MDAnalysis`
