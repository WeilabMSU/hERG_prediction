# Virtual screening of DrugBank database for hERG blockers using topological Laplacian-assisted AI models

---
This script is for the paper "Virtual screening of DrugBank database for hERG blockers using topological Laplacian-assisted AI models". With the script, machine-learning classification model based on natural language processing (NPL) method can be used to predict molecular compound's liability on the hERG potassium channel. 

## Requirements

OS Requirements
- CentOS Linux 7 (Core)

Python Dependencies
- setuptools (>=18.0)
- python (>=3.7)
- pytorch (>=1.2)
- rdkit (2020.03)
- biopandas (0.2.7)
- numpy (1.17.4)
- scikit-learn (0.23.2)
- scipy (1.5.2)
- pandas (0.25.3)
- cython (0.29.17)


## Download the repository
Download the repository from Github
```shell
# download repository by git
git clone https://github.com/WeilabMSU/hERG_prediction.git
```
## Install the pretrained model for feature generation

The feature generation follows the work "Extracting Predictive Representations from Hundreds of Millions of Molecules" by Dong Chen, Jiaxin Zheng, Guo-Wei Wei+ and Feng Pan." The pretrained model in their work was built based on transformer NPL techniques and is utilized to generate molecular features here.

Download and install the pretrained model under the downloaded hERG_prediction folder.

```shell
cd hERG_prediction
bash install-transformer.sh
```

## Download the trained classification model

Download the trained classification model for predicting hERG blockers/non-blockers. The trained model was obtained by integrating gradient boosting decision tree (GBDT) algorithm with molecular features, which were generated by the pretrained model. The training of model was based on hERG blocker/non-blocker dataset from reference "Support vector machine model for
herg inhibitory activities based on the integrated herg database using descriptor selection by nsga-ii" by Keiji Ogura, Tomohiro Sato, Hitomi Yuki, and Teruki Honma. 

```shell
cd hERG_prediction
wget https://weilab.math.msu.edu/Downloads/hERG_Models.zip
unzip hERG_Models.zip
```

## Generate features and carry out predictions
The input for our feature generation model is *.smi file, which stores molecules of SMILES format. The command below can be used to generate molecular features and carry out the predictions to discriminate hERG blockers/non-blockers.

```python
cd hERG_prediction
python generation-prediction.py --path-to-smi example.smi
```
The generated featurs are saved in the folder "features", and the prediction results are saved in the folder "results". The prediction file contains two columns including "block type" and "blocker probability". The column "block type" has two labels, i.e. 0 (non-blocker) and 1 (blocker). The column "blocker probability" indicates the probability to be blockers according to our predictions.


## Reference

1. Dong Chen, Jiaxin Zheng, Guo-Wei Wei, and Feng Pan. Extracting predictive representations from
hundreds of millions of molecules. The Journal of Physical Chemistry Letters, 12(44):10793–10801, 2021.

2. Keiji Ogura, Tomohiro Sato, Hitomi Yuki, and Teruki Honma. Support vector machine model for
herg inhibitory activities based on the integrated herg database using descriptor selection by nsga-ii.
Scientific reports, 9(1):1–12, 2019.

## License
All codes released in this study is under the MIT License.
