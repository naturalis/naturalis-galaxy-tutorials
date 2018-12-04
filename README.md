# Naturalis Galaxy Tutorial
A "how to" tutorial for the use of the Naturalis Galaxy pipeline.

## Analysing a mixed amplicon dataset
This tutorial will show a step by step introduction of the Naturalis Galaxy pipeline. The tutorial will use an example dataset that was sequenced paired-end with the Illumina MiSeq. This dataset consists of environmental air samples collected in Leiden. The dataset contains ITS (Internal Transcribed Spacer region) sequences packaged in six .fastq files.

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
* Select the "CutAdapt Sequence Trimmer" tool under "**Processing Tools**".
* Select "Zip file" under "**FastQ or zip?**".
* Select "**Tutorial_Samples.zip zip**" (the output file from step 2) under "**Zip file.**".
* Change the settings below. Remaining settings can be kept at default.
```
Trim reads at the 5'-end --> 25
Trim reads at the 3'-end --> 25
```
![Sequence trimmer options](https://github.com/JasperBoom/naturalis-galaxy-tutorial/blob/master/src/PrimerTrimmingFull.PNG)

The output is displayed in the Galaxy history panel.  
![History panel trimmed primers](https://github.com/JasperBoom/naturalis-galaxy-tutorial/blob/master/src/HistoryPanelPrimerTrimmingFull.png)

### Step 4:
Run a sequence analysis.  
With the universal ITS primers trimmed off, the reads are ready for a sequence analyzer.
* Select the "PRINSEQ Sequence Analyzer" tool under "**Analysis Tools**".
* Select "Zip file" under "**Single or zip file?**".
* Select "FastQ file(s)" under "**FastQ or fastA file(s).**".
* Select "**Trimmed_Zip**" (the output file from step 3) under "**Zip file.**".

The tool will output a file with a length distribution graphic.  
![Sequence analyzer output](https://github.com/JasperBoom/naturalis-galaxy-tutorial/blob/master/src/SequenceAnalyzerOne.PNG)  
Based on this distribution, another set of trimming options can be determined.  
The clustering methods UPARSE and UNOISE available in the Naturalis Galaxy pipeline work best with input that is as much of the same length as possible (without losing/trimming off to much of your dataset).

### Step 5:
Trim reads to same length.  
The majority of reads, and the largest peak can be found at a length of 359. Everything beyond that length can be cut back to 359 from the 3’-end, this way you retain relevant information, but still achieve a smaller length distribution. Anything below a length of 300 can be discarded.  
![Sequence length distribution](https://github.com/JasperBoom/naturalis-galaxy-tutorial/blob/master/src/LengthTrimmingFull.PNG)
* Select the "CuAdapt Sequence Trimmer" tool under "**Processing Tools**".
* Select "Zip file" under "**FastQ or zip?**".
* Select "**Trimmed_Zip**" (the output file from step 4) under "**Zip file.**".
* Change the settings below. Remaining settings can be kept at default.
```
Trim reads from 3'-end to certain legnth --> 359
Discard reads below certain length       --> 300
```
The results of this trimming can be checked by doing another sequence analysis.  
![Sequence length analysis](https://github.com/JasperBoom/naturalis-galaxy-tutorial/blob/master/src/SequenceAnalyzerTwo.PNG)

### Step 6:
Clustering and OTU generation.  
The example dataset has now been prepared for clustering. The clustering method for this tutorial will be UPARSE.
* Select the "Make otu table" tool under "**Cluster Tools**".
* Select "**Trimmed_Zip**" (the output file from step 5) under "**zip file containing fasta or fastq files**".
* Select "UPARSE" under "**Clustering**".
* Remaining settings can be kept at default.

The output table will look like this. This file will be named "**Trimmed_Zip otu table**".  
![OTU output table one](https://github.com/JasperBoom/naturalis-galaxy-tutorial/blob/master/src/OTUTableOne.PNG)  
Along with the OTU table. A sequence file has been generated named "Trimmed Zip sequence".  
The third file "Trimmed_Zip log" will not be used in this tutorial.  

### Step 7:
Identifying OTUs.  
The newly generated file named "**Trimmed_Zip sequence**" contains a representative read for every generated OTU. These reads can be used to identify the species linked to a OTU.
* Select the "Identify reads with blastn and find taxonomy" tool under "**Identification Tools**".
* Select "**Trimmed_Zip sequence**" (the output file from step 6) under "**fasta file**".
* Select "ITS (Genbank 22-11-2018)" under "**Database**".
* Change the settings below. Remaining settings can be kept at default.
```
Identity percentage cutoff --> 90
```
The output BLAST table will contain 114 lines and look like this. The file will be named "**Trimmed_Zip sequence BLAST original taxonomy**".  
![BLAST output table one](https://github.com/JasperBoom/naturalis-galaxy-tutorial/blob/master/src/BLASTTableOne.PNG)  
This file contains a lot of information.  
* Query ID: this column shows which OTU the identification belongs to.
* Subject: this column is the full name of the database entry used for the identification.
* Identity percentage: this column contains a percentage specific to every identification, the percentage shows how much the query and the database reference are alike, 100% is a very good identification.
* Source: this column shows the reference database used to retrieve the taxonomy information.
* Taxonomy: this column shows the full taxonomic information for an identification, starting at Kingdom / Phylum / Class / Order / Family / Genus / Species.
