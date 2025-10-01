# Hadoop word count, sort, search - Python

This is the final project regarding the EEN474 (Cloud Computing) course taken in FA25 at NDU - Louaize.<br/>
Applied in this final project are concepts of cloud computing using Hadoop, understanding proper namenode and datanode usage with HDFS, and running python scripts for word count, sort, and search on a Hadoop Cluster.<br/><br/>
**Main Features:**<br/>
🔄️ Word Count.<br/>
🔠 Word Sort.<br/>
🔍 Word Search.<br/>


## Before Proceeding:
This program relies on the Hadoop framework which is built on Java, ran through Python.<br/>
This section is dedicated to guide users through the environment setup required in order to successfully launch Hadoop and its pre-requisistes.<br/>

▫️**Tech Used:** Python 3.8+<br/>
▫️**Dependencies:** WinRaR, Java, Hadoop (single-node).<br/>‎ ‎ ‎ ‎ <br/>

### ⚪ Installing Java
Head on over to the Oracle [website](https://www.oracle.com/java/technologies/downloads/), and install the latest Java 8 for Windows 64x. After downloading, create a new folder "Java" in the root C:\ directory then run the installer.<br/>
Jump into [C:\Program Files\Java] & cut the newly created "jdk-1.8" folder, and paste it back into the "Java" folder created beforehand. Java should now be ready to use on the host machine by opening CMD and typing "java". <br/><br/>
⚠️ **If "java" command returns as an unrecognized command:**<br/>
▫️Open "Environment Variables" on the host machine.<br/>
▫️Create a new path, named "JAVA_HOME", and linked to "C:\Java\jdk-1.8\bin".<br/>
▫️In the same window, edit the "Path" System Variable. Inside, create a new variable "C:\Java\jdk-1.8\bin". <br/>
▫️Apply everything and close out.<br/>

Java should now be successfully installed on the host machine. Check the installed Java version by typing in CMD "java -version".<br/>‎ ‎ ‎ ‎ ‎ <br/>

### ⚪ Installing Hadoop
Head on over to the Apache Hadoop [website](https://www.apache.org/dyn/closer.cgi/hadoop/common/hadoop-3.4.1/hadoop-3.4.1.tar.gz), press on "Download" and choose a stable version. Once satisfied, click on the "binary" link, then on the download link at the top of the page.<br/>
Once downloaded, extract the zip file containing the Hadoop folder, then move that folder over to root C:\ and rename it "hadoop" for convenience. Inside, head to "C:\hadoop\etc\hadoop" and right click edit the "hadoop-env" file.<br/>
Set the default Java path to our newly created Java folder. The edited line of code should look like: [ set JAVA_HOME = C:\Java\jdk-1.8 ]<br/><br/>
⚠️ **Creating Environment Variables here is mandatory:**<br/>
▫️Open "Environment Variables" on the host machine.<br/>
▫️Create a new path, named "HADOOP_HOME", and linked to "C:\hadoop\bin".<br/>
▫️In the same window, edit the "Path" System Variable. Inside, create TWO new variables "C:\hadoop\bin" & "C:\hadoop\sbin". <br/>
▫️Apply everything and close out.<br/>

Check the installed Hadoop version by typing in CMD "hadoop" then "hadoop version".<br/>

⭕ If when running "hadoop version", it echoes [ ERROR: could not find or load main class El ], you might have spaces in your account username, which are forbidden characters. To fix this:<br/>
▫️Head back to "C:\hadoop\etc\hadoop" and right click edit the "hadoop-env" file.<br/>
▫️Scroll until the last line is reached.<br/>
▫️Replace %USERNAME% with your account username with NO SPACES.<br/>

Hadoop should now be successfully installed on the host machine. Check the installed Hadoop version by typing in CMD "hadoop" then "hadoop version".<br/>‎ ‎ ‎ ‎ ‎ <br/>

### ⚪ Configuring Hadoop
Head back to "C:\hadoop\etc\hadoop" and open the "core-site" XML file to edit with notepad. In the last "configuration" section, edit it to include HDFS as shown below:<br/>
```html
<configuration>
  
<property>
<name>fs.defaultFS</name>
<value>hdfs://localhost:9000</value>
</property>

</configuration>
```
<br/>Go back to "C:\hadoop" and create a new "data" folder. Inside, create 2 more folders named "namenode" & "datanode". The paths of these respective folders will be used in the next step.<br/>
Head back to "C:\hadoop\etc\hadoop" and open the "httpfs-site" XML file and the "hdfs-site" XML file to edit with notepad. Just like before in the last "configuration" section, edit it as such in both files:<br/>
```html
<configuration>

<property>
<name>dfs.replication</name>
<value>1</value>
</property>

<property>
<name>dfs.namenode.name.dir</name>
<value>C:\hadoop\data\namenode</value>
</property>

<property>
<name>dfs.datanode.data.dir</name>
<value>C:\hadoop\data\datanode</value>
</property>

</configuration>
```
<br/>Head back to "C:\hadoop\etc\hadoop" and open the "mapred-site" XML file to edit with notepad. Just like before in the last "configuration" section, edit it as such:<br/>
```html
<configuration>

<property>
<name>mapreduce.framework.name</name>
<value>yarn</value>
</property>

</configuration>
```
<br/>Finally, head back to "C:\hadoop\etc\hadoop" and open the "yarn-site" XML file to edit with notepad. Just like before in the last "configuration" section, edit it as such:<br/>
```html
<configuration>

<property>
<name>yarn.nodemanager.aux-services</name>
<value>mapreduce_shuffle</value>
</property>

<property>
<name>yarn.nodemanager.auxservices.mapreduce.shuffle.class</name>
<value>org.apache.hadoop.mapred.ShuffleHandler</value>
</property>

</configuration>
```

<br/> **⭕IMPORTANT:** Hadoop is not configured to run on Windows by default. As such, head to your Hadoop directory "C:\hadoop" and delete the "bin" folder. Next, download the ZIP file uploaded to this GitHub repository containing the new bin folder, and place it inside "C:\hadoop".<br/>
Open the new bin folder and run "winutils.exe". This will give an error based on what .dll files might be missing from the host machine. If any is missing, they must be downloaded from the Internet and placed into System32 "C:\Windows\System32" folder to successfully run Hadoop. Keep running the progtam until no other errors show.<br/><br/>

## Starting up Hadoop
**Run CMD as Administrator:**
<br/>
💠 "hdfs namenode -format" to format the Hadoop namenode. [ONE TIME RUN]<br/>
💠 "start-dfs.cmd" to start the namenode and datanode.<br/>
💠 "start-yarn.cmd" to start Hadoop.<br/>

**To visually check Cluster: Open Browser**
<br/>
💠 "localhost:9870" to check namenode.<br/>
💠 "localhost:9864" to check datanode.<br/>
💠 "localhost:8088" to check Hadoop ressource manager.<br/><br/>

## Uploading to HDFS:
### ⚪ Data Files Upload<br/>
1️⃣ Create a folder on your machine containing the data files to upload. Here, take [C:\hadoop\local_input] as an example path.<br/>
2️⃣ Run in CMD: "hdfs dfs -mkdir /input" This will create a folder (directory) inside the HDFS to store the files.<br/>
3️⃣ Run in CMD: "hdfs dfs -put C:/hadoop/local_input/DataFileName.txt /input" This will copy the file from the local machine to the newly created directory in the HDFS.<br/>

**⭕HELPFUL NOTE:** To check directories in HDFS, either head to "localhost:9870" and in the "Utilities" tab -> Browse the File system, or run in CMD "hdfs dfs -ls /input" which will list all files in the /input directory.<br/><br/>

### ⚪ Python Scripts Upload
Since we are Streaming to Hadoop with Python, the code files must not be uploaded to HDFS, they stay on the local machine. The code will be available as a ZIP in this repository to make everyone's life easier :)<br/>
⭕ Start Hadoop as usual, the cd into the folder containing the .py files, and run the jobs from there.<br/><br/>

1️⃣ **Word Count Job:** <br/>
```
hadoop jar %HADOOP_HOME%\share\hadoop\tools\lib\hadoop-streaming-*.jar ^
  -input /input ^
  -output /wc_out ^
  -mapper wc_mapper.py ^
  -reducer wc_reducer.py ^
  -file wc_mapper.py ^
  -file wc_reducer.py
```
📤 **To Check Output:** <br/>
```
hdfs dfs -cat /wc_out/part-00000 | more
```
🔎 **Explanation:** <br/>
hadoop jar ... hadoop-streaming-*.jar → runs the Hadoop Streaming JAR (lets you use Python instead of Java for MapReduce).<br/>
-input /input → the directory in HDFS containing your text files.<br/>
-output /wc_out → where Hadoop will store the results (must NOT exist beforehand).<br/>
-mapper wc_mapper.py → your Python script that tokenizes words and outputs <word, 1>.<br/>
-reducer wc_reducer.py → your reducer that sums counts per word.<br/>
-file wc_mapper.py -file wc_reducer.py → ship these Python files to the cluster.<br/><br/>


<br/> 2️⃣ **Sort By Count Job:** <br/>
```
hadoop jar %HADOOP_HOME%\share\hadoop\tools\lib\hadoop-streaming-*.jar ^
  -input /wc_out ^
  -output /sort_count_out ^
  -mapper sort_by_count_mapper.py ^
  -reducer sort_by_count_reducer.py ^
  -file sort_by_count_mapper.py ^
  -file sort_by_count_reducer.py

```
📤 **To Check Output:** <br/>
```
hdfs dfs -cat /sort_count_out/part-00000 | more
```

<br/><br/> 3️⃣ **Sort By Word Job:** <br/>
```
hadoop jar %HADOOP_HOME%\share\hadoop\tools\lib\hadoop-streaming-*.jar ^
  -input /wc_out ^
  -output /sort_word_out ^
  -mapper sort_by_word_mapper.py ^
  -reducer sort_by_word_reducer.py ^
  -file sort_by_word_mapper.py ^
  -file sort_by_word_reducer.py
```
📤 **To Check Output:** <br/>
```
hdfs dfs -cat /sort_word_out/part-00000 | more
```

<br/><br/> 4️⃣ **Word Search: "Hadoop"** <br/>
```
hadoop jar %HADOOP_HOME%\share\hadoop\tools\lib\hadoop-streaming-*.jar ^
  -input /input ^
  -output /search_out ^
  -mapper "search_mapper.py hadoop" ^
  -reducer search_reducer.py ^
  -file search_mapper.py ^
  -file search_reducer.py
```
📤 **To Check Output:** <br/>
```
hdfs dfs -cat /search_out/part-00000 | more
```




