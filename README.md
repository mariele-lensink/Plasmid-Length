# Plasmid-Length
Program uses raw reads from Oxford Nanopore sequencing data to estimate plasmid size and creates a subselection of high quality reads of a similar length.

## Input
Uses a fastq file of raw reads from a single plasmid sample. Program is intended to be used with Oxford Nanopore Sequencing Data.
(currently being edited to take in .gz files)

## Output
Creates a fasta file of reads that are of similar length to the predicted length of the plasmid.

## Command Line Options
--inFile [X]      (Required) input file 
--outFile [X]     (Required) name for output file
-s                (Optional) Uses otsu threshold method to separate a the bimodal distribution of read lengths. Use this 
                  option when your data shows a greater number or short length reads than long reads.
-q                (Optional) After reads are selected, their average phred quality score will be calculated. If it is below 
                  14, they will be filtered out of the final output.
                  *using this option may lower the number of reads in your final output file*

## Example

### Default
./plasmidsizeselector.py --inFile exampleReads.fastq --outFile exampleReadsOutput.fastq

  *program will produce a single histogram plot, ideally like this:*
  ![Frequency of Read Lengths](githubexample1.jpg)
  
  *then it will write an output file called "exampleReadsOutput.fastq" (according to user input) of all of the reads from the bin with the highest count 
  
### Separating a Bimodal Distribution (using -s option)
./plasmidsizeselector.py --inFile exampleReads.fastq --outFile exampleReadsOutput.fastq -s

  *program will first produce the same initial plot as the default settting:*
  ![Frequency of Read Lengths](githubexample1.jpg)
  
  *but after calculating the threshold value between the 2 modes, will produce a second plot, this time only containg the reads after the cutoff. *
  ![Frequecny of Read Lengths Greater than Threshold Value](githubexample2.jpg)
  
  *then it will write an output file called "exampleReadsOutput.fastq" (according to user input) of all of the reads from the bin with the highest count 
