# Hadoop word count, sort, search - Python

This is the final project regarding the EEN474 (Cloud Computing) course taken in FA25 at NDU - Louaize.<br/>
Applied in this final project are concepts of [INSERT MAIN IDEA WHEN DONE].<br/><br/>
**Main Features:**<br/>
🔄️ Word Count.<br/>
🔠 Word Sort.<br/>
🔍 Word Search.<br/>


## Before Proceeding:
This program relies on the Hadoop framework which is built on Java, ran through Python.<br/>
This section is dedicated to guide users through the environment setup required in order to successfully launch Hadoop and its pre-requisistes.<br/>

▫️**Tech Used:** Python 3.8+<br/>
▫️**Dependencies:** WinRaR, Java, Hadoop (single-node).<br/>‎ ‎ ‎ ‎ <br/>

### Installing Java
Head on over to the Oracle [website](https://www.oracle.com/java/technologies/downloads/), and install the latest Java 8 for Windows 64x. After downloading, create a new folder "Java" in the root C:\ directory then run the installer.<br/>
Jump into [C:\Program Files\Java] & cut the newly created "jdk-1.8" folder, and paste it back into the "Java" folder created beforehand. Java should now be ready to use on the host machine by opening CMD and typing "java". <br/><br/>
⚠️ **If "java" command returns as an unrecognized command:**<br/>
▫️Open "Environment Variables" on the host machine.<br/>
▫️Create a new path, named "JAVA_HOME", and linked to "C:\Java\jdk-1.8\bin".<br/>
▫️In the same window, edit the "Path" System Variable. Inside, create a new variable "C:\Java\jdk-1.8\bin". <br/>
▫️Apply everything and close out.<br/>

Java should now be successfully installed on the host machine. Check the installed Java version by typing in CMD "java -version".<br/>‎ ‎ ‎ ‎ ‎ <br/>

### Installing Hadoop
Head on over to the Apache Hadoop [website](https://www.apache.org/dyn/closer.cgi/hadoop/common/hadoop-3.4.1/hadoop-3.4.1.tar.gz), press on "Download" and choose a stable version. Once satisfied, click on the "binary" link, then on the download link at the top of the page.<br/>
Once downloaded, extract the zip file containing the Hadoop folder, then move that folder over to root C:\ and rename it "hadoop" for convenience. Inside, head to "C:\hadoop\etc\hadoop" and right click edit the "hadoop-env" file.<br/>
Set the default Java path to our newly created Java folder. The edited line of code should look like: [ set JAVA_HOME = C:\Java\jdk-1.8 ]<br/><br/>
⚠️ **Creating Environment Variables here is mandatory:**<br/>
▫️Open "Environment Variables" on the host machine.<br/>
▫️Create a new path, named "HADOOP_HOME", and linked to "C:\hadoop\bin".<br/>
▫️In the same window, edit the "Path" System Variable. Inside, create TWO new variables "C:\hadoop\bin" & "C:\hadoop\sbin". <br/>
▫️Apply everything and close out.<br/>

⭕ If when running "hadoop version", it echoes [ ERROR: could not find or load main class El ], you might have spaces in your account username, which are forbidden characters. To fix this:<br/>
▫️Head back to "C:\hadoop\etc\hadoop" and right click edit the "hadoop-env" file.<br/>
▫️Scroll until the last line is reached.<br/>
▫️Replace %USERNAME% with your account username with NO SPACES.<br/><br/>

Hadoop should now be successfully installed on the host machine. Check the installed Hadoop version by typing in CMD "hadoop" then "hadoop version".<br/><br/>‎ ‎ ‎ ‎ ‎ <br/>







