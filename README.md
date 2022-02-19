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
$ wget --continue --no-check-certificate -O jdk-8-linux-x64.tar.gz --header Cookie: oraclelicense=a http://download.oracle.com/otn-pub/java/jdk/8-b132/jdk-8-linux-x64.tar.gz <br />
$ tar xzf jdk-8-linux-x64.tar.gz <br />
$ mv jdk-8/ jdk  <br />
$ java -version 
$ cd ~
$ vi .bash_profile
<br />
Java JDK 1.8 
export JAVA_HOME=/opt/jdk <br />
export JRE_HOME=/opt/jdk/jre <br />
export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin <br />
<br />
$ source .bash_profile
<br />
print java version and checks if returns correctly

##### Generating SSH





  
  
 
 




