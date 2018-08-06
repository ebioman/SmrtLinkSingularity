# PacBio SmrtLink Image

This is a singularity definition file which permits to package the current PacBio smrtlink tools (smrtlink_5.1.0.26412).
The current final image is ~3.4 Gb large and is **not fully tested**.
E.g. sometimes building singularity images would crash my personal laptop - no idea why...


## How to

 - install singularity on your machine (I tested only on Fedora myself)
 - make sure you have sudo rights
 - proceed with the build (an example)

        sudo singularity build --sandbox Directory Image.def
 
 - convert into an image

        sudo singularity build MyImage.img Directory

 - execute an app

        singularity exec MyImage.img blasr -v
