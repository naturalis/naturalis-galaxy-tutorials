## Subset .gz.zip and Cutadapt

This short instruction is written for a specific use case where a zip-archive of gzipped fastq files\
needs to subsetted into primer specific sets (R1, R2, etc), for each set the primer has to be trimmed\
and the fastq output exported as .gz.zip again.

Import the zip-archive
![import_screenshot](https://github.com/naturalis/naturalis-galaxy-tutorials/blob/master/Manage%20zip%20and%20trim%20primer/01_import.jpg)

Display the contents of the archive with *Manage zip*
![display_content](https://github.com/naturalis/naturalis-galaxy-tutorials/blob/master/Manage%20zip%20and%20trim%20primer/%2002_display_content.jpg)

Create a subset (e.g. R1) with *Manage zip*
![create_subset](https://github.com/naturalis/naturalis-galaxy-tutorials/blob/master/Manage%20zip%20and%20trim%20primer/03_create_subset.jpg)

For convenience rename the subset (edit attributes) so the contents are clear
![edit_attributes](https://github.com/naturalis/naturalis-galaxy-tutorials/blob/master/Manage%20zip%20and%20trim%20primer/04_edit_attributes.jpg)

Select the created subset with *Trim primers* and provide the primer-sequence that needs to be trimmed;\
make sure *input type* is set to gzip files
![trim_primer](https://github.com/naturalis/naturalis-galaxy-tutorials/blob/master/Manage%20zip%20and%20trim%20primer/05_cutadapt.jpg)

Repeat these steps for additional subsets (e.g. R2).\
Trimmed subsets (here renamed R1/R2_trimmed_zip) can be downloaded as a single file after combining these\
archives with 'create zip' from *Manage zip*
![combine_archives]()
