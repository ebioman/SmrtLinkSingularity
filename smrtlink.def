Bootstrap: docker
From: centos:latest
IncludeCmd:yes

%labels
maintained by Emanuel Schmid @ VITAL-IT
Version v1.0

%help
This is the current PacBio collection of tools as in smrtlink version V5.1.0 from
[I am link](https://www.pacb.com/support/software-downloads/).
In CentOS instead of Ubuntu to please admins

the standard tools should be available, not the graphical interface though

%environment
    SHELL=/bin/bash
        
%post
# default mount points
mkdir -p /scratch/cluster/monthly /scratch/local /scratch/cluster/weekly

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
        dirname
    


echo "download and extract smrtlink"
wget -c https://downloads.pacbcloud.com/public/software/installers/smrtlink_5.1.0.26412.zip --no-check-certificate
unzip -u -P 9rVkq3HT smrtlink_5.1.0.26412.zip

echo "add new user if not existant"
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

#less ideal here, better at the end as we need to download otherwise each time in testing phase
rm -rf smrtlink_5.1.0.26412.zip

echo "now switch to smrt-user and start installation"

su $SMRT_USER
SMRT_ROOT="/opt/pacbio/smrtlink"
echo $SMRT_ROOT

if [ -d $SMRT_ROOT ] 
then 
        rm -rf $SMRT_ROOT
        ./smrtlink_5.1.0.26412.run smrtlink --rootdir $SMRT_ROOT --smrttools-only       
else
        ./smrtlink_5.1.0.26412.run smrtlink --rootdir $SMRT_ROOT --smrttools-only       
fi

echo "cleaning up"
#not working yet, need to figure out how I return sudo again - without password...
#su
#rm smrtlink_5.1.0.26412.*

%environment
export PATH=/opt/pacbio/smrtlink/smrtcmds/bin/:$PATH
