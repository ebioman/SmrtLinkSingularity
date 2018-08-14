# PacBio SmrtLink Image

This is a singularity definition file which permits to package the current PacBio smrtlink tools (smrtlink_5.1.0.26412) + the isoseq3.
The current final image is ~2.2 Gb large and is **not fully tested**.

Update: now the legacy version v2.3 is added as well - not including the patches yet though


## How to

 - install singularity on your machine (I tested only on Fedora myself)
 - make sure you have sudo rights
 - proceed with the build (an example)

        sudo singularity build --sandbox Directory Image.def
 
 - convert into an image

        sudo singularity build MyImage.img Directory

 - execute an app

        singularity exec --bind $PWD MyImage.img blasr input.bam reference.fasta
        
 In theory, the ``--bind`` should not be necessary to mount the current folder and data passed to the Image directly.
 This is working on my Fedora machine but **not** on some other CentOS7 machines.
