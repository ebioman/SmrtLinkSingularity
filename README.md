# PacBio SmrtLink Image

This is a singularity definition file which permits to package the current PacBio smrtlink tools (smrtlink_5.1.0.26412) + the isoseq3.
The current final image is ~2.2 Gb large and is **not fully tested**.

## Specfile

The specfile is designed to work optimal in sandbox mode and therefore contains a few checks for users and directories which are not necessary for a normal build mode but will result in issues if a sandbox mode is used.

## How to

 - install singularity on your machine (I tested only on Fedora myself)
 - make sure you have sudo rights
 - proceed with the build (an example)

        sudo singularity build --sandbox Directory Image.def
 
 - convert into an image

        sudo singularity build MyImage.img Directory

 - execute an app

        singularity exec --bind $PWD MyImage.img blasr input.bam reference.fasta
        
