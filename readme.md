# KIKT:Weakly Supervised Dynamic Scene Graph Generation with Temporal-enhanced In-domain Knowledge Transferring

## Installation
Following PLA/environment.yaml to construct the virtual environment.

## Dataset
### Data preperation
1. For object detection results, we use pre-trained object detector [VinVL](https://github.com/pzzhang/VinVL) to generate detection results, you can follow our baseline [PLA](https://github.com/zjucsq/PLA/tree/master) to generate them on your own.

2. For dataset, download from [Action Genome](https://github.com/JingweiJ/ActionGenome).

3. Download necessary weakly-supervised annotation files and pre-trained weight are stored in [](), the final data structure should be like

```
| -- data
     | -- action-genome
           | -- frames     ## sample frames
           | -- videos     ## original videos
           | -- AG_detection_results   ## pre-trained object detector results
           | -- annotations ## weakly supervised scene graph generation annotations
           | -- AG_detection_results_refine ## refined object detector results(optional)
| -- refine
      | -- output # pre-trained relation aware transformer weight
| -- PLA
      | -- model # pre-trained scene graphe generation weight
```

## Evaluation

### Relation-Aware Transformer Model
```
cd ~/refine
python scripts/evaluate.py # evaluate the performance of object detection
```
| Model  | AP@1 |AP@10|AR@1 | AR@10|Weight|
| --- | ----------- |----- |----- |----- |----- |
|PLA(baseline)    | 11.4 |11.6 |33.3 |37.6| -|
| Ours  | 24.3|26.6|30.2|45.1|[weight]()|

### Scene Graph Generation Model
```
cd ~/PLA
python test.py --cfg configs/final.yml # for final scene graph generation performance evaluation
```
| Model  | W/R@10|W/R@20|W/R@50|N/R@10|N/R@20|N/R@50|weight|
| --- | ----------- |----- |----- |----- |----- |----- |----- |
|PLA(baseline)    | 14.32|20.42|25.43|14.78|21.72|30.87|-|
| Ours  | 17.50 |22.46| 27.73| 18.67| 24.52| 33.65|[weight]()|
## Training

### Step1. Optical Flow Extraction
We use [RAFT](https://github.com/princeton-vl/RAFT) to generate the optical flow in our data, you can either use our pre-processed optical flow (stored in []()) or generate them on you own by following steps:

```
cd ~/RAFT   ## download the RAFT ckpt accordingly
python gen_test.py
python gen_train.py
```
Then place the generated optical flow file within folder ~/data/action-genome/.
### Step2. Relation-aware Refine Training
```
cd ~/refine
python scripts/train.py 
```
### Step3. PLA Training
```
cd ~/PLA
python train.py --cfg configs/oneframe.yml # for image SGG model
python train.py --cfg configs/final.yml # for video SGG model
```
## Acknowledgement
We build our project upon [PLA](https://github.com/zjucsq/PLA/tree/master), [RAFT](https://github.com/princeton-vl/RAFT), thanks for their works.
## Citation
```
```


