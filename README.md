# Code for "Rare Event Detection in Imbalanced Multi-Class Datasets Using an Optimal MIP-Based Ensemble Weighting Approach"
This repository contains the code and instructions to reproduce the experiments presented in our paper "Rare Event Detection in Imbalanced Multi-Class Datasets Using an Optimal MIP-Based Ensemble Weighting Approach" by Georgios Tertytchny, Georgios L. Stavrinides, and Maria K. Michael.

# Abstract
To address the challenges of imbalanced multi-class datasets typically used for rare event detection in critical cyber-physical systems, we propose an optimal, efficient, and adaptable mixed integer programming (MIP) ensemble weighting scheme. Our approach leverages the diverse capabilities of the classifier ensemble on a granular per class basis, while optimizing the weights of classifier-class pairs using elastic net regularization for improved robustness and generalization. Additionally, it seamlessly and optimally selects a predefined number of classifiers from a given set. We evaluate and compare our MIP-based method against six well-established weighting schemes, using representative datasets and suitable metrics, under various ensemble sizes. The experimental results reveal that MIP outperforms all existing approaches, achieving an improvement in balanced accuracy ranging from 0.99% to 7.31%, with an overall average of 4.53% across all datasets and ensemble sizes. Furthermore, it attains an overall average increase of 4.63%, 4.60%, and 4.61% in macro-averaged precision, recall, and F1-score, respectively, while maintaining computational efficiency.

# Source Code Availability
The complete source code used in this research, including scripts for training, weight computation, and inference, is available in this repository to ensure the reproducibility of our results and provide a practical foundation for further research and development based on our work.

# Prerequisites
1. **Bash** **Shell**: Ensure you have a Bash-compatible shell to execute the script.
2. **Python 3.x:** The shell script calls several Python scripts. Ensure Python 3 is installed and accessible via python3.
3. **Python Dependencies:** Install any required libraries for the Python scripts. Common dependencies include:
   - numpy (https://numpy.org/)
   - pandas (https://pandas.pydata.org/)
   - scikit-learn (https://scikit-learn.org/stable/)
   - gurobipy (https://pypi.org/project/gurobipy/) 
   
# Datasets
1. **LeakDB**: https://zenodo.org/records/13985057 (Check also **DATASETS** folder for the .csv we used)
2. **NSL-KDD**: https://raw.githubusercontent.com/HoaNP/NSL-KDD-DataSet/refs/heads/master/KDDTrain%2B_20Percent.txt
3. **SG-MITM**: https://zenodo.org/records/8375657 (Check also **DATASETS** folder for the .csv we used)
4. **CIC-IDS2017**: https://www.unb.ca/cic/datasets/ids-2017.html

# Execution
To execute the code, run the RUN.sh script. If you need to change permissions for execution, use the following command:

```bash
chmod +x RUN.sh
```

# Workflow of RUN.sh
**Step 1:** Training & Accuracy Matrix Computation
1. Input dataset (e.g., D1_LEAKDB.csv) is trained for a set of classifiers using stratified k-folds (in our case **k=5**)
2. Unnecessary lines are removed to produce the accuracy matrix for the classifiers

**Step 2:** Weight Computation
Weighting schemes introduced in our paper are applied:
1.   Uniform Weighting Per Classifier (UW)
2.   Uniform Weighting Per Classifier Class (UW_PCA)
3.   Accuracy-based Weighting Per Classifier (WA)
4.   Accuracy-based Weighting Per Classifier Class (WA_PCA)
5.   Differential Evaluation Weighting (DE)
6.   Bayesian Model Averaging (BMA)
7.   **MIP & Elastic Net Weighting (MIPEN)**

**Step 3:** Inference
**Uncomment and customize the inference lines to use generated weights for evaluation:**
python3 "$inference_scripts_folder/2_INFERENCE_ALGORITHM.py" --dataset $input_file --weights 0.12,0.12,... --output "$results_folder/1_NSL_UW.csv"

**RESULTS**
All generated weights and inference results are saved in respective folders.

**WEIGHTS**: Contains weight files like UW_D1_LEAKDB.txt.

**RESULTS**: Contains inference outputs like 1_NSL_UW.csv.

**Running Example**
By setting in RUN.sh the **dataset_code_number="D2_NSL_KDD"**
**The script will:**
1. Process **D2_NSL_KDD.csv**
2. Generate intermediate files: **D2_NSL_KDD_ACC.csv** and **D2_NSL_KDD_ACCURACIES.csv**
3. Compute weights and save them in the **WEIGHTS** folder
4. Run inference and compute results saved in **RESULTS** folder

At the end of the script, you will see:

**Script execution completed.**

# Contact
For any queries, feel free to raise an issue in this GitHub repository or contact the maintainers directly.
