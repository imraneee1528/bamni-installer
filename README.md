# Bahmni Install 0.93 

yum install -y https://kojipkgs.fedoraproject.org//packages/zlib/1.2.11/19.fc30/x86_64/zlib-1.2.11-19.fc30.x86_64.rpm

yum install -y epel-release

yum install -y python-pip

pip install pip==19.1

pip install --upgrade pip

pip install babel==v1.0 python-stdnum urllib3==1.21.1 idna==2.5 chardet==3.0.2 certifi==2017.4.17 qrcode pyserial pypdf python-chart psycogreen passlib ofxparse requests
 
# Install the bahmni command line program (Choose the version you want)

yum install -y https://repo.mybahmni.org/releases/bahmni-installer-0.93-219.noarch.rpm
 
# Note, before running the below command check whether the /etc/bahmni-installer/setup.yml already exists or not.

curl -L https://tinyurl.com/yyoj98df >> /etc/bahmni-installer/setup.yml
 
# Edit the setup.yml file and add the Bahmni Repo URL

nano /etc/bahmni-installer/setup.yml

bahmni_repo_url: https://repo.mybahmni.org/releases/

# clone git 

git clone https://github.com/imraneee1528/bamni-installer.git

cd bamni-installer

sudo rm -r /opt/bahmni-installer

sudo mv bahmni-installer /opt/cat << EOF > /etc/yum.repos.d/pgdg-96.repo

# Add repo postgresql

[pgdg90]

name=PostgreSQL 9.6 RPMs for RHEL/CentOS 7

baseurl=https://yum-archive.postgresql.org/9.6/redhat/rhel-7-x86_64

enabled=1

gpgcheck=0

gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-PGDG

EOF

# You can also configure custom inventory file instead of local.

echo "export BAHMNI_INVENTORY=local" >> ~/.bashrc

source ~/.bashrc
 
# Now fire the installer. If you have exported the variable as above you can ignore the "-i local" option. 

bahmni -i local --skip bahmni-reports install 
 
  
# Verify installed components using the command:

yum list installed | grep bahmni

