# Command Line Tools for Genomic Data Science_Grade3

## Grad3

### Question 1
How many sequences were in the genome?

    grep -c "^>" wu_0.v7.fas
Ans:

    7

### Question 2
What was the name of the third sequence in the genome file? Give the name only, without the “>” sign.

    grep "^>" wu_0.v7.fas|head -n 3|tail -n 1
Ans:

    Chr3

### Question 3
What was the name of the last sequence in the genome file? Give the name only, without the “>” sign.

    grep "^>" wu_0.v7.fas|head -n 3|tail -n 1
Ans:
    
    mitochondria

### Question 4
How many index files did the operation create?

    mkdir wu_0
    bowtie2-build wu_0.v7.fas wu_0
Ans:
    
    6
    
### Question 5
What is the 3-character extension for the index files created?

Ans:
    
    bt2

### Question 6
How many reads were in the original fastq file?

    wc –l wu_0_A_wgs.fastq 
Ans:

    147354

### Question 7
How many matches (alignments) were reported for the original (full-match) setting? Exclude lines in the file containing unmapped reads.

    bowtie2 -x wu_0/wu_0 -U wu_0_A_wgs.fastq -S out.full.sam
    samtools view out.full.sam|cut -f 3|grep -v "*"|wc -l
Ans:

    137719

### Question 8
How many matches (alignments) were reported with the local-match setting? Exclude lines in the file containing unmapped reads.

    samtools view out.local.sam|cut -f 3|grep -v "*"|wc -l
Ans:

    141044


### Question 9
How many reads were mapped in the scenario in Question 7?

    samtools view out.full.sam|cut -f 1,3|grep -v "*"|cut -f 1 |sort -u|wc -l
Ans:

    137719
### Question 10
How many reads were mapped in the scenario in Question 8?

    samtools view out.local.sam|cut -f 1,3|grep -v "*"|cut -f 1 |sort -u|wc -l
Ans:

    141044

### Question 11
How many reads had multiple matches in the scenario in Question 7? You can find this in the bowtie2 summary; note that by default bowtie2 only reports the best match for each read.

Ans:

    43939
    
### Question 12
How many reads had multiple matches in the scenario in Question 8? Use the format above. You can find this in the bowtie2 summary; note that by default bowtie2 only reports the best match for each read.

Ans:

    56105
    
### Question 13
How many alignments contained insertions and/or deletions, in the scenario in Question 7?

    samtools view out.full.sam|cut -f 1,6|grep "D"|cut -f1 >a.txt
    samtools view out.full.sam|cut -f 1,6|grep "I"|cut -f1 >b.txt
    cat a.txt b.txt |sort -u|wc -l
Ans:

    83561
    
### Question 14
How many alignments contained insertions and/or deletions, in the scenario in Question 8?

    samtools view out.local.sam|cut -f 1,6|grep "D"|cut -f1 >a.txt
    samtools view out.local.sam|cut -f 1,6|grep "I"|cut -f1 >b.txt
    cat a.txt b.txt |sort -u|wc -l
    
Ans:

    83445
    
### Question 15
How many entries were reported for Chr3?

    samtools view -bT wu_0.v7.fas out.full.sam > out.full.bam
    #then sorting it:
    samtools sort out.full.bam out.full.sorted
    
    samtools mpileup -f wu_0.v7.fas -uv out.full.sorted.bam > out.full.mpileup.vcf
    cat out.full.mpileup.vcf | grep -v "^#" | cut -f1 | grep -c "^Chr3"
    
Ans:

    360295

### Question 16
How many entries have ‘A’ as the corresponding genome letter?

    cat out.full.mpileup.vcf | grep -v "^#"|cut -f4|grep "^A$" |wc -l
    
Ans:

    1150985
    
### Question 17
How many entries have exactly 20 supporting reads (read depth)?

    cat out.full.mpileup.vcf | grep -v "^#"|cut -f8|grep "DP=20;" |wc -l

Ans:

    1816
    
### Question 18
How many entries represent indels?

    cat out.full.mpileup.vcf | grep -v "^#"|grep -c "INDEL"
    
Ans:

    1972

### Question 19
How many entries are reported for position 175672 on Chr1?

    cat out.full.mpileup.vcf | grep -v "^#"|cut -f 1,2|grep "175672$"|grep "Chr1"
Ans:

    2

### Question 20
How many variants are called on Chr3?

    samtools mpileup -f wu_0.v7.fas -g out.full.sorted.bam > out.full.mpileup.bcf
    bcftools call -m -v -O v out.full.mpileup.bcf > out.final.vcf
    cat out.final.vcf | grep -v "^#" |  cut -f1 | sort | uniq -c | grep "Chr3"
    
Ans:

    398
    
### Question 21
How many variants represent an A->T SNP? If useful, you can use ‘grep –P’ to allow tabular spaces in the search term.

    cat out.final.vcf | grep -v "^#" |cut -f4,5|grep -P "^A\tT$"|wc -l
Ans:

    392

### Question 22
How many entries are indels?

    cat out.final.vcf | grep -v "^#" |grep "INDEL"|wc -l
Ans:

    320

### Question 23
How many entries have precisely 20 supporting reads (read depth)?

    cat out.final.vcf | grep -v "^#" |grep "DP=20;"|wc -l
Ans:

    2

### Question 24
What type of variant (i.e., SNP or INDEL) is called at position 11937923 on Chr3?
    
    cat out.final.vcf | grep -v "^#" |grep -P "Chr3\t11937923"|wc -l
    
Ans:

    SNP

