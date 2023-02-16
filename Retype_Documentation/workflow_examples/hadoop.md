---
order: 90
label: Hadoop
icon: dot-fill
visibility: hidden
---

Hadoop is a scalable, distributed computing solution provided by Apache. Similar to queuing systems, Hadoop allows for distributed processing of large data sets.

## Workflow

### Installing Hadoop Manually to Shared Filesystem

!!!
The flight environment will need to be activated before the environments can be created so be sure to run `flight start` or [setup your environment to automatically activate the flight environment](/flight_environment_usage/flight_overview/flight_system/#activating-the-flight-system).
!!!

- Install dependencies for Hadoop (press 'y' to confirm the installation when prompted):
```bash
[flight@chead1 (mycluster1) ~]$ sudo yum install java-1.8.0-openjdk.x86_64 java-1.8.0-openjdk-devel.x86_64
```
- Download Hadoop v3.2.1:
```bash
[flight@chead1 (mycluster1) ~]$ wget -O /tmp/hadoop.tgz https://archive.apache.org/dist/hadoop/common/hadoop-3.2.1/hadoop-3.2.1.tar.gz
```
- Decompress the Hadoop installation to shared storage:
```bash
[flight@chead1 (mycluster1) ~]$ cd /opt/apps
[flight@chead1 (mycluster1) ~]$ tar xzf /tmp/hadoop.tgz
```
- Edit line 54 in `/opt/apps/hadoop-3.2.1/etc/hadoop/hadoop-env.sh` to point to the Java installation as follows:
```bash
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.242.b08-0.el7_7.x86_64/jre
```
### Downloading the Hadoop Job

These steps help setup the Hadoop environment and download a spreadsheet of data which will Hadoop will sort into sales units per region.

- Download and source Hadoop environment variables:
```bash
[flight@chead1 (mycluster1) ~]$ wget https://tinyurl.com/hadoopenv
[flight@chead1 (mycluster1) ~]$ source hadoopenv
```
- Create job directory:
```bash
[flight@chead1 (mycluster1) ~]$ mkdir MapReduceTutorial
[flight@chead1 (mycluster1) ~]$ chmod 777 MapReduceTutorial
```
- Download job data:
```bash
[flight@chead1 (mycluster1) ~]$ cd MapReduceTutorial
[flight@chead1 (mycluster1) MapReduceTutorial]$ wget -O hdfiles.zip https://tinyurl.com/hdinput1
[flight@chead1 (mycluster1) MapReduceTutorial]$ unzip -j hdfiles.zip
```
- Check that job data files are present:
```bash
[flight@chead1 (mycluster1) MapReduceTutorial]$ ls
desktop.ini  hdfiles.zip  SalesCountryDriver.java  SalesCountryReducer.java  SalesJan2009.csv  SalesMapper.java
```
### Preparing the Hadoop Job

- Compile java for job:
```bash
[flight@chead1 (mycluster1) MapReduceTutorial]$ javac -d . SalesMapper.java SalesCountryReducer.java SalesCountryDriver.java
```
- Create a manifest file:
```bash
[flight@chead1 (mycluster1) MapReduceTutorial]$ echo "Main-Class: SalesCountry.SalesCountryDriver" >> Manifest.txt
```
- Compile the final java file for job:
```bash
[flight@chead1 (mycluster1) MapReduceTutorial]$ jar cfm ProductSalePerCountry.jar Manifest.txt SalesCountry/*.class
```
### Starting the Hadoop Environment

- Start the Hadoop distributed file system service:
```bash
[flight@chead1 (mycluster1) MapReduceTutorial]$ $HADOOP_HOME/sbin/start-dfs.sh
```
- Start the resource manager, node manager and app manager service:
```bash
[flight@chead1 (mycluster1) MapReduceTutorial]$ $HADOOP_HOME/sbin/start-yarn.sh
```
- Create directory for processing data and copy sales results in:
```bash
[flight@chead1 (mycluster1) MapReduceTutorial]$ mkdir ~/inputMapReduce
[flight@chead1 (mycluster1) MapReduceTutorial]$ cp SalesJan2009.csv ~/inputMapReduce/
```
- Load the data into the distributed file system:
```bash
[flight@chead1 (mycluster1) MapReduceTutorial]$ $HADOOP_HOME/bin/hdfs dfs -ls ~/inputMapReduce
```
### Running the Hadoop Job

- Execute the MapReduce job:
```bash
[flight@chead1 (mycluster1) MapReduceTutorial]$ $HADOOP_HOME/bin/hadoop jar ProductSalePerCountry.jar ~/inputMapReduce ~/mapreduce_output_sales
```

- View the job results:
```bash
[flight@chead1 (mycluster1) MapReduceTutorial]$ $HADOOP_HOME/bin/hdfs dfs -cat ~/mapreduce_output_sales/part-00000 | more
```
