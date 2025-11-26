# Process Mining Analysis of Brazilian Emergency Room Healthcare Data

A comprehensive process mining analysis of patient flow in a Brazilian Emergency Room, developed as the final exam project for the Business Information Systems course at the University of Milano.

## Project Overview

This project applies process mining techniques to analyze and optimize emergency room patient pathways using real healthcare event log data. The analysis covers the complete patient journey from admission ("Atendimento") to discharge ("Alta"), identifying bottlenecks, process variants, and opportunities for operational improvement.

## Dataset

- **Source**: UpFLux Healthcare Database (Brazilian Emergency Room)
- **Time Period**: July-August 2020
- **Total Events**: ~3,000 events
- **Patient Cases**: 443 unique patients
- **Activities**: 9 distinct activities including Atendimento (Admission), Triagem (Triage), Consulta (Consultation), Exames (Examinations), and Alta (Discharge)

### Key Attributes

| Attribute | Description |
|-----------|-------------|
| `case:concept:name` | Unique patient identifier |
| `concept:name` | Activity type |
| `time:timestamp` | Event timestamp |
| `Nível de Urgência` | Urgency level (Baixo, Média, Idoso, etc.) |
| `CID` | ICD diagnostic code |
| `Doença` | Disease description |
| `outlier_label` | Pre-labeled outlier classification |

## Analysis Components

### 1. Data Quality Assessment & Preprocessing
- Timestamp validation and null handling
- Duplicate detection and removal
- Case completeness filtering (cases ending with "Alta")
- Critical attribute validation

### 2. Activity Frequency Analysis
- Distribution analysis of 9 unique activities
- Pareto analysis of activity occurrences
- Resource workload assessment

### 3. Variant Analysis
- Identification of 111 unique process variants
- Power-law distribution analysis
- Variant frequency and performance correlation

### 4. Performance-Oriented Analysis
- Processing time calculation per activity
- Lead time computation (total case duration)
- Waiting time analysis between activities
- Bottleneck identification

### 5. Clinical Segmentation Analysis
- Segmentation by urgency level (Nível de Urgência)
- Comparative analysis across patient groups
- Statistical testing (Kruskal-Wallis, Chi-Square)
- Rework pattern detection by segment

### 6. Process Discovery
- **Directly-Follows Graph (DFG)**: Visual process flow representation
- **Inductive Miner**: Petri Net and Process Tree generation
- **Alpha Miner**: Comparative model discovery

### 7. Quality Metrics Evaluation
- **Fitness**: Trace replay conformance (Token-Based Replay)
- **Precision**: Behavioral appropriateness (ETC Conformance)
- **Simplicity**: Model complexity assessment
- **F1 Score**: Harmonic mean of fitness and precision

### 8. Variant-Filtered Model Discovery
- Top-k variant filtering for improved precision
- Coverage vs. precision trade-off analysis
- Optimized model generation

### 9. Predictive Analytics (Machine Learning)
- Feature engineering from process data
- Classification models for outcome prediction
- Regression models for lead time prediction
- SHAP analysis for feature importance interpretation

## Key Findings

- **Dominant Disease**: Influenza (J11.1) accounts for ~79% of cases (COVID-19 period)
- **Mean Case Duration**: ~2.2 hours with high variance
- **Process Complexity**: 111 variants indicate significant process variability
- **Urgency Impact**: Significant statistical difference in lead times across urgency levels
- **Rework Patterns**: Higher urgency cases show increased activity repetition

## Technologies & Libraries

```
pandas>=1.3.0
pm4py>=2.7.0
matplotlib>=3.5.0
seaborn>=0.11.0
numpy>=1.21.0
scipy>=1.7.0
scikit-learn>=1.0.0
shap>=0.41.0
powerlaw>=1.5
```

## Installation

1. Create and activate a virtual environment:
```bash
python -m venv bimexam-venv
source bimexam-venv/bin/activate  # Linux/Mac
# or
bimexam-venv\Scripts\activate  # Windows
```

2. Install required packages:
```bash
pip install pandas pm4py matplotlib seaborn numpy scipy scikit-learn shap powerlaw
```

3. For Jupyter notebook support:
```bash
pip install jupyter ipykernel
python -m ipykernel install --user --name=bimexam-venv --display-name "Python BIMExam"
```

## Usage

1. Place the dataset file (`UpFLux_Healthcare_Database_labeled.csv`) in your project directory
2. Update the `filepath` variable in the notebook to match your data location
3. Run the Jupyter notebook cells sequentially:
```bash
jupyter notebook Exam.ipynb
```

## Project Structure

```
├── Exam.ipynb                          # Main analysis notebook
├── README.md                           # This file
├── UpFLux_Healthcare_Database_labeled.csv  # Dataset (not included)
├── petri_net_inductive_miner.png       # Generated Petri Net visualization
├── process_tree_inductive_miner.png    # Generated Process Tree
├── petri_net_model.pnml                # Exported Petri Net model
└── petri_net_alpha_miner.png           # Alpha Miner comparison model
```

## Methodology

The analysis follows the standard Process Mining methodology:

1. **Data Extraction** → Load and validate event log
2. **Data Preprocessing** → Clean, filter, and prepare data
3. **Process Discovery** → Generate process models
4. **Conformance Checking** → Evaluate model quality
5. **Process Enhancement** → Performance and variant analysis
6. **Predictive Analytics** → Machine learning for outcome prediction

## Statistical Tests Applied

| Test | Purpose | Result |
|------|---------|--------|
| Kruskal-Wallis | Lead time differences across urgency levels | Significant (p < 0.05) |
| Chi-Square | Rework independence from urgency level | Significant (p < 0.05) |
| Wasserstein Distance | Activity distribution comparison | Varies by segment |

## Output Artifacts

- Process models (Petri Net, Process Tree, DFG)
- Quality metrics reports
- Statistical test results
- Visualization exports (PNG)
- SHAP feature importance plots

## Author

**Angela**  
Business Information Systems  
University of Milano  
Academic Year 2024-2025

## License

This project is submitted as academic coursework. Dataset usage is subject to original data provider terms.

## Acknowledgments

- Course: Business Information Systems
- Dataset: UpFLux Healthcare Database
- Process Mining Library: pm4py
