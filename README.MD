
# Install

To install the required packages, `cd` to this directory and run the following.
```
sudo apt update
sudo apt install python3-dev python3-pip
sudo apt-get install python-setuptools
sudo easy_install pip
```

Create an environment `sign4bb-venv` 
```
sudo pip3 install -U virtualenv  # system-wide install
virtualenv -p python3 ./sign4bb-venv
source ./sign4bb-venv/bin/activate
```
The above assumes using Python 3.6, if you're using Conda with Python 3.7, you can create the environment this way
```
conda create -n sign4bb-venv python=3.6
source activate sign4bb-venv
```
Then install the requirements,
```
pip install -r ./requirements/(tf_gpu_linux|linux|osx)_requirements.txt
python -m ipykernel install --user --name sign4bb-venv --display-name "Python (sign4bb-venv)"
```

#### TL;DR (recommended)
```
mkdir ../sign4bb-venv
conda env create -p ../sign4bb-venv -f ./requirements/conda_env.yaml
conda activate ../sign4bb-venv/
```

# Running code

Whenever you'd like to run any of the scripts. Make sure the environment is activated.
```
source ./sign4bb-venv/bin/activate
```

To deactivate:
```
deactivate
```

If you installed it with conda, you can run `conda`'s corresponding commands


# Downloading pre-trained models & Datasets

```
export PYTHONPATH=`pwd`
python utils/download_models.py # downloads mnist and cifar10 models
python utils/download_cifar10.py # download cifar10 dataset
```
MNIST will be downloaded upon first run of the code. 
For IMAGENET, please download the imagenet validation set and make sure the foloder is structured in the following:

# To run Keep K experiment

```
python ./experiments/keep_k_sign_exp.py
```

# To view experiments based on Tensorboard:
Currently, `hamming_dist_exp`, `partial_derivatives_exp` export their results to Tensoboard

```
tensorboard --logdir=../data/hamming_dist_exp/
```

# To generate algorithms' hyperparameter tables:

```
# to export parameter table of algorithms
json_files = get_jsonfiles('*bandit*')
utils.latex_fcts.config_json_2_tbl_latex(json_files)
```

TeX files will be generated in `data/tex_tbls`

# To generate plots/tables from `attacks/blackbox/run_attack.py`

`run_attack.py` will store results into both `h5` file (logging progress of the algorithms) as well as a json (logging the final status of the algorithms)

To generate plots from data stored in the resulting `h5` file

```
utils.plt_fcts.plt_from_h5tbl(['../../data/blackbox_attack_exp/{H5_FILE_NAME}.h5'])
```

Plots will be generated in `data/blackbox_attack_exp/{H5_FILE_NAME}_plots`

To generate latex tables from the resulting `json` file
```
utils.latex_fcts.res_json_2_tbl_latex('../../data/blackbox_attack_exp/{JSON_FILE_NAME}.json')
```

Tex files will be generated in `data/blacbox_attack_exp`
