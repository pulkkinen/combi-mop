# combimop
# Multiobjective optimization identifies cancer-selective combination therapies
Otto I. Pulkkinen, Prson Gautam, Ville Mustonen, and Tero Aittokallio

# The repopsitory contains 
## 1. In-house data (FIMM_combinationData_PrsonGautam-20201004T071304Z-001.zip)

## 2. Supplementary notebook
### Multiobjective optimization for cell line MALME-3M using the NCI ALMANAC


This Jupyter notebook performs biobjective optimization of therapeutic and nonselective effects of drug  combinations based on the NCI ALMANAC data.

Of the original NCI ALMANAC data, a table with each row containing growth inhibition data for a two-drug combination was collected. The first column of the table contained a combination index (running from 0 to 82409), the second and the third column showed the names of the drugs in a two-drug combination, and the fourth and fifth columns were their respective concentrations. The remaining 60 columns were the growth fractions (growth inhibition values between -100 (full inhibition) and 100 (no effect) reported in the NCI ALMANAC) for the NCI-60 cell lines. The names of the cell lines were listed in the first row of the table.

The script first transforms the data into a tensor of type (60, 104, 104, 5, 5) as input Q, where 60 is the number of cell lines in the NCI-60, 104 is the total number of drug compounds. For each pair of drugs (the tensor is symmetric with respect to interchange of second and third indices) on each of the 60 cell lines, there is a 5x5 matrix which have the drug concentrations as the first column and the first row, and the growth inhibition values normalized to [0,1] as a 4x4 submatrix. The value 0 indicates complete inhibition, and the value 1 means that the combination had no effect on the growth rate at that pair of concentrations.

In order to apply this notebook to a different dataset, the parameters for numbers of cell lines (nCellLines), number of drugs (nDrugs), and number of concentrations (nConcentrations) for each drug in the combination matrices need to be re-defined below. The data can be imported as a table (described below) or directly as a tensor of type (nCellLines, nDrugs, nDrugs, nConcentrations, nConcentrations). The construction of this tensor, called Q here, is shown below.

Although the biobjective optimization, that is, finding Pareto optimal combinations by using the epsilon-constraint method is quite general, and can be done just by running the code with the re-defined parameters and an associated input tensor, the full list of features, such as highlighting special combinations with specific colors, can be only achieved by going through the code line-by-line. Also, naming the drugs and cell lines helps in performing searches and in the analysis of results.

NCI ALMANAC growth inhibition data is available for download at 
https://wiki.nci.nih.gov/display/NCIDTPdata/NCI-ALMANAC .

NCI ALMANAC: [Holbeck SL, et al. (2017) The National Cancer Institute ALMANAC: A Comprehensive Screening Resource for the Detection of Anticancer Drug Pairs with Enhanced Therapeutic Activity. Cancer Res. 77(13):3564–3576.]
