# Naturalis Galaxy Tutorial
A "how to" tutorial for the use of the Naturalis Galaxy pipeline

## Analysing a mixed amplicon dataset
This tutorial will show a step by step introduction of the Naturalis Galaxy pipeline. The tutorial will use an example dataset that was sequenced paired-end with the Illumina MiSeq. This dataset consist out of environmental air samples collected in Leiden. The dataset contains ITS (Internal Transcribed Spacer region) sequences packaged in six .fastq files.

### Preparations:
In order to start this tutorial, the example dataset will need to be downloaded and an account on the Naturalis Galaxy instance will need to be created.
* The example dataset in .zip format can be downloaded [here](https://drive.google.com/open?id=1NrdTEC7X2QFrMDJX640B3N5NRp5kRs_R)
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
The example dataset exists out of 6 .fastq files. Every 2 files are linked as pairs. Those pairs need to be merged into single reads.
* Select the "Merge reads" tool under "**Processing tools**".
* Select the "**Tutorial_Samples.zip**" under "**zip file containing fasta or fastq files**"

