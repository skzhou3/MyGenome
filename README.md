# MyGenome
*The following is a basic record of the methods and results from the whole genome assembly of rice blast fungus, Pyricularia oryzae.*

## Sequence quality assessment
*Upload and assess the quality of the forward and reverse sequences. Trim if adaptor content is above 5%.*
1. Upload sequences as .gz files.
2. Run both forward and reverse sequences through FastQC for quality assessment.
```
fastqc Pd8825_1.fq.gz
fastqc Pd8825_2.fq.gz
```
NOTE: For ease of access, the resulting .html files generated by FastQC can be uploaded to the local computer. From the FastQC, it is clear that the overall quality is high, however, adaptor content is still present (~12%). 
![Sequence Quality Base](https://github.com/user-attachments/assets/439a15a1-7d5e-421c-8b23-422fad38200a)
![Sequence Quality Tile](https://github.com/user-attachments/assets/124917e4-0c8d-4286-be62-97d4e591c8e4)
![Initial Adaptor Content](https://github.com/user-attachments/assets/cb921a02-5f58-43b1-9931-6fe725bc103a)
*Images above are from the forward reads.*

## Trimming
*To remove adaptor content, the following Trimmomatic command-line was used to trim both forward and reverse sequences.*
1. Run customized Trimmomatic command.
```
java -jar ~/sequences/trimmomatic-0.38.jar PE -threads 2 -phred33 -trimlog Pd8825_errorlog.txt Pd8825_1.fq Pd8825_2.fq Pd8825_1_paired.fastq Pd8825_1_unpaired.fastq Pd8825_2_paired.fastq Pd8825_2_unpaired.fastq ILLUMINACLIP:adaptors.fasta:2:30:10 SLIDINGWINDOW:20:20 MINLEN:140
```
2. Run paired sequences through FASTQC to assess the quality of the trimming.
```
fastqc Pd8825_1_paired.fastq
fastqc Pd8825_2_paired.fastq
```
*Another FastQC revealed the adaptor content reduced to ~2% in the resulting trimmed sequences.*
![image](https://github.com/user-attachments/assets/5f2530df-92b9-40e7-944a-37dc20904694)

The following table summarizes the results from Trimmomatic:

|  Sequence  | Reads | Adaptor Content |
| ------------- | ------------- | -------------- |
| Raw Forward  | 7692782  | ~12% |
| Raw Reverse  | 7692782  | ~12% |
| Trimmed Forward  | 6356740  | ~2% |
| Trimmed Reverse  | 6356740  | ~2% |

***NOTE:** HTML files from the FastQC before and after trimming can be found under the `FastQC` directory.*
## Assembly
Prepare for genome assembly by transferring files from virtual machine to MCC. 
1. Log into MCC.
2. 
