# Command Line Tools for Genomic Data Science_Grade1
## Grade1

### Question 1
How many chromosomes are there in the genome?

     grep chr apple.genome |wc -l


Ans:

    3

### Question 2
How many genes?

    cut -f 1  apple.genes|sort  -u|wc -l
    
Ans:

    5453
### Question 3
How many transcript variants?
    
    cut -f 2  apple.genes|sort  -u|wc -l
    
Ans:

    5456
    
### Question 4
How many genes have a single splice variant?
    
    cut -f 1,2  apple.genes|sort -u|cut -f1|uniq -c|grep "      1" |wc -l
Ans:

    5450
### Question 5
How may genes have 2 or more splice variants?

    cut -f 1,2  apple.genes|sort -u|cut -f1|uniq -c|grep -v "      1"|wc -l

Ans:
    
    3

### Question 6
How many genes are there on the ‘+’ strand?

    cut -f 1,4  apple.genes|grep '+'|sort -u|wc -l

Ans:

    2662
### Question 7
How many genes are there on the ‘-’ strand?

    cut -f 1,4  apple.genes|grep '-'|sort -u|wc -l

ANS:

    2791

### Question 8
How many genes are there on chromosome chr1?

    cut -f 1,3  apple.genes|grep 'chr1'|sort -u |wc -l

Ans

    1624
### Question 9
How many genes are there on each chromosome chr2?

    cut -f 1,3  apple.genes|grep 'chr2'|sort -u |wc -l

Ans

    2058
### Question 10
How many genes are there on each chromosome chr3?

    cut -f 1,3  apple.genes|grep 'chr3'|sort -u |wc -l

Ans

    1771
### Question 11
How many transcripts are there on chr1?

    cut -f 2,3  apple.genes|grep 'chr1'|sort -u |wc -l

Ans

    1625
### Question 12
How many transcripts are there on chr2?

    cut -f 2,3  apple.genes|grep 'chr2'|sort -u |wc -l

Ans

    2059
    
### Question 13
How many transcripts are there on chr3?

    cut -f 2,3  apple.genes|grep 'chr3'|sort -u |wc -l

Ans

    1772
    
### Question 14
How many genes are in common between condition A and condition B?

    cut -f 1 apple.conditionA|sort -u > apple.condA.sorted.genes
    cut -f 1 apple.conditionB|sort -u > apple.condB.sorted.genes
    comm -1 -2 apple.condA.sorted.genes apple.condB.sorted.genes |wc -l
    
Ans:

    2410

### Question 15
How many genes are specific to condition A?

    cut -f 1 apple.conditionA|sort -u > apple.condA.sorted.genes
    cut -f 1 apple.conditionB|sort -u > apple.condB.sorted.genes
    cut -f 1 apple.conditionC|sort -u > apple.condC.sorted.genes
    cat apple.condC.sorted.genes apple.condB.sorted.genes|sort -u > mergeBC.genes
    comm -2 -3 apple.condA.sorted.genes mergeBC.genes|wc -l

Ans:
    
    387
### Question 16
How many genes are specific to condition B?

    cat apple.condA.sorted.genes apple.condC.sorted.genes|sort -u > mergeAC.genes
    comm -2 -3 apple.condB.sorted.genes mergeAC.genes|wc -l

Ans:

    398
    
### Question 17
How many genes are in common to all three conditions?

    cut –f1 apple.conditionC | sort –u > apple.condC.sorted.genes
    cat apple.cond{A,B,C}.sorted.genes |sort|uniq -c|grep " 3 "|wc -l  
Ans:

    1608
    
    
