# Google Cloud Shell

## overview

- google cloud platformで、cassandra環境を構築する

## FIXME

- [ ] **FIXME**  ccmがインストール後に、起動できない。sudoでインストール？

## reference

- 

## logs

### ** `gcloud version`

- list up cloud SDK components installed

```
Welcome to Cloud Shell! Type "help" to get started.
Your Cloud Platform project in this session is set to vm19a-240600.
Use “gcloud config set project [PROJECT_ID]” to change to a different project.
sakai_memoru@cloudshell:~ (vm19a-240600)$ gcloud version
Google Cloud SDK 244.0.0
alpha 2019.02.22
app-engine-go
app-engine-java 1.9.73
app-engine-php " "
app-engine-python 1.9.85
app-engine-python-extras 1.9.74
beta 2019.02.22
bq 2.0.43
cbt
cloud-build-local
cloud-datastore-emulator 2.1.0
core 2019.04.26
datalab 20190116
docker-credential-gcr
gcd-emulator v1beta3-1.0.0
gsutil 4.38
kubectl 2019.04.26
pubsub-emulator 2019.04.26
```

### ** basic operation

```bash
sakai_memoru@cloudshell:~ (vm19a-240600)$ cd ~
sakai_memoru@cloudshell:~ (vm19a-240600)$ ls
README-cloudshell.txt
sakai_memoru@cloudshell:~ (vm19a-240600)$ ls -la
total 48
    ;;
drwxr-xr-x 8 sakai_memoru sakai_memoru 4096 May 14 09:16 .
drwxr-xr-x 4 root         root         4096 May 14 09:14 ..
-rw------- 1 sakai_memoru sakai_memoru   40 May 14 09:33 .bash_history
-rw-r--r-- 1 sakai_memoru sakai_memoru  220 May 16  2017 .bash_logout
-rw-r--r-- 1 sakai_memoru sakai_memoru 3706 May 14 09:14 .bashrc
drwxr-xr-x 4 sakai_memoru sakai_memoru 4096 May 14 09:15 .cache
drwxr-xr-x 4 sakai_memoru sakai_memoru 4096 May 14 09:15 .config
drwx------ 2 sakai_memoru sakai_memoru 4096 May 14 09:14 .docker
drwxr-xr-x 5 sakai_memoru sakai_memoru 4096 May 14 09:15 .npm
-rw-r--r-- 1 sakai_memoru sakai_memoru  675 May 16  2017 .profile
lrwxrwxrwx 1 sakai_memoru sakai_memoru   38 May 14 09:14 README-cloudshell.txt -> /google/devshell/README-cloudshell.txt
drwxr-xr-x 2 sakai_memoru root         4096 May 14 09:14 .theia
drwxr-xr-x 3 sakai_memoru sakai_memoru 4096 May 14 09:14 .yarn
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ vim .bashrc                                
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ . .bashrc
                            2019
       April                  May                   June
Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa
    1  2  3  4  5  6            1  2  3  4                     1
 7  8  9 10 11 12 13   5  6  7  8  9 10 11   2  3  4  5  6  7  8
14 15 16 17 18 19 20  12 13 14 15 16 17 18   9 10 11 12 13 14 15
21 22 23 24 25 26 27  19 20 21 22 23 24 25  16 17 18 19 20 21 22
28 29 30              26 27 28 29 30 31     23 24 25 26 27 28 29
                                            30
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$
```



- display each tool of initial version 

    ```
    
    sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ python --version
    Python 2.7.13
    sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ python3 --version
    Python 3.5.3
    
    sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ java -version
    openjdk version "1.8.0_212"
    OpenJDK Runtime Environment (build 1.8.0_212-8u212-b01-1~deb9u1-b01)
    OpenJDK 64-Bit Server VM (build 25.212-b01, mixed mode)
    sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ node --version
    v10.14.2
    
    sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ mvn --version
    Apache Maven 3.6.0 (97c98ec64a1fdfee7767ce5ffb20918da4f719f3; 2018-10-25T03:41:47+09:00)
    Maven home: /opt/maven
    Java version: 1.8.0_212, vendor: Oracle Corporation, runtime: /usr/lib/jvm/java-8-openjdk-amd64/jre
    Default locale: en_US, platform encoding: UTF-8
    OS name: "linux", version: "4.14.104+", arch: "amd64", family: "unix"
    
    sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ git --version
    git version 2.11.0
    ```



### ** `gcloud alpha cloud-shell`

### ** Sample “create Cassandra db env”

#### * reference

- smart se instruction
    - https://github.com/shoshii/waseda_smartse/blob/master/doc/work_nosql_cassandra.md
- **Apache Cassandraを試してみる**
- https://qiita.com/sasayabaku/items/dfae9ef3b1582a9cc5bb
    - Cassandra Clusterを、ローカル環境で疑似的に稼働させる開発用ツール
- **YCSBの概要とCassandraへのベンチマーク**
- https://qiita.com/noralife/items/35a956f682b1aca475f6
    - YCSBは、Yahoo! Researchが開発して、OSSとして公開されているNoSQLを対象としたBench Mark Tool。負荷シナリオが定義されている。

#### * Environment

```
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ java -version
openjdk version "1.8.0_212"
OpenJDK Runtime Environment (build 1.8.0_212-8u212-b01-1~deb9u1-b01)
OpenJDK 64-Bit Server VM (build 25.212-b01, mixed mode)
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ pip --version
pip 19.1 from /usr/local/lib/python2.7/dist-packages/pip-19.1-py2.7.egg/pip (python 2.7)
```



#### * pip

```
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ sudo apt install python
Reading package lists... Done
Building dependency tree       
Reading state information... Done
python is already the newest version (2.7.13-2).
0 upgraded, 0 newly installed, 0 to remove and 42 not upgraded.
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ python --version
Python 2.7.13
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ python
Python 2.7.13 (default, Sep 26 2018, 18:42:22)
[GCC 6.3.0 20170516] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import sys
>>> for p in sys.path:
...     print(p)
...

/usr/lib/python2.7
/usr/lib/python2.7/plat-x86_64-linux-gnu
/usr/lib/python2.7/lib-tk
/usr/lib/python2.7/lib-old
/usr/lib/python2.7/lib-dynload
/home/sakai_memoru/.local/lib/python2.7/site-packages
/usr/local/lib/python2.7/dist-packages
/usr/local/lib/python2.7/dist-packages/pip-19.1-py2.7.egg
/usr/lib/python2.7/dist-packages
>>> exit()
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ vim .bashrc
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ vim .bashrc
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ . .bashrc
                            2019
       April                  May                   June
Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa
    1  2  3  4  5  6            1  2  3  4                     1
 7  8  9 10 11 12 13   5  6  7  8  9 10 11   2  3  4  5  6  7  8
14 15 16 17 18 19 20  12 13 14 15 16 17 18   9 10 11 12 13 14 15
21 22 23 24 25 26 27  19 20 21 22 23 24 25  16 17 18 19 20 21 22
28 29 30              26 27 28 29 30 31     23 24 25 26 27 28 29
                                            30
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ pip -V
pip 19.1 from /usr/local/lib/python2.7/dist-packages/pip-19.1-py2.7.egg/pip (python 2.7)
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$
```



 

#### * install cassandra

- [ ] **FIXME** cassandraそのもののinstall

#### * install CCM

- 

```
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ pip install ccm --user
DEPRECATION: Python 2.7 will reach the end of its life on January 1st, 2020. Please upgrade your Python as Python 2.7 won't be maintained after that date. A future version of pip will drop support for Python 2.7.
Collecting ccm
  Downloading https://files.pythonhosted.org/packages/fc/ab/b51afd466cc4acf2192e230ddb6fd3adb56066f05c7be1852af7bd655068/ccm-3.1.4.tar.gz (72kB)
     |████████████████████████████████| 81kB 2.7MB/s
Collecting pyYaml (from ccm)
  Downloading https://files.pythonhosted.org/packages/9f/2c/9417b5c774792634834e730932745bc09a7d36754ca00acf1ccd1ac2594d/PyYAML-5.1.tar.gz (274kB)
     |████████████████████████████████| 276kB 7.4MB/s
Requirement already satisfied: six>=1.4.1 in /usr/local/lib/python2.7/dist-packages (from ccm) (1.12.0)
Building wheels for collected packages: ccm, pyYaml
  Building wheel for ccm (setup.py) ... done
  Stored in directory: /home/sakai_memoru/.cache/pip/wheels/fd/e6/7b/4c2c9b50ba40b2c983f806dcb21a8308ec7e5c2cfb03ad92aa
  Building wheel for pyYaml (setup.py) ... done
  Stored in directory: /home/sakai_memoru/.cache/pip/wheels/ad/56/bc/1522f864feb2a358ea6f1a92b4798d69ac783a28e80567a18b
Successfully built ccm pyYaml
Installing collected packages: pyYaml, ccm
Successfully installed ccm-3.1.4 pyYaml-5.1
```



```bash
.bashrc
export PATH=$PAHT:~/.local/bin
```



```
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ ccm
Missing arguments
Usage:
  ccm <cluster_cmd> [options]
  ccm <node_name> <node_cmd> [options]

```



#### * install YCSB

```
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ mvn --version
Apache Maven 3.6.0 (97c98ec64a1fdfee7767ce5ffb20918da4f719f3; 2018-10-25T03:41:47+09:00)
Maven home: /opt/maven
Java version: 1.8.0_212, vendor: Oracle Corporation, runtime: /usr/lib/jvm/java-8-openjdk-amd64/jre
Default locale: en_US, platform encoding: UTF-8
OS name: "linux", version: "4.14.104+", arch: "amd64", family: "unix"
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ git clone https://github.com/brianfrankcooper/YCSB.git
Cloning into 'YCSB'...
remote: Enumerating objects: 18089, done.
remote: Total 18089 (delta 0), reused 0 (delta 0), pack-reused 18089
Receiving objects: 100% (18089/18089), 31.10 MiB | 9.19 MiB/s, done.
Resolving deltas: 100% (6962/6962), done.
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ cd YCSB/
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~/YCSB$ mvn clean package -DskipTests
```

```
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ ls
README-cloudshell.txt  YCSB
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ cd YCSB/
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~/YCSB$ bin/ycsb -h
usage: bin/ycsb command database [options]

Commands:
    load           Execute the load phase
    run            Execute the transaction phase
    shell          Interactive mode
:
:
:
Options:
    -P file        Specify workload file
    -cp path       Additional Java classpath entries
    -jvm-args args Additional arguments to the JVM
    -p key=value   Override workload property
    -s             Print status to stderr
    -target n      Target ops/sec (default: unthrottled)
    -threads n     Number of client threads (default: 1)

Workload Files:
    There are various predefined workloads under workloads/ directory.
    See https://github.com/brianfrankcooper/YCSB/wiki/Core-Properties
    for the list of workload properties.
positional arguments:
  {load,run,shell}      Command to run.
  {accumulo,accumulo1.6,accumulo1.7,accumulo1.8,aerospike,arangodb,arangodb3,asynchbase,azurecosmos,azuretablestorag
e,basic,basicts,cassandra-cql,cassandra2-cql,cloudspanner,couchbase,couchbase2,dynamodb,elasticsearch,elasticsearch5
,elasticsearch5-rest,foundationdb,geode,googlebigtable,googledatastore,hbase098,hbase10,hbase12,hbase14,hbase20,hype
rtable,ignite,ignite-sql,infinispan,infinispan-cs,jdbc,kudu,maprdb,maprjsondb,memcached,mongodb,mongodb-async,nosqld
b,orientdb,postgrenosql,rados,redis,rest,riak,rocksdb,s3,solr,solr6,tarantool}
                        Database to test.
optional arguments:
  -h, --help            show this help message and exit
  -cp CLASSPATH         Additional classpath entries, e.g. '-cp
                        /tmp/hbase-1.0.1.1/conf'. Will be prepended to the
                        YCSB classpath.
  -jvm-args JVM_ARGS    Additional arguments to pass to 'java', e.g. '-Xmx4g'
```



#### * ccm

- node数3で、cluster起動用のファイルを作成（cassandra version は2.0.11）

```
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ ccm create -n 3 -v 2.0.11 test
11:45:42,266 ccm INFO Downloading http://archive.apache.org/dist/cassandra/2.0.11/apache-cassandra-2.0.11-bin.tar.gz to /tmp/ccm-csAo3F.tar.gz (17.177MB)
  18010992  [100.00%]11:45:46,586 ccm INFO Extracting /tmp/ccm-csAo3F.tar.gz as version 2.0.11 ...
Current cluster is now: test
/home/sakai_memoru/.local/lib/python2.7/site-packages/ccmlib/node.py:1501: YAMLLoadWarning: calling yaml.load() without Loader=... is deprecated, as the default Loader is unsafe. Please read https://msg.pyyaml.org/load for full details.
  data = yaml.load(f)
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ ccm start
/home/sakai_memoru/.local/lib/python2.7/site-packages/ccmlib/cluster_factory.py:22: YAMLLoadWarning: calling yaml.load() without Loader=... is deprecated, as the default Loader is unsafe. Please read https://msg.pyyaml.org/load for full details.
  data = yaml.load(f)
/home/sakai_memoru/.local/lib/python2.7/site-packages/ccmlib/node.py:143: YAMLLoadWarning: calling yaml.load() without Loader=... is deprecated, as the default Loader is unsafe. Please read https://msg.pyyaml.org/load for full details.
  data = yaml.load(f)
```

- `ccm start`  and `ccm status`

```
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ ccm start
/home/sakai_memoru/.local/lib/python2.7/site-packages/ccmlib/cluster_factory.py:22: YAMLLoadWarning: calling yaml.load() without Loader=... is deprecated, as the default Loader is unsafe. Please read https://msg.pyyaml.org/load for full details.
  data = yaml.load(f)
/home/sakai_memoru/.local/lib/python2.7/site-packages/ccmlib/node.py:143: YAMLLoadWarning: calling yaml.load() without Loader=... is deprecated, as the default Loader is unsafe. Please read https://msg.pyyaml.org/load for full details.
  data = yaml.load(f)
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ ccm status
/home/sakai_memoru/.local/lib/python2.7/site-packages/ccmlib/cluster_factory.py:22: YAMLLoadWarning: calling yaml.load() without Loader=... is deprecated, as the default Loader is unsafe. Please read https://msg.pyyaml.org/load for full details.
  data = yaml.load(f)
/home/sakai_memoru/.local/lib/python2.7/site-packages/ccmlib/node.py:143: YAMLLoadWarning: calling yaml.load() without Loader=... is deprecated, as the default Loader is unsafe. Please read https://msg.pyyaml.org/load for full details.
  data = yaml.load(f)
Cluster: 'test'
---------------
node1: UP
node3: UP
node2: UP
```



```
sakai_memoru@cs-6000-devshell-vm-95c7e8ba-3e83-43c7-b583-a8ea19ff52b1:~$ ccm node1 nodetool status
/home/sakai_memoru/.local/lib/python2.7/site-packages/ccmlib/cluster_factory.py:22: YAMLLoadWarning: calling yaml.load() without Loader=... is deprecated, as the default Loader is unsafe. Please read https://msg.pyyaml.org/load for full details.
  data = yaml.load(f)
/home/sakai_memoru/.local/lib/python2.7/site-packages/ccmlib/node.py:143: YAMLLoadWarning: calling yaml.load() without Loader=... is deprecated, as the default Loader is unsafe. Please read https://msg.pyyaml.org/load for full details.
  data = yaml.load(f)

Datacenter: datacenter1
=======================
Status=Up/Down
|/ State=Normal/Leaving/Joining/Moving
--  Address    Load       Tokens  Owns (effective)  Host ID                               Rack
UN  127.0.0.1  36.25 KB   1       66.7%             7ffe41e7-fbf6-4a83-8522-9bf42c8b45a5  rack1
UN  127.0.0.2  36.25 KB   1       66.7%             15bc01a5-686e-475d-8feb-ea5c96445244  rack1
UN  127.0.0.3  36.25 KB   1       66.7%             f09ad29c-fbc9-443c-88ea-c6e3fd98e1a1  rack1
```





### ** update

![img](https://gyazo.com/c77f0bd90fce50d6f0dc49e8dc185d51.png)
<https://gyazo.com/c77f0bd90fce50d6f0dc49e8dc185d51>