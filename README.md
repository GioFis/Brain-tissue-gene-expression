# Brain-tissue-gene-expression

Human RNA-Seq dataset 
composed by 36 samples from 6 tissues.
• Data have been preprocessed by us in order to discard:
  − genes with low quality or inconsistent annotations
  − Mitochondrial genes
  − tRNAs and rRNAs
• Of the ~ 56k human genes that are annotated in the latest GenCode annotation, only 28266 high  quality genes have been retained 
See https://www.gencodegenes.org/ for more details

For each sample we have the raw expression values (read counts) for
   − 18829 (high quality) protein coding genes and 
   − 9438 (high quality) non protein coding RNAs (6520 lincRNA, 1780 snRNAs and 1137 miRNAs)
   
The dataset consists of 3 (tab delineated) files:
− Counts.csv: a table containing gene expression values (read 
counts) for the 28266 human genes. Since we have 6 tissues and 
6 biological replicates, a total of 36 replicates (columns) are 
included in the file 
− Annot.csv: a table containing the annotation (gene symbol and class) for the 28266 genes
− Design.csv: a table containing the design of the RNAseq experiment (i.e the tissue, individual and sex associated to each biological replicate)

See https://gtexportal.org/home/publicationsPage for a complete list of the publications associated with the GTEX project

PART 1

We used the edgeR package in order to:
− 1 read the data into a dgeList object
− 2 keep only genes that are likely to be expressed (i.e genes that have more 
than 10 reads in at least 2 replicates)
− 3 perform normalization (both for library size and composition)
− 4 perform a MDS (~PCA) plot of the data
− 5 select 2 different (and meaningful, that is not too close on the PCA plot) 
biological conditions and perform a differential expression analysis using the 
exactTest() function
− 6 create a topTags type of edgeR object containing the list of differentially expressed genes (DEGs)DEGs should have a FDR <= 0.01

− 7 Assign all the genes into one of the 4 possible classes: 
        DE_UP (FDR<=0.01 and logFC>0), 
        DE_DOWN (FDR<=0.01 and logFC>0), 
        notDE_UP (FDR<=0.01 and logFC>0), 
        notDE_DOWN (FDR<=0.01 and logFC>0), and then do a 
boxplot of the logFC of the genes belonging to each class

PART 2

− Perform a PCA (principal component analysis) to ascertain whether 
there is some separation between biological replicates of different 
sexes
− For each tissue, consider only genes expressed (>10 reads in at 
least 2 replicates) in that tissue.
− Use edgeR (exactTest) to perform a differential expression analysis
− Consider all the genes that show a FDR <= 0.05 as “sex specific” 
DEGs
− Draw a Venn Diagram of the Sex specific genes between the 2 tissues considered
− Draw a Venn Diagram between the DEGs (as identified in the common part) and genes that show Sex specific expression in at least one of the tissues considered
