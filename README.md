# DDAffinity-network
<img src="./assets/cover.png" alt="cover" style="width:50%;" />

DDAffinity: Predicting the changes in binding affinity of multiple point mutations using protein three-dimensional structure

[[Github]](https://www.biorxiv.org/content/10.1101/2023.02.28.530137)

## Install

### Environment

```bash
conda env create -f env.yml -n DDAffinity
conda activate DDAffinity
```

The default PyTorch version is 1.12.1 and cudatoolkit version is 11.3. They can be changed in [`env.yml`](./env.yml).

## Preparation of processed dataset

We generated all protein mutant complex data from wild-type complex data  in  [SKEMPI v2 Database](https://opig.stats.ox.ac.uk/webapps/oas/oas) using rde/datasets/Foldx.py and [SKEMPI2.csv](https://drive.google.com/file/d/19QTWf7Wg2Gci1sy4e5aWHbY_8HCWcRBP/view?usp=drive_link).  Then we use rde/datasets/skempi2_parallel.py to transform the PDB files of wild-type and mutant complexes  into processed dataset [SKEMPI2_cache](https://drive.google.com/file/d/1VgvcWT9gCBsBQ2f65Eix_vNNXqxWHIK1/view?usp=drive_link).

### Datasets

| Dataset   | Download Script                                    | Processed Dataset                                                                                     |
| --------- | -------------------------------------------------- |-------------------------------------------------------------------------------------------------------|
| [SKEMPI v2](https://life.bsc.es/pid/skempi2) | [`data/get_skempi_v2.sh`](./data/get_skempi_v2.sh) | [`data/SKEMPI2/SKEMPI2_cache`](https://drive.google.com/file/d/1VgvcWT9gCBsBQ2f65Eix_vNNXqxWHIK1/view?usp=sharing) |

### Trained Weights

https://drive.google.com/file/d/1JLdHrKkwWLTsiNBaH8-x9qnEpfp9q-73/view?usp=drive_link

## Usage

### Evaluate DDAffinity

```bash
python test_DDAffinity.py ./configs/train/mpnn_ddg.yml --device cuda:1
```

### Case Study 1: Predict Mutation Effects for SARS-CoV-2 RBD

```bash
python case_study.py ./configs/inference/case_study_1.yml --device cuda:1
```

### Case Study 2: Human Antibody Optimization

```bash
python case_study.py ./configs/inference/case_study_2.yml --device cuda:1
```

### Predict Mutational Effects for a SARS-CoV-2 Human Antibody and Other Protein Complexes

```bash
python pointmut_analysis.py ./configs/inference/case_study.yml
```

💡 The script can also predict mutational effects for other protein complexes. Please refer to the example configuration file  [`7FAE_RBD_Fv_mutation.yml`](./configs/inference/7FAE_RBD_Fv_mutation.yml) to create your own mutation instruction.

### Train DDAffinity

```bash
python train_DDAffinity.py ./configs/train/mpnn_ddg.yml --num_cvfolds 10 --device cuda:1
```


```bibtex
@inproceedings{luo2023rotamer,
  title={Rotamer Density Estimator is an Unsupervised Learner of the Effect of Mutations on Protein-Protein Interaction},
  author={Shitong Luo and Yufeng Su and Zuofan Wu and Chenpeng Su and Jian Peng and Jianzhu Ma},
  booktitle={The Eleventh International Conference on Learning Representations },
  year={2023},
  url={https://openreview.net/forum?id=_X9Yl1K2mD}
}
```
