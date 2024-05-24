# Analyze_PAM_from_BE_Result
Code for Engineering XXX XXX Nickase for Robust Base Editing with Broad Targeting Range, NCB, 2024
Analyze PAM sequence from Base Edit results.

Protospacer adjacent motif(PAM) and transposon-associated motif(TAM) are key DNA sequence for RNA-guild gene editor to bind and reconize target DNA.
The commod method to identify the PAM or TAM is using Cas protein to cut a target site with random NNNNN PAM sequence. Since there is a double strand 
break, some sequencing reads might loss or modify its original PAM or TAM infomation.

Here we proposed a new method to identify PAM or TAM using Base-edit method. This method will not generate double strand break, which will make 
the detection more accurate.

# How it work
Firstly, we utilized NGS Tools (version 1.6.3, https://github.com/Hanhui-Ma-Lab/NGS_Tools) to conduct a thorough analysis of the sequencing results, aiming to confirm the occurrence of base editing. During this process, we adhered to the phred33 standard for quality filtering of sequencing data, retaining only high-quality sequences with an overall accuracy exceeding 99% for subsequent alignment. We took the DNA location corresponding to the sgRNA as the key target and precisely aligned the sequencing results, focusing on detecting C to T base substitutions. If only C to T substitutions were detected, we categorized them as correct edits; whereas other types of substitutions, insertions, or deletions were uniformly classified as indel.

After confirming the existence of base editing and its high efficiency, we further conducted TAM analysis on the sequencing results. We extracted all existing TAM types from the NGS sequencing data and separately tallied the edited reads and unedited reads containing these TAMs. For the TAM sequences within the edited reads, we calculated the occurrence probabilities of various possible bases at each position and conducted a comparison with the background probabilities (usually the probabilities of random occurrence), thereby obtaining the bits value for each position. The value directly reflects the preference of our base editing tool for a certain base: a higher bits value indicates stronger recognition ability of the tool for that base, while a lower bits value suggests a relatively lower requirement for sequence specificity. To visually present these analysis results, we generate a sequence logo map. The above steps was achieved by utilizing the WebLogo software (version 3.7.12, https://github.com/WebLogo/weblogo) to calculate bits value and generate sequence logos based on the bits values. These logos graphically show the base preferences at each position in the sequence, making the results more intuitive and understandable.

Next, to fairly compare the contributions of different TAMs, we classify all reads by the types of TAM, then we calculate the edit efficiency  corresponding to each TAM.




# How to use:
## Dependence
pleas make sure you have the following dependence installed.
```
tqdm
seaborn
matplotlib
pandas
jupyter
```

## Usage
1. Analyse the NGS data with [NGS_Tools](https://github.com/Masterchiefm/NGS_Tools) or [CRISPResso2](https://github.com/pinellolab/CRISPResso2/tree/master/CRISPResso2).
2. If your base editor work, download this project and copy the notebook to the result folder, then run the notebook.
3. You will see these figure including sequence logo, ratio ranking, edit efficiency...
