####################################
Upload Reference Genome to WebApollo
####################################

Reference genome can be made available on web apollo with two options.

1. contact Biocommons user support for WebApollo credential.
2. upload reference genome via Jbrowse followed the instructions below.


Upload Reference genome using Jbrowse. Please follow the instructions below.

1. prepare your reference genome file (e.g FASTA, GFF3 and 2bit)
2. obtain an account from BioCommons team
3. Go to WebApollo 
4. logon to web apollo using your credential 
5. following the data_loading_ tutorial to upload your reference genome.

.. _data_loading: https://genomearchitect.readthedocs.io/en/latest/Data_loading.html

#######
Example
#######
Users with Admin permission is permitted to create new genomes and upload tracks using the upload features provided by WebApollo.

Upload Reference Genome
***********************

1. Login with your admin credential.

.. figure:: ../_static/login.JPG

2. Click on the "Organism" tab at the top section on the right-hand side panel.

.. figure:: ../_static/Create_New_Genome.JPG

3. Click on the "Upload New Organism" at the bottom section of the right-hand side panel.

.. figure:: ../_static/Create_New_Genome2.JPG

4. Upload your reference genome (FASTA FORMAT) using the pop up windows
     |  **Name**       : Brassica_Rapa
     |  **DNA**        : Select the fasta file of your reference genome from local terminal
     |  **Search DB**  : Select your 2bit blat file if available
     |  **Genes**      : Brassica
     |  **Species**    : Rapa
     |  **Non-default Translation Table**  : optional

.. figure:: ../_static/select_upload_file.JPG

5. **Result**
     | The uploaded reference genome (e.g. Brassica Rapa) is now available on the right-hand side panel.

.. figure:: ../_static/genome_result.JPG

Upload Genome Annotation File
*****************************

1. Click on "Tracks" tab at the top section on the right-hand side panel and Click on on "+ New Track" button under the tab menu.

.. figure:: ../_static/add_tracks.JPG

2. Select the track type to upload (e.g. GFF3)

.. figure:: ../_static/track_type

3. Provide the information for the following fields:
     | **Track Name**    : v2 [Note: numeric format followed by dot is not recommended (e.g. 1.0)]
     | **Top Type (Remove for single-level features)** : gene (e.g. feature in the third column of GFF3)
     | **Category** : optional

.. figure:: ../_static/Select_track_type.JPG

4. **Result**
     | The uploaded genome annotation track is available on the right-hand side panel.

.. figure:: ../_static/Upload_Gff3.JPG
