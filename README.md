## Requirements
This code has been tested with
- python 3.8
- tensorflow 2.11.0
- CUDA 11.6

## Installation
```
pip install tensorflow opencv-python autolab_core tqdm
```
## Evaluation
Evaluate the results of DualPoseNet reported in the paper:

```
python eval.py
```
## Data Preparation

Download the data provided by [NOCS](https://github.com/hughw19/NOCS_CVPR2019) ([real_train](http://download.cs.stanford.edu/orion/nocs/real_train.zip), [real_test](http://download.cs.stanford.edu/orion/nocs/real_test.zip),
[ground truths](http://download.cs.stanford.edu/orion/nocs/gts.zip),
and [mesh models](http://download.cs.stanford.edu/orion/nocs/obj_models.zip)), and unzip them in the folder ```data/``` as follows:

```
data
├── CAMERA
│   ├── train
│   └── val
├── Real
│   ├── train
│   └── test
├── gts
│   ├── val
│   └── real_test
└── obj_models
    ├── train
    ├── val
    ├── real_train
    └── real_test
```

Run the following scripts to prepare training instances:

```
cd provider
python training_data_prepare.py
```

## Training

Command for training DualPoseNet:
```
python main.py --phase train --dataset REAL275
```
The configurations can be modified in ```utils/config.py```.

## Testing
Command for testing DualPoseNet without refined learning:
```
python main.py --phase test --dataset REAL275
```

Command for testing DualPoseNet with refined learning:
```
python main.py --phase test_refine_encoder --dataset REAL275
```

We also provider another faster way of refinement by directly finetuning the pose-sensitive features:
```
python main.py --phase test_refine_feature --dataset REAL275
```

The configurations can also be modified in ```utils/config.py```.