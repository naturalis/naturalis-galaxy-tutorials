# Galaxy LCA (Lowest Common Ancestor) 
A tool to determine the lowest common ancestor from BLAST results with taxonomy. This approach is partly based on MEGAN's (Huson et al., 2007) LCA method. This tool is more flexible and easier to use then MEGAN, it does not specifically use taxonids or separated mapping files. Instead, the script handles files with the taxonomy present in the last column of the input file. Those input files can be generated with our BLAST pipeline (not been published yet) or you can create them manually. Determining the lowest common ancestor can help to identify sequences that do not have a significant good blast hit. The basis of the approach for the analyses goes into the folowing order:
<br /><br />
**Step 1, determine the top percentage based on bitscore:** <br />
Of all the blast hits a sub-selection will be made of the top hits based on a percentage of the bitscore. If the top percentage is set to 8% the top will be calculated like 0.92\*bitscore best hit=top threshold. In this example, all hits with a bitscore above 294.4 will continue to the next step.   

| Query | Subject | Identity percentage | Coverage | bitscore |
| --- | --- | --- | --- | --- |
| Otu1 | hit1 | 93 | 95 | 320 |
| Otu1 | hit2 | 93 | 95 | 320 |
| Otu1 | hit3 | 91 | 94 | 310 |
| Otu1 | hit4 | 90 | 95 | 301 |
| Otu1 | hit5 | 89 | 94 | 300 |
| Otu1 | hit6 | 85 | 95 | 290 |
| Otu1 | hit7 | 84 | 95 | 290 |
| Otu1 | hit8 | 81 | 90 | 281 |
| Otu1 | hit9 | 80 | 89 | 275 |
| Otu1 | hit10 | 79 | 88 | 274 |

<br />

**Step 2, filter on threshold:** <br />
From the top hits there will be filtered on identity, coverage and bitscore. Let's choose a threshold of 90 identity, 90 coverage and 250 bitscore. All hits with scores above the thresholds will go to the next step. 

| Query | Subject | Identity percentage | Coverage | bitscore |
| --- | --- | --- | --- | --- |
| Otu1 | hit1 | 93 | 95 | 320 |
| Otu1 | hit2 | 93 | 95 | 320 |
| Otu1 | hit3 | 91 | 94 | 310 |
| Otu1 | hit4 | 90 | 95 | 301 |
| Otu1 | hit5 | 89 | 94 | 300 |

<br />

**Step 3, determine the lowest common ancestor:** <br />
Of all the remaining hits the lowest common ancestor is determined. The script starts at species level, it checks if all the hits are coming from the same species. If not it checks at genus level and so on. 

| Query | Subject | taxonomy |
| --- | --- | --- |
| Otu1 | hit1 | Animalia / Arthropoda / Insecta / Diptera / Asilidae / Scarbroughia / Scarbroughia delicatula |
| Otu1 | hit2 | Animalia / Arthropoda / Insecta / Diptera / Asilidae / Scarbroughia / Scarbroughia delicatula |
| Otu1 | hit3 | Animalia / Arthropoda / Insecta / Diptera / Asilidae / Schildia / Schildia fragilis |
| Otu1 | hit4 | Animalia / Arthropoda / Insecta / Diptera / Asilidae / Scytomedes / Scytomedes haemorrhoidalis |

With this example data and thresholds the identification of otu1 will be Asilidae. This is a basic explanation of the LCA approach, more advanced filter settings and output options are shown at the example commands.
<br />

## Getting Started
