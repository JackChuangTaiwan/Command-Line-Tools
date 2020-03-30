# Command Line Tools for Genomic Data Science_Grade2
## Grade2

### Question 1
How many alignments does the set contain?
   
    samtools view athal_wu_0_A.bam | wc -l
Ans:
    221372
### Question 2
How many alignments show the read’s mate unmapped?
   
    samtools view athal_wu_0_A.bam| cut -f 7 |grep -c '*'
Ans:

    65521
### Question 3
How many alignments contain a deletion (D)?

    samtools view athal_wu_0_A.bam| cut -f 6 |grep "D"|wc -l
Ans:
    
    2451

### Question 4
How many alignments show the read’s mate mapped to the same chromosome?

    samtools view athal_wu_0_A.bam| cut -f 7 |grep -c '='
Ans:
    
    150913

### Question 5
How many alignments are spliced?

    samtools view athal_wu_0_A.bam| cut -f 6 |grep "N"|wc -l
Ans:

    0

### Question 6
How many alignments does the set contain?

    samtools sort athal_wu_0_A.bam athal_wu_0_A.sorted
    samtools index athal_wu_0_A.sorted.bam
    samtools view athal_wu_0_A.sorted.bam "Chr3:11777000-11794000" |wc -l

Ans:
    
    7081

### Question 7
How many alignments show the read’s mate unmapped?

    samtools view athal_wu_0_A.sorted.bam "Chr3:11777000-11794000"| cut -f 7|grep -c "*"
Ans:

    1983
### Question 8
How many alignments contain a deletion (D)?
    
    samtools view athal_wu_0_A.sorted.bam "Chr3:11777000-11794000"| cut -f 6|grep -c "D"
Ans:
    
    31

### Question 9
How many alignments show the read’s mate mapped to the same chromosome?

    samtools view athal_wu_0_A.sorted.bam "Chr3:11777000-11794000"| cut -f 7|grep -c "="

Ans:

    4670
    
### Question 10
How many alignments are spliced?

    samtools view athal_wu_0_A.sorted.bam "Chr3:11777000-11794000"| cut -f 6|grep -c "D"
Ans:

    0
### Question 11
How many sequences are in the genome file?

    samtools view -H athal_wu_0_A.bam |grep -c "SN"
Ans:

    7
    
### Question 12
What is the length of the first sequence in the genome file?

    samtools view -H athal_wu_0_A.bam |grep "SN"|head -n 1|cut -f 3
Ans:

    29923332

### Question 13
What alignment tool was used?
    
    samtools view -H athal_wu_0_A.bam
Ans:

    stampy
    

### Question 14
What is the read identifier (name) for the first alignment?

    samtools view athal_wu_0_A.bam |head -n 1|cut -f 1
Ans:
    
    GAII05_0002:1:113:7822:3886#0

### Question 15
What is the start position of this read’s mate on the genome? Give this as ‘chrom:pos’ if the read was mapped, or ‘*” if unmapped.

    samtools view athal_wu_0_A.bam |head -n 1|cut -f 3,4
Ans:

    Chr3:11700332

### Question 16
How many overlaps (each overlap is reported on one line) are reported?

    bedtools intersect -a athal_wu_0_A.bam -b athal_wu_0_A_annot.gtf -bed -wo > overlaps.bed
    wc -l overlaps.bed

Ans:

    3101

### Question 17
How many of these are 10 bases or longer?

    cut -f22 overlaps.bed | sort -nrk1 > lengths
Ans:

    2899
    
### Question 18
How many alignments overlap the annotations?

    wc -l overlap.bed
Ans:

    3101   

### Question 19
Conversely, how many exons have reads mapped to them?
    
    cut -f 13-21 overlaps.bed |sort -u|wc -l
Ans:

    21

### Question 20
If you were to convert the transcript annotations in the file “athal_wu_0_A_annot.gtf” into BED format, how many BED records would be generated?

    cut -f 9 athal_wu_0_A_annot.gtf | cut -d " " -f 1,2 | sort -u | wc -l
    
Ans:
   
    4