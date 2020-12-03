#################
Genome Annotation
#################

Jbrowse is a web-based genome visualisation and curation platform. The genome annotation can be generated using the annotation pipeline of interest. Galaxy_ is a bioinformatics cloud platform containing a collection of bioinformatics for handling and processin genomic data.

.. _Galaxy: https://usegalaxy.org.au/

Genome annotation using Galaxy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Maker_ is one of the popular genome annotation pipelines for annotating de novo assembly and is available on the main Galaxy (usegalaxy_).The tutorial_ of genome annotation with Maker contains a hands-on for genome annotation using Galaxy. Please see the Current Protocols (CP_)  for more details. 

.. _Maker: http://weatherby.genetics.utah.edu/MAKER/wiki/index.php/MAKER_Tutorial_for_WGS_Assembly_and_Annotation_Winter_School_2018
.. _usegalaxy: https://usegalaxy.org/
.. _tutorial: https://training.galaxyproject.org/training-material/topics/genome-annotation/tutorials/annotation-with-maker/tutorial.html

Genome annotation data
~~~~~~~~~~~~~~~~~~~~~~
Below is a list of genomic data files from the tutorial above.   
::

  https://zenodo.org/api/files/4385871d-9632-4fae-9aaf-f8ed692163d1/augustus_training_1.tar.gz
  https://zenodo.org/api/files/4385871d-9632-4fae-9aaf-f8ed692163d1/augustus_training_2.tar.gz
  https://zenodo.org/api/files/4385871d-9632-4fae-9aaf-f8ed692163d1/S_pombe_chrIII.fasta
  https://zenodo.org/api/files/4385871d-9632-4fae-9aaf-f8ed692163d1/S_pombe_genome.fasta
  https://zenodo.org/api/files/4385871d-9632-4fae-9aaf-f8ed692163d1/S_pombe_trinity_assembly.fasta
  https://zenodo.org/api/files/4385871d-9632-4fae-9aaf-f8ed692163d1/Swissprot_no_S_pombe.fasta

The Jbrowse GUI allows users to create/add a new organism by uploading the species file (e.g. FASTA) and the annotation file (e.g. gff3)
The Jbrowse requires both the raw and the index file to add new organism or tracks.

Please make sure the following files are prepared before the upload.

Organism file 
:: 
  
  1) fasta file ends with fa or fasta and index file ends with fai (if the fasta is added using command line).
  2) a genome file in 2bit format is required for the upload (e.g. species.2bit)
  Samtools can be used to create the index file with the following command.
  The 2bit file can be created using the faToTwoBit_ tool.
  e.g. 
    samtools faidx species.fasta
  e.g. 
    faToTwoBit species.fa species.2bit

.. _faToTwoBit: http://hgdownload.soe.ucsc.edu/admin/exe/linux.x86_64/faToTwoBit

Annotation file 
::
  
  Gff3 should be sorted and is required to be compressed using the bgzip tool.
  e.g.
    bgzip species.sorted.gff3
    tabix -p gff species.sorted.gff3.gz
 
Evidence Tracks (BAM) file
::
  
  The evidence track file requires both BAM file and BAM index file.
  Samtools can be used to create the BAM index file with the follwoing command.
  e.g.
    samtools index species.bam
    

If the data size (> 2G) can be made available on Jbrowse via command line. Please contact us_ after sign up on Apollo-portal_ if you want to make your data available on Jbrowse via command line. Once you have granted the access to your Apollo VM, you can prepare your data in the following manner:
::
  
  1) cd into your apollo_data folder
  2) create a folder named after your organism (e.g. organims_A)
  3) cd into organism_A folder
  4) index the organism_A.fasta using samtools (see the instrunction above)
  5) index the sorted annotation file (e.g. gff3 - see the instruction above)
  6) index the track file (e.g. BAM - see the instruction above)
  7) run prepare-refseqs.pl --fasta Organism_A.fa to prepare the genome file for Jbrowse
  8) run flatfile-to-json.pl --tracklabel Organism_A --key "Organism_A" --gff Organism_A.gff3 --trackType CanvasFeatures --type CDS --autocomplete all to prepare annotation file
  9) run generate-names.pl to make the Organism_A searchable on Jbrowse.
  Note: the perl scripts is part of and is available on apollo platform.

The folder layout
::
  
  /path/to/apollo_data
  /path/to/apollo_data/Organism_A
  /path/to/apollo_data/Organism_A/Oragnism_A.fa
  /path/to/apollo_data/Organism_A/Organism_A.fa.fai
  /path/to/apollo_data/Organism_A/Organism_A.sorted.gff3.gz
  /path/to/apollo_data/Organism_A/Oragnism_A.sorted.gff3.gz.tbi
  /path/to/apollo_data/Organism_A/Oragnism_A-sorted.bam
  /path/to/apollo_data/Organism_A/Organism_A-sorted.bam.bai
  /path/to/apollo_data/Organism_A/tracks.conf

The evidence and variant (if available) tracks can be made available by editing the tracks.conf file in the Organism_A folder in this example.

The tracks.conf file format.
::
  
  [tracks.genes]
  urlTemplate=Organism_A.sorted.gff3.gz
  storeClass=JBrowse/Store/SeqFeature/GFF3Tabix
  type=CanvasFeatures

  [tracks.alignments]
  urlTemplate=Organism_A-sorted.bam
  storeClass=JBrowse/Store/SeqFeature/BAM
  type=Alignments2

.. _Apollo-portal: https://apollo-portal.genome.edu.au/
.. _us: apollo-support@genome.edu.au
.. _CP: https://currentprotocols.onlinelibrary.wiley.com/doi/10.1002/0471250953.bi0411s48
