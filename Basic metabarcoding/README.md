# Basic metabarcoding tutorial
This tutorial assumes that you have a basic understanding about what galaxy is and why we use it. And you need to have an [activated account](https://github.com/naturalis/naturalis-galaxy-tutorials/tree/master/Create%20account) and be able to [upload](https://github.com/naturalis/naturalis-galaxy-tutorials/tree/master/Upload%20files) files. The [example file](https://github.com/naturalis/naturalis-galaxy-tutorials/raw/master/Basic%20metabarcoding/example_files/bulk_samples.zip) that is used for this tutorial can you find in de example_files folder.

**1. Upload [bulk_samples.zip](https://github.com/naturalis/naturalis-galaxy-tutorials/raw/master/Basic%20metabarcoding/example_files/bulk_samples.zip)**
<br />
The first step is to upload the example file, make sure that before you click on the start button you have slected the file type "zip". If you dont know how to do that check out this [page](https://github.com/naturalis/naturalis-galaxy-tutorials/tree/master/Upload%20files)
<br />

**2. Merge the paired end reads**
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

Make sure you select the bulk_samples.zip file as input and click on the execute button. After clicking on this button you will get two new "history blocks" in most right panel. If the block is yellow the tool is running, green means the tool is finished and with red there is something wrong. When the tool in finished you can click on the view icon to view or download your data. You can open a history block by clicking on the link, it and this gives you a few more options like a dowload button. Fow now take a look at the log output, a combining percentage of around 98% is good so we can proceed.
<br />

![merge_log](https://github.com/naturalis/naturalis-galaxy-tutorials/blob/master/Basic%20metabarcoding/img/basic_merge_log_output.jpg)

<br />

**3. Trim primers**<br />
The primer sequences always need to be trimmed off, in galaxy you can do this with a tool called "Trim primers". In this tutorial we want to trim off the primers and only want to work with reads where both the forward and reverse primers are found. For the example data the following primer sequences are used:

| Orientation | sequence |
| --- | --- | 
| forward | GACWGGWTGRACWGTNTAYCC  |
| reverse | TGRTTYTTYGGNCAYCCHGAC |

You need to fill in the primer sequence in the orientation on how you can find it back in your fastq files. Often this means that you need to reverse complement it first. The make a sequence reverse complement you can for example use this website: http://arep.med.harvard.edu/labgc/adnan/projects/Utilities/revcomp.html

Your window with settings should look like something like this:

![trim_primers_parameters](https://github.com/naturalis/naturalis-galaxy-tutorials/blob/master/Basic%20metabarcoding/img/trim_primers_parameters.jpg)

In the following table there is a short explanation:

| Parameter | Description |
| --- | --- | 
| input type | Does your zip contain .gz or fastq files  |
| Settings mode | This parameter determines the output and which settings you need to fill in later. <br /> <ul><li>Trim forward primers only, look only for the forward primers and trim it off. Only if the primer is found the read will be written to the output file</li><li>Trim reverse primers only, look only for the forward primers and trim it off. Only if the primer is found the read will be written to the output file</li><li>Both need to be present, check the forward and reverse primer are present and trim it off. Only if both primers are found the read will be written to the output file</li><li>Both need to be present and are anchored, check if the forward and reverse primer are present on the very outside of the read and trim it off. Only if both primers are found the read will be written to the output file</li><li>Forward needs to be present, reverse is optional. This first checks if the forward primer is present and trims it off. If the forward primer is found the reverse primer will be checked. The read is written to the output file if the forward primer is found</li></ul> |
| Minimum number of bases that need to match | Since Cutadapt allows partial matches between the read and the adapter sequence, short matches can occur by chance, leading to erroneously trimmed bases. To reduce the number of falsely trimmed bases, the alignment algorithm requires that, by default, at least five bases match between adapter and read  |
| Minimum  | All searches for adapter sequences are error tolerant. Allowed errors are mismatches, insertions and deletions. The level of error tolerance is adjusted by specifying a maximum error rate, which is 0.1 (=10%) by default.  |
| Minimum read length  | Discard processed reads that are shorter than this length  |
| Output untrimmed sequences | When this is set to yes you will can an extra outputfile containing the untrimmed reads  |

<br />

**4. Check length distribution**<br />
A good and easy check if your primers worked and amplified your target is to check the length distribution. This is the length of the sequences in your FASTQ files. Beforehand you mostly know the length or range of lengths of your target. You can check this with the "Sequence analyzer" tool. As input for this tool you can use the output of step 3. After executing this tool you will get more information then only the length distribution. In this basic tutorial we will not look at the other information. The graph will look like something like this:
![length_distribution](https://github.com/naturalis/naturalis-galaxy-tutorials/blob/master/Basic%20metabarcoding/img/length_distribution.jpg)

**5. Filter on length**<br />
As you can see on the output of step 4 there are a few reads smaller then the expected target. With this example data it is not clear to see that in the bar chart but you can see that there are reads found with a length of 13bp. The expected length of the exampel data is between 310 and 320 bp. We are not interested in reads smaller or longer so we need to filter them out. You can do this with a tool called "Sequence trimmer". This tool has many parameters but for now we only set **Minimum read length=310** and **Maximum read length=320**



