# first


Installation des paquets :

Lancez un terminal et entrez les commandes suivantes :

yum install gcc* compat-gcc*
yum install glibc* compat-glibc*
yum install compat-db*
yum install libxp* openmotif
yum install cpp* libstdc++* compat-libstdc++*
yum install libaio*
yum install binutils ksh sysstat elfutils* setarch
Fichier /etc/sysctl.conf :

Editez le fichier et ajoutez les lignes suivantes à la fin :

fs.aio-max-nr = 1048576
fs.file-max = 6815744
kernel.shmall = 2097152
kernel.shmmax = 2123476992
kernel.shmmni = 4096
kernel.sem = 250 32000 100 128
net.ipv4.ip_local_port_range = 9000 65500
net.core.rmem_default = 262144
net.core.rmem_max = 4194304
net.core.wmem_default = 262144
net.core.wmem_max = 1048586
Après modification, il faut recharger la nouvelle configuration à l'aide de la commande sysctl -p.

Fichier /etc/security/limits.conf :

Editez le fichier et ajoutez les lignes suivantes à la fin :

oracle  soft    nproc   2048
oracle  hard    nproc   65536
oracle  soft    nofile  1024
oracle  hard    nofile  65536
oracle  soft    stack   10240
Fichier /etc/pam.d/login :

Editez le fichier et ajoutez les lignes suivantes à la fin :

session    required     /lib64/security/pam_limits.so
Attention : Si vous utilisez un serveur 32 bits, il faut remplacer "lib64" par "lib".

Désactiver SELinux :

Editez le fichier et passez la valeur SELINUX à disabled :

SELINUX=disabled
Utilisateurs, groupes et droits :

Créez les groupes suivants :

groupadd oinstall
groupadd dba
groupadd oper
Créez le compte utilisateur oracle :

useradd -g oinstall -G dba oracle
passwd oracle
Créez le dossier /oracle/product/11.2/db_1 :

mkdir -p /oracle/product/11.2/db_1
chown -R oracle:oinstall /oracle
Editez le fichier /home/oracle/.bash_profile et ajoutez les lignes suivantes à la fin :

TMP=/tmp; export TMP
TMPDIR=$TMP; export TMPDIR
ORACLE_BASE=/oracle; export ORACLE_BASE
ORACLE_HOME=$ORACLE_BASE/product/11.2/db_1; export ORACLE_HOME
ORACLE_SID=le nom de votre base de données; export ORACLE_SID
ORACLE_TERM=xterm; export ORACLE_TERM
PATH=$ORACLE_HOME/bin:$PATH; export PATH
LD_LIBRARY_PATH=$ORACLE_HOME/lib:/lib:/usr/lib; export LD_LIBRARY_PATH
CLASSPATH=$ORACLE_HOME/JRE:$ORACLE_HOME/jlib:$ORACLE_HOME/rdbms/jlib; export CLASSPATH
ulimit -u 16384 -n 65536
Installation d'Oracle :

Redémarrez le serveur et connectez-vous avec le compte oracle.

Télécharger Oracle :

Vous pouvez télécharger Oracle : ici.

Installation & mise en route :
