# Mendelian Inheritance Analysis and Trait Prediction

## Problem Statement
In genetics, verifying parentage and understanding inheritance patterns are critical for genetic counseling, research, and personalized medicine. This project aims to analyze genomic data to:
1. Confirm whether a child’s DNA is consistent with being inherited from the given parents using Mendelian inheritance rules.
2. Predict potential traits or risks based on specific SNPs (Single Nucleotide Polymorphisms) using a trait database.

---

## Aim
The aim of this project is to:
1. Verify parentage by analyzing inheritance consistency.
2. Identify homozygosity/heterozygosity patterns in the child’s genotype.
3. Predict traits or health risks based on a predefined trait database.
4. Calculate confidence that the child belongs to the given parents based on genomic data.

---

## Dataset Description
The input datasets include genomic data for three individuals: father, mother, and child. Each dataset is stored in a CSV file with the following structure:

| Column         | Description                                                                 |
|----------------|-----------------------------------------------------------------------------|
| `# rsid`       | Unique identifier for each SNP (Single Nucleotide Polymorphism).           |
| `chromosome`   | The chromosome number where the SNP is located.                            |
| `position`     | The genomic position of the SNP in base pairs.                             |
| `genotype`     | The alleles present at the SNP (e.g., `AA`, `AG`, `GG`).                   |

### Input Files
- `Father Genome.csv`: Genomic data for the father.
- `Mother Genome.csv`: Genomic data for the mother.
- `Child 1 Genome.csv`: Genomic data for the child.

### Output Files
1. **`Inheritance_Analysis.csv`**:
   - Contains inheritance consistency and homozygosity/heterozygosity analysis for each SNP.
2. **`Child_result_Trait_Predictions.csv`**:
   - Includes trait predictions based on a predefined trait database.
3. **`Child_Inheritance_Confidence_Analysis.csv`**:
   - Final summary with confidence score indicating how likely the child belongs to these parents.

---

## Procedure

### 1. Loading Data
The genomic data for the father, mother, and child are loaded from CSV files into Pandas DataFrames.

### 2. Data Merging
The datasets are merged on common columns (`# rsid`, `chromosome`, and `position`) to align SNPs across all individuals.

### 3. Inheritance Analysis
For each SNP:
- The child’s genotype is checked against Mendelian inheritance rules.
- If the child’s alleles are a valid combination of one allele from each parent, it is marked as `"Consistent"`. Otherwise, it is marked as `"Inconsistent"`.

### 4. Homozygosity/Heterozygosity Analysis
For each SNP in the child’s genotype:
- **Homozygous**: Both alleles are identical (e.g., `AA`, `GG`).
- **Heterozygous**: The alleles differ (e.g., `AG`, `AC`).

### 5. Trait Prediction
A predefined trait database maps specific SNPs to traits and their associated risk alleles:
- If the child’s genotype contains a risk allele, they are flagged as being at risk for that trait.


### 6. Confidence Calculation
Confidence in parentage is calculated as: Confidence = (Consistent SNPs / Total SNPs) * 100



---

## Results

### Example Output (Inheritance Analysis):
| # rsid       | chromosome | position | genotype_father | genotype_mother | genotype_child | inheritance | child_homozygosity |
|--------------|------------|----------|-----------------|-----------------|----------------|-------------|---------------------|
| rs12564807   | 1          | 734462   | AA              | AA              | AA             | Consistent  | Homozygous          |
| rs3131972    | 1          | 752721   | AG              | GG              | AG             | Consistent  | Heterozygous        |
| rs148828841  | 1          | 760998   | AC              | CC              | AC             | Consistent  | Heterozygous        |

### Example Output (Trait Prediction):
| # rsid       | genotype_child | trait_prediction            |
|--------------|----------------|-----------------------------|
| rs12564807   | AA             | No data                    |
| rs3131972    | AG             | No data                    |
| rs148828841  | AC             | No data                    |

### Confidence Score:
- Total SNPs Analyzed: **601,802**
- Consistent SNPs: **596,351**
- Confidence: **99.09%**

---

## Usage Instructions

### Prerequisites
- Python 3.x
- Pandas library
