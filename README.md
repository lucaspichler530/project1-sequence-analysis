# project1-sequence-analysis
A python project comparing and analysing treatment and control samples using next-generation sequencing (NGS) data to identify DNA mutations.

**Title and Purpose**

This python program analyses next-generation sequencing (NGS) data from six _Schizosaccharomyces pombe_ samples, three treatment samples (treated with a Genotoxic agent) and three untreated control samples. Using various functions, it identifies nucleotide substitutions, and investigates the differences in mutation patterns across the treatment and control groups.

**How to run the program**

Open the Jupyter notebook using Google Colab, an interactive Python environment including independent cells and a variable inspector. Run the setup cells first in order to load the appropriate reference sequence and sequencing reads. Finally, execute and produce the function definitions, test and final analysis cells in order.

**Inputs and Outputs**

The **inputs** include a 200-nucleotide reference DNA sequence and, a collection of sequencing reads containing a read ID, sample name, experimental group (treatment or control), and a DNA sequence.

The **outputs** include a validated read record for each sample, identified mutations and a summary on mutation frequencies. Furthermore, it outputs substitution types and the frequency of each mutated position. Using a Welch's t-test, it also compares the three most frequently mutated positions between the treatment and control samples.

**Code design**

Each step of the analysis is split into five stages, each containing one separate function. `validate_read()` checks and normalises input reads (correct length, case and valid characters). `find_mutations()` identifies all mutations and mutations at each position of a valid read. `analyse_reads()` combines functions 1 and 2 to analyse all DNA reads (validity and mutations). `summarise_samples()` summarises and groups the information for all samples. `compare_positions()` statistically analyses and interprets results using Welch's t-test.

Dictionaries were used to store information on reads and mutations as they facilitate the access of important values such as sample names, mutation positions and substitution types through descriptive keys. Important original input data such as invalid reads and their errors and mutations were not discarded and instead stored in new dictionaries in order to preserve data quality information. 

Dictionaries were also used to count mutations at each position for position comparisons. Samples with zero mutations were also included, ensuring that sample comparisons were not restricted to only mutated samples.

**Testing**

Artifical datasets containing valid and invalid sequences were created to test each functios (lowercases, incorrect lengths and invalid characters).  
```python
test_lowercase = validate_read("atgc", test_reference)
assert test_lowercase == {"sequence": "ATGC", "valid": True, "errors": []}
```
Empty inputs and samples with no valid reads were also tested to check whether functions could handle edge cases.  
```python
test_empty_list = analyse_reads([], test_reference)
assert test_empty_list = []
```
Artifical datasets with known mutations were also used to check that correct nucleotide positions, group means and statistical comparisons were correctly returned.  
```python
assert test_summary_results[0]["statistic"] is not None
assert test_summary_results[0]["p_value"] is not None
```
