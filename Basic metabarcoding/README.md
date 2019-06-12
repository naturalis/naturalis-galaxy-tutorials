# Basic metabarcoding tutorial
This tutorial assumes that you have a basic understanding about what galaxy is and why we use it. And you need to have an [activated account](https://github.com/naturalis/naturalis-galaxy-tutorials/tree/master/Create%20account) and be able to [upload](https://github.com/naturalis/naturalis-galaxy-tutorials/tree/master/Upload%20files) files. The [example file](https://github.com/naturalis/naturalis-galaxy-tutorials/raw/master/Basic%20metabarcoding/example_files/bulk_samples.zip) that is used for this tutorial can you find in de example_files folder.

**1.Upload [bulk_samples.zip](https://github.com/naturalis/naturalis-galaxy-tutorials/raw/master/Basic%20metabarcoding/example_files/bulk_samples.zip)**
<br />
The first step is to upload the example file, make sure that before you click on the start button you have slected the file type "zip". If you dont know how to do that check out this [page](https://github.com/naturalis/naturalis-galaxy-tutorials/tree/master/Upload%20files)
<br />

**2.Merge the paired end reads**
<br />
The first step is to merge the paird-ends, sometimes this is also called doing a paired-end assembly. In galaxy you do this with a tool called "Merge reads"(1). The most left panel is called the tool panel(2) and there you can find all the tools that you need. You can also search for tools by using "search tools" field(3). The screen looks like this:<br />
<br />
![merge](https://github.com/naturalis/naturalis-galaxy-tutorials/blob/master/Basic%20metabarcoding/img/basic_merge.jpg)
<br />
Every tool has an input field and a number of different parameter options. For this tutorial we use the default values but if you are going to analyse your own dataset feel free to make adjustments. In the following table there is a short explanation:
<br />

| Parameter | Description |
| --- | --- | 
| input type | Does your zip contain .gz or fastq files  |
| Minimum overlap | The minimum required overlap length between two reads to provide a confident overlap |
| Maximum overlap | The maximum allowed overlap, if this option is set to low you will get a warning in the log  |
| mismatch ratio | Maximum allowed ratio between the number of mismatched base pairs and the overlap length. Two reads will not be combined with a given overlap if that overlap results in a mismatched base density higher than this value. |
| combine read pairs in both orientations |  Also try combining read pairs in the "outie" orientation. Only use this option if you know what you are doing.  |
| Output | This parameter has three pre-defined options. It determines which files will be written to the output |

Make sure you select the bulk_samples.zip file as input and click on the execute button. After clicking on this button you will get two new "history blocks" in most right panel. If the block is yellow the tool is running, green means the tool is finished and with red there is something wrong. When the tool in finished you can click on the view icon to view or download your data. You can open a history block by clicking on the link, it and this gives you a few more options like a dowload button. Fow now take a look at the log output.
<br />
![merge_log](https://github.com/naturalis/naturalis-galaxy-tutorials/blob/master/Basic%20metabarcoding/img/basic_merge_log_output.jpg)

