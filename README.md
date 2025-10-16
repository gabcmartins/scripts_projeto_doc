#Preparing data for analyses
1. When files are at SRA: script_get_sra #make sure to have a .txt file with accession numbers
2. Removing adapters and low quality sequences: script_filtering_fastp
3. Download and index of human genome: script_get_human_genome_GRch38
4. Align human genome and reads: script_align_reads_human_genome
5. Remove aligned sequences with samtools: script_remove_human_genome

Generating contigs
1. Merge of paired-end sequences with flash: script_flash #non-essential step, but improves megahit assembling. #caution: do not exclude fastq R1 and R2 original files after the merge.
2. Contig assembling with megahit: script_megahit

Generating genes relative abundance 
1. Prediction of coding dna sequences with prodigal: prodigal_script 
2. Aligment of CDS and database: first use make_db, then: script_diamond
3. To calculate the abundance, first you have to index prodigal output (.fna) and then align against the reads, for this purpose do:
   - indexing_fna
   - align_fna_reads
   - convert_sam_bam_and_sort
4. Index and generate idxstats (which will provide the number of mapped reads/CDS): indexing_idxstats
5. To filter the best aligments of diamond output, use: filtering_diamong_output
6. To organize idxstats output and calculate RPKM for normalization, use: treating_idxstats
7. To merge idxstats results with diamond output (now you will actually have rpkm and cds matches): joining_idxstats_diamond
Important: scripts 5,6 and 7 of this list are in Python. 
   
