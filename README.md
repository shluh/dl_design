# DL Design
ppgc@ufrgs repo
msc student: shirlei carmo

## DL On-premisses
### Stack
Environment: On-prem. Possible values {Cloud; OnPrem; MultiCloud; Hybrid} <br />
Storge: HDFS <br />
Compute: Spark (Standalone Cluster Manager) <br />
Data Management: Not applicable <br />
Advanced Analytcs Enterprise Reporting Applications: Not applicable

### Software Installation
Software: Virtural Box  <br />
SO: CentOS (minimal iso http://ftp.unicamp.br/pub/centos/7/isos/x86_64/CentOS-7-x86_64-Minimal-2009.iso) <br />
3 Virtual Machines: 1 Namenode and 3 Datanodes <br />

#### Settings <br />
  Network > Adapter > Bridged Adapter (VM setup step)<br />
  NetWork & Hostname > Enable network interface (SO installation step) ; Update 'host name' option. ie: {hdpmaster} <br />

update pkgs <br />
$ yum update <br /><br />
 
##### SSH
[remote_machine] Collect VMS ip > $ ip addr show <br />
[remote_machine] Check if it is possible to access via ssh, should return 'active ( running)' > $ service sshd status <br />
[local_machine ] Access remote machines via SSH >  $ ssh user@ip<br />
[master_node   ] Add worker machine's IP in local host file. ie: {ip hostname} > $ vi /etc/hosts <br />
  ** repeat this flow on data nodes <br />
    
##### JDK8
[install on all machines]<br />
$ cd /opt/ <br />
$ wget --no-cookies --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" https://javadl.oracle.com/webapps/download/GetFile/1.8.0_301-b09/d3c52aa6bfa54d3ca74e617f18309292/linux-i586/jdk-8u301-linux-x64.tar.gz <br />

unzip and rename to <jdk>
<br />
ADD in .bash_profile

#Java JDK 1.8 
export JAVA_HOME=/opt/jdk <br />
export JRE_HOME=/opt/jdk/jre <br />
export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin <br />
<br />
$ source .bash_profile
<br />
print java version and checks if returns correctly

##### Generating SSH

Create haddop user
  
useradd -m hadoop <br />
passwd hadoop<br />

SSH setup<br />
vi /etc/ssh/sshd_config<br />
    
uncomment lines bellow<br />
Port 22<br />
#AddressFamily any<br />
ListenAddress 0.0.0.0<br />
ListenAddress ::<br />
PubkeyAuthentication yes<br />
  
$systemctl restart sshd.service<br /><br />

Create SSH security key (only on node master) <br />

$ su hadoop<br />
$ cd ~<br />
$ ssh-keygen<br /><br />

Copy the key<br />
$ ssh-copy-id -i ~/.ssh/hdp-key.pub hadoop@hdpdatanode1<br />
$ ssh-copy-id -i ~/.ssh/hdp-key.pub hadoop@hdpdatanode2<br />
$ ssh-copy-id -i ~/.ssh/hdp-key.pub hadoop@hdpmaster<br />
  
##### Hadoop setup 3.x
$ cd /opt<br />
$ wget https://dlcdn.apache.org/hadoop/common/hadoop-3.3.1/hadoop-3.3.1.tar.gz<br />
$ tar -xvf hadoop-3.3.1.tar.gz<br />
$ mv hadoop-3.3.1.tar.gz hadoop<br />
$ chown -R hadoop:hadoop hadoop/<br />
 
SET env vars at .bash_profile<br />
# Java JDK 1.8<br />
export JAVA_HOME=/opt/jdk<br />
export JRE_HOME=/opt/jdk/jre<br />
export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin<br /><br />

# Hadoop<br />
export HADOOP_HOME=/opt/hadoop<br />
export PATH=$PATH:$HADOOP_HOME/bin<br />

  
  
 
 




