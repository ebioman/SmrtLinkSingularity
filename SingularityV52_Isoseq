Bootstrap: docker
From: centos:latest

%labels
maintained by Emanuel Schmid @ VITAL-IT
Version v5.1.0.26412

%help
This is the current PacBio collection of tools as in smrtlink version V5.1.0 from
[I am link](https://www.pacb.com/support/software-downloads/).
It furthermore includes the

 - isoseq3

In CentOS instead of Ubuntu to please admins

the standard tools should be available, not the graphical interface though

%environment
    SHELL=/bin/bash
        
%post

# install software
yum update -y -q && yum install -y -q \
        build-essential \
        gcc-multilib \
        libboost-all-dev \
        libhdf5-serial-dev \
        zlib1g-dev \
        pkg-config \
        wget \
        rsync \
        unzip \
        which \
        bzip2 \
        dirname
    


echo "add new user if not existent"
        
SMRT_USER=smrtanalysis
if ! grep -c "smrtanalysis:" /etc/passwd
then
        useradd  -g users -d /home/$SMRT_USER -s /bin/bash -p PacBio $SMRT_USER
else
        echo    "user already exists"
fi

echo "generate a new PacBio root directory and make smrtuser owner"

SMRT=/opt/pacbio
if [ ! -d $SMRT ]
then
        mkdir $SMRT
        chown smrtanalysis:users $SMRT
fi





echo "now switch to smrt-user"

su $SMRT_USER
SMRT_ROOT="/opt/pacbio/smrtlink"
cd $SMRT

echo "download and extract smrtlink"
wget -c https://downloads.pacbcloud.com/public/software/installers/smrtlink_5.1.0.26412.zip --no-check-certificate
unzip -u -P 9rVkq3HT smrtlink_5.1.0.26412.zip


if [ -d $SMRT_ROOT ] 
then 
        rm -rf $SMRT_ROOT
        ./smrtlink_5.1.0.26412.run smrtlink --rootdir $SMRT_ROOT --smrttools-only       
else
        ./smrtlink_5.1.0.26412.run smrtlink --rootdir $SMRT_ROOT --smrttools-only       
fi

wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O miniconda3.sh 
bash miniconda3.sh -b -p /opt/pacbio/miniconda
export PATH="/opt/pacbio/miniconda/bin/:$PATH"
conda config --add channels conda-forge
conda config --add channels defaults
conda config --add channels r
conda config --add channels bioconda
conda install -y isoseq3

echo "cleaning up"
rm smrtlink_5.1.0.26412.*


%environment
export PATH=/opt/pacbio/smrtlink/smrtcmds/bin/:$PATH
export PATH=/opt/pacbio/miniconda/bin/:$PATH

%runscript
exec /bin/bash "$@"
