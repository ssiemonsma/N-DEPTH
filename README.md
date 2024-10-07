# N-DEPTH: Neural Depth Encoding for Compression-Resilient 3D Video Streaming
[Paper](https://www.mdpi.com/2079-9292/13/13/2557) | [Research Lab](https://www.holorealitylab.com/)

This repository contains the training code for N-DEPTH (Neural Depth Encoding for Compression-Resilient 3D Video Streaming), as described in the paper "N-DEPTH: Neural Depth Encoding for Compression-Resilient 3D Video Streaming" by Stephen Siemonsma and Tyler Bell.

## Overview

N-DEPTH is a novel neural depth encoding method optimized for lossy compression codecs to efficiently encode depth maps into 24-bit RGB representations. This repository provides the training code in the form of a Jupyter notebook, along with an Anaconda environment file for easy setup.

## Requirements
- Anaconda or Miniconda
- [FlyingThing3D dataset disparity maps](https://lmb.informatik.uni-freiburg.de/resources/datasets/SceneFlowDatasets.en.html)
- NVIDIA GPU (other configurations untested)

## Setup
```
conda env create --name ndepth --file=environment.yml
conda activate ndepth
jupyter-notebook N-DEPTH_training_notebook.ipynb
```
Inside of the training notebook under the "Configuration" section, you must set config.dataset_path to the parent directory where you have unpacked the FlyingThings3D disparity maps.
All of the other configuration variables are pre-set to reasonable default corresponding to the results of the journal publication.
The N-Depth network can be trained by running the entire notebook (i.e., Run -> Run All Cells).
For long, unattended training sessions, I would encourage the use of Papermill with a command such as the following:
```
papermill N-DEPTH_training_notebook.ipynb N-DEPTH_training_notebook.ipynb --inject-input-path --request-save-on-cell-execute --no-progress-bar --autosave-cell-every 60
```
The training notebook will be update in-place every 60 seconds and can be inspected in Jupyter Notebook or Jupyer Lab.
The output can be saved to a different notebook by choosing an alternative file name for the second [Papermill](https://github.com/nteract/papermill) argument.

The training script will generate checkpoint files in a "weights" directory and TensorBoard logs in a "TensorBoard_logs" directory.
An "images" directory will also be created and populated with lossless depth-to-RGB encodings.
These encodings are in the form of 100x100 PNGs which show the depth-to-RGB mapping at various points of the training session.
If the elements of "neural_encoding_for_ones_mask" images are plotted row-wise with 3D axes corresponding to the red, green, and blue pixel values, helical encoding structures will be evident as the network nears convergence.
When these plots are animated over the training duration, [videos such as this supplementary video](https://zenodo.org/records/11399505/files/N-DEPTH-RGB-15s.mp4) from the journal publication can be generated.

## Citation

If you use this code in your research, please cite our paper:
```
@Article{electronics13132557,
  AUTHOR = {Siemonsma, Stephen and Bell, Tyler},
  TITLE = {N-DEPTH: Neural Depth Encoding for Compression-Resilient 3D Video Streaming},
  JOURNAL = {Electronics},
  VOLUME = {13},
  YEAR = {2024},
  NUMBER = {13},
  ARTICLE-NUMBER = {2557},
  URL = {https://www.mdpi.com/2079-9292/13/13/2557},
  ISSN = {2079-9292},
  DOI = {10.3390/electronics13132557}
}
```
