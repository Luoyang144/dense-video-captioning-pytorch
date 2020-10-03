# Event Sequence Generation Network
**Unoffical** re-implementation of Event Sequence Selection Network (ESGN) in paper titled "[streamlined dense video captioning](https://arxiv.org/abs/1904.03870v1)". Note that we do not adopt SST to encode the proposal-level features, which is different from the original model. 

# Environment
1. Python 3.6.2
2. CUDA 10.0, [PyTorch 1.2.0](https://pytorch.org/get-started/locally/) (may work on other versions but has not been tested)
3. other modules, run `pip install -r requirement.txt`

# Prerequisites
- C3D feature. Download C3D feature files (`sub_activitynet_v1-3.c3d.hdf5`) from [here](http://activity-net.org/challenges/2016/download.html#c3d). Convert the h5 file into npy files and place them into `./data/c3d`.

- Download annotation files and pre-generated proposals files (top100 proposals generated by [DBG](https://arxiv.org/pdf/1911.04127.pdf)) from [Google Drive](https://drive.google.com/drive/folders/1NSL7v7ax-9veJOcLxJpMzFyl5MTCUIUO?usp=sharing), and place them into `./data`. 

# Usage

- Training 
```
cfg_path=cfgs/esgn.yml
python train_RL.py --path_opt $cfg_path
```
the checkpoint files are saved in this folder `./save`.

- Validation
```
python eval.py --eval_folder esgn_c3d_run0 
```

- Validation with re-ranking
```
python eval.py --eval_folder esgn_c3d_run0 --eval_esgn_rerank
```

# Performance
| Model | proposal model | Avg proposal number |Avg Precision | Avg Recall | F1| download |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Original ESGN | SST            | 2.85 | 55.58 | 57.57 | 56.66 | |
| My reimpl. |  SST              | 2.79 | 53.80 | 61.37 | 57.34 | |
| My reimpl. |  DBG              | 2.73 | 52.67 | 58.90 | 55.62 | [url](https://drive.google.com/drive/folders/10E0U2Mun0ymYXwDDMIstETu4SVmWdtmL?usp=sharing) |
|My reimpl. with reranking | DBG | 1.66 | 37.66 | 67.47 | 48.33 | |

# Pretrained model
Download the pre-trained model and put it into `./save/esgn_c3d_run0`, then run `python eval.py --eval_folder esgn_c3d_run0`.

# References
- Awesome [ImageCaptioning.pytorch](https://github.com/ruotianluo/ImageCaptioning.pytorch) project.
- [Official implementation](https://github.com/XgDuan/WSDEC) of "Weakly Supervised Dense Event Captioning in Videos".
