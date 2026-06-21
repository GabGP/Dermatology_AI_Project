# Machine Learning: Differential Diagnosis of Erythemato-Squamous Diseases

**Professional Seminar 1: Artificial Intelligence - AN - 2026**

**Group No. 3:** Carlos Alvarez (23004004), Gabriel Garcia (17001171), Elvis Suc (17006296)


---

## Introduction
Erythemato-squamous diseases represent a significant diagnostic challenge, as they share visually similar lesions, both clinically and histologically, and can evolve into one another in early stages. 

This project applies multiclass classification techniques using machine learning algorithms to analyze clinical data and accurately differentiate 6 categories of the disease, achieving faster diagnoses.

---

## Dataset Description
The dataset comes from the UCI Machine Learning Repository and contains clinical and histological information of patients with erythemato-squamous diseases.

**Independent Variables (Features):**
'erythema', 'scaling', 'definite-borders', 'itching', 'koebner phenomenon', 'follicular papules', 'family history', 'pnl infiltrate', 'exocytosis', 'hyperkeratosis', 'parakeratosis', 'clubbing of the rete ridges', 'spongiform pustule', 'munro microabcess', 'disappearance of the granular layer', 'inflammatory mononuclear infiltrate', 'age'

**Dependent Variables (Target):**
'class'

**Data Types:**
Numeric `Int64` type, except age with `Float64` type.

**Classes and Samples:**
| No. | Class | Samples |
| :--- | :--- | :--- |
| 1. | Psoriasis | 112 |
| 2. | Seborrheic Dermatitis | 61 |
| 3. | Lichen Planus | 72 |
| 4. | Pityriasis Rosea | 49 |
| 5. | Chronic Dermatitis | 52 |
| 6. | Pityriasis Rubra Pilaris | 20 |

**Total Samples:** 366

---

## Methodology

### 1. Data Validation
The 'dermatology.data' dataset is downloaded and processed as a CSV with missing values represented as "?". In addition, the obtained data types are checked and their information is observed, such as ranges and quantity.

### 2. Data Pre-Processing
* **Missing Values:** 8 rows with missing data were found and removed, as they did not represent a considerable amount compared to the rest of the data.
* **Encoding:** All data was already encoded; it was only necessary to apply label encoding to the target.
* **Separating Variables:** Using a correlation matrix, the dependent and independent variables were selected based on their relationship with the target, dependency transitivity, and strong relationship between features. Thus, out of 34 features, only 17 remained.
* **Normalization:** Due to the scale between features, it was required to normalize all data to ranges between 0 and 1.
* **Class Balancing:** It was required to balance the classes due to the high imbalance between them. Therefore, the SMOTE-Tomek method was applied, which combines oversampling with synthetic data for minority classes and then performs undersampling to remove any remaining noise.

### 3. Model Training
After configuring each model, the models were trained with 80% of the dataset and base training was performed except for the neural network, where callbacks such as EarlyStopping, ModelCheckpoint, and Tensorboard were used.

### 4. Model Validation
Each model was evaluated with 20% of the dataset, in addition to making predictions to obtain the Accuracy, Recall, Precision, and F1 Score metrics. Finally, the best model was determined by comparing the models using the averaged metrics of 10 trainings with `random_state` 2026 on the dataset.

---

## Results
Four multiclass classification models were trained and evaluated on the dermatology dataset. The performance of each model is summarized in the following table:

| Metric | Neural Network | Neural Network V2 | Support Vector Machine | Random Forest |
| :--- | :--- | :--- | :--- | :--- |
| **Accuracy** | 91.79% | 89.55% | 95.52% | 96.27% |
| **Recall** | 91.97% | 89.99% | 96.10% | 96.77% |
| **Precision** | 92.01% | 89.82% | 96.01% | 96.43% |
| **F1-Score** | 91.94% | 89.89% | 95.91% | 96.43% |

* The model with the best performance across all metrics was Random Forest. 
* It is worth mentioning that SVM has greater consistency between trainings due to its deterministic nature.

---

## Conclusions
* The three evaluated machine learning models proved to be effective for classification.
* Class balancing with SMOTE-Tomek was decisive, given the imbalance of 112 vs 20 samples between classes.
* Reducing from 34 to 17 features through correlation eliminated noise without sacrificing performance.
* On small and structured datasets, classical models outperformed the neural network.
* Random Forest was the winning model with a Recall of 96.77%, a critical metric in medical contexts.

---

## Future Improvements
* Increase the dataset size by collecting more clinical samples, especially from minority classes, to improve model generalization.
* Test different configurations in the neural network, such as adding extra layers or adjusting the learning rate, since it was the model with the lowest performance.
* Integrate the model into a real clinical environment as a medical diagnosis support tool, allowing dermatologists to validate their diagnoses with a data-driven second opinion.
