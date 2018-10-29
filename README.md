# Naturalis Galaxy Tutorial
A "how to" tutorial for the use of the Naturalis Galaxy pipeline

## Analysing a mixed amplicon dataset
This tutorial will show a step by step introduction of the Naturalis Galaxy pipeline. The tutorial will use an example dataset that was sequenced paired-end with the Illumina MiSeq. This dataset consist out of environmental air samples collected in Leiden. The dataset contains ITS (Internal Transcribed Spacer region) sequences packaged in six .fastq files.

### Preparations:
In order to start this tutorial, the example dataset will need to be downloaded and an account on the Naturalis Galaxy instance will need to be created.
* The example dataset in .zip format can be downloaded [here](https://drive.google.com/open?id=1NrdTEC7X2QFrMDJX640B3N5NRp5kRs_R).
* Create an account by clicking on ´you may create one´. And fill in the form.    
![Link to account creation form](https://github.com/JasperBoom/naturalis-galaxy-tutorial/blob/master/src/CreateAccountFull.PNG)
* Make sure to verify your email address.

### Step 1:
Upload the example dataset to the Naturalis Galaxy instance.  
Files of almost any kind can be uploaded to Galaxy. This is done by clicking on upload button in the upper left corner.
* Click on the “up” arrow in the upper left corner (next to the “**Tools**” menu name).  
![Upload file button](https://github.com/JasperBoom/naturalis-galaxy-tutorial/blob/master/src/UploadFull.PNG)
* Select the “Tutorial_Samples.zip” file.  
![Button for file choosing](https://github.com/JasperBoom/naturalis-galaxy-tutorial/blob/master/src/UploadSelectFull.PNG)
* Manually set the format for the file to “zip”.  
![Search field for file format](https://github.com/JasperBoom/naturalis-galaxy-tutorial/blob/master/src/UploadManualFull.PNG)
* Click on "start" to submit the dataset.  
![Button for starting file upload](https://github.com/JasperBoom/naturalis-galaxy-tutorial/blob/master/src/UploadStartFull.PNG)
* The dataset will show up in the Galaxy history panel on the right side of the screen.  
![History panel](https://github.com/JasperBoom/naturalis-galaxy-tutorial/blob/master/src/HistoryPanelFull.PNG)

### Step 2:
Merge Illumina paired-end reads.  
The example dataset exists of 6 .fastq files. Every 2 files are linked as pairs. Those pairs need to be merged into single reads.
* Select the "Merge reads" tool under "**Processing Tools**".
* Select the "**Tutorial_Samples.zip**" under "**zip file containing fasta or fastq files**".
* Further settings can be kept at default.
```
Minimum overlap --> 10
Maximum overlap --> 300
Mismatch ratio  --> 0.25
Output          --> Output merged reads only
```
![History panel merged reads](https://github.com/JasperBoom/naturalis-galaxy-tutorial/blob/master/src/MergedReadsFull.PNG)

### Step 3:
Trim Illumina primers.  
The example dataset has now been merged. However, it still contains universal ITS primers. These need to be trimmed off in order to gain organism specific reads.
* Select the "CuAdapt Sequence Trimmer" tool under "**Processing Tools**".
* Select "Zip file" under "**FastQ or zip?**"
* Select "**Tutorial_Samples.zip zip**" (the output file from step 2) under "**Zip file.**"
* Change the settings below. Remaining settings can be kept at default.
```
Trim reads at the 5'-end
Trim reads at the 3'-end
```
![Sequence trimmer options](https://github.com/JasperBoom/naturalis-galaxy-tutorial/blob/master/src/PrimerTrimmingFull.PNG)
* The output is displayed in the Galaxy history panel.  
![History panel trimmed primers](https://github.com/JasperBoom/naturalis-galaxy-tutorial/blob/master/src/HistoryPanelPrimerTrimmingFull.png)

### Step 4:
Run sequence analyzer.  
With the universal ITS primers trimmed off, the reads are ready for a sequence analyzer.
* Select the "PRINSEQ Sequence Analyzer" tool under "**Analysis Tools**".
* Select "Zip file" under "**Single or zip file?**".
* Select "FastQ file(s)" under "**FastQ or fastA file(s).**".
* Select "**Trimmed_Zip**" (the output file from step 3) under "**Zip file.**".

The tool will output a file with a length distribution graphic.  
![Sequence analyzer output](https://github.com/JasperBoom/naturalis-galaxy-tutorial/blob/master/src/SequenceAnalyzerOne.PNG)  
Based on this distribution, another set of trimming options can be determined.  
The clustering methods UPARSE and UNOISE available in the Naturalis Galaxy pipeline require input that is as much of the same length as possible.

### Step 5:
Trim reads to same length.  
