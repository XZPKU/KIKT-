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

### Model Zoo

## Training

### Step1. Optical Pre-Process
We use [RAFT](https://github.com/princeton-vl/RAFT) to generate the optical flow in our data, you can either use our pre-processed optical flow (stored in []()) or generate them on you own by following steps:


Then place the generated optical flow file within .
### Step2. Relation-aware Refine Training

### Step3. PLA Training


