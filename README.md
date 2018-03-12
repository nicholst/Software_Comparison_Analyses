# Exploring the Impact of Analysis Software on fMRI Results

Supporting code to perform the analyses and create the figures of the manuscript with the same title available at <ADD_BIORXIV_DOI_WITH_LINK>.

## Table of contents
   * [How to cite?](#how-to-cite)
   * [How to reproduce the figures?](#how-to-reproduce-the-figures)
      * [Fig. 1a](#fig-1a)
      * [Fig. 1b](#fig-1b)
      * [Fig. 2](#fig-2)
      * [Fig. 3](#fig-3)
      * [Fig. 4](#fig-4)
      * [Fig. 5](#fig-5)
      * [Fig. 6](#fig-6)
   * [How to rerun the full analysis?](#how-to-rerun-the-full-analysis)
   * [Contents overview](#contents-overview)

## How to cite

To cite this repository, please cite the corresponding manuscript: 

"Exploring the Impact of Analysis Software on fMRI Results" Alexander Bowring, Thomas E. Nichols, Camille MaumetTechnical Report bioRxiv: 1-<ADD_NUM_OF_PAGES>. doi: <ADD_DOI_WITH_LINK>. 

## How to reproduce the figures

### Dependencies
To reproduce the figures, you will need to install the dependencies listed in `requirements.txt`, this can be done using pip with:
```
pip install -r requirements.txt
```

You will also need to have Jupyter notebook installed, we recommend using [Anaconda](https://conda.io/docs/user-guide/install/index.html) to perform the install.

### Fig. 1a

#### Left column

1. From a Terminal, run:

    ```
    jupyter notebook ./figures/ds001_notebook.ipynb
    ```

3. In the notebook, run all the cells up to the cell starting with `from lib import bland_altman` which will reproduce the first column of figure 1a.


#### Right column
Same as Fig. 1 left but using `./figures/ds109_notebook.ipynb`.

### Fig. 1b
Same as 1a but using `./figures/ds120_notebook.ipynb`.

### Fig. 2
#### Left sub-plot
1. From a Terminal, run:

    ```
    jupyter notebook ./figures/ds001_notebook.ipynb
    ```

3. In the notebook, run all the cells up to the cell starting with `from lib import dice`.

#### Middle sub-plot
Same as Fig. 2 left but using `./figures/ds109_notebook.ipynb`.

#### Right sub-plot
Same as Fig. 2 left but using `./figures/ds120_notebook.ipynb`.

### Fig. 3

#### Left column
1. From a Terminal, run:

    ```
    jupyter notebook ./figures/ds001_notebook.ipynb
    ```

3. In the notebook, run all the cells up to the cell starting with `from lib import euler_characteristics`.

#### Right column
Same as Fig. 3 left but using `./figures/ds109_notebook.ipynb`.

### Fig. 4
1. From a Terminal, run:

    ```
    jupyter notebook ./figures/ds001_notebook.ipynb
    ```

3. In the notebook, run all the cells up to the cell starting with `from lib import plot_excursion_sets`.

### Fig. 5
#### Left column
1. From a Terminal, run:

    ```
    jupyter notebook ./figures/ds001_notebook.ipynb
    ```

3. In the notebook, run all the cells up to the cell starting with `bland_altman.bland_altman('Bland-Altman Plots: Permutation Tests'`.

#### Right column
Same as Fig. 5 left but using `./figures/ds109_notebook.ipynb`.

### Fig. 6
#### Left column
1. From a Terminal, run:

    ```
    jupyter notebook ./figures/ds001_notebook.ipynb
    ```

3. In the notebook, run all the cells up to the cell starting with `reload(bland_altman) bland_altman.bland_altman_intra('Bland-Altman Plots: Parametric vs Permutation'`.

#### Right column
Same as Fig. 6 left but using `./figures/ds109_notebook.ipynb`.

## How to rerun the full analysis

### Raw data
To run the experiments included in the manuscript, raw data must be downloaded from [OpenfMRI.org](https://openfmri.org) and copied on your local computer:
 - ds000001 revision 2.0.4: https://openfmri.org/dataset/ds000001/
 - ds000109 revision 2.0.2: https://openfmri.org/dataset/ds000109/
 - ds000120 revision 1.0.0: https://openfmri.org/dataset/ds000120/

### Analysis of ds000001

#### Data processing using SPM, FSL and AFNI
Given:
 - `<PATH_TO_RAW_DATA>`: the path to the raw data for `ds000001` and
 - `<PATH_TO_OUTPUT>`: the path to the output folder where the results should be stored (must end with a `ds001` sub-folder).

1. In `scripts/process_ds001_SPM.m` replace the values of `study_dir` and `results_dir` by `<PATH_TO_RAW_DATA>` and `<PATH_TO_OUTPUT>` respectively.

2. In `scripts/process_ds001_FSL.py` and `scripts/process_ds001_AFNI.py` replace the values of `raw_dir` and `results_dir` by `<PATH_TO_RAW_DATA>` and `<PATH_TO_OUTPUT>` respectively.

1. For the SPM analysis, inside Matlab run:

    ```
    addpath('scripts')
    addpath(fullfile('scripts', 'lib'))
    process_ds001_SPM
    ```
    
    This will create onsets, preprocess the data, and run first and group level analyses. 
    
2. For the FSL analysis, from a terminal run:

    ```
    python scripts/process_ds001_FSL.py
    ```

3. For the AFNI analysis, from a terminal run:

    ```
    python scripts/process_ds001_AFNI.py
    ```
    
#### Derived data

##### Derived images
The derived data available on NeuroVault at https://neurovault.org/collections/2209/ can be reproduced as follows:

1. NIDM-Results packs for SPM and FSL are available in `<PATH_TO_OUTPUT>/SPM/LEVEL2` and `<PATH_TO_OUTPUT>/FSL/LEVEL2` respectively.

2. For the resliced images, inside Matlab run

    ```
    addpath('scripts')
    addpath(fullfile('scripts', 'lib'))
   	ds001_reslice_images
    ```

##### Other derived data
The csv files containing the Euler characteristics can be recomputed in Matlab, using:
    ```
    addpath('scripts')
    addpath(fullfile('scripts', 'lib'))
   	ds001_euler_chars
    ```
    
### Analysis of ds000109
Same as for ds000001, replacing all occurences of `001` by `109` and https://neurovault.org/collections/2209/ by https://neurovault.org/collections/2238/.


### Analysis of ds000120
Same as for ds000001, replacing all occurences of `001` by `120` and https://neurovault.org/collections/2209/ by https://neurovault.org/collections/2488/.

## Contents overview
```
 	ds001: Part of ds001 output data (excluding images)
	ds109: Part of ds109 output data (excluding images)
	ds120: Part of ds109 output data (excluding images)
	figures: Scripts and notebooks to reproduce the figures
	scripts: Scripts to rerun the analysis 
	.gitignore: git configuration file
	README.md: current file
```
