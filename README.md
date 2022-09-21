# Belajar Apache Storm
> disusun oleh Hardiyanto

<img src="https://github.com/dwiHard/belajar-apache-storm/blob/main/apache_storm_logo_icon_168601.png" height="200px">

## Version
* Apache Storm v.2.4.0
* Java v.11

## Installation
1. Setting PATH
ikuti command berikut
```
vim ~/.bashrc
```
lalu tambahkan
```
export STROM_HOME=/home/hard/Documents/apache strom/apache-storm-2.4.0
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk
export PATH=$PATH:$JAVA_HOME/bin:$STROM_HOME/bin
```
lalu simpan dan keluar dari text editor lalu jalankan command
```
source ~/.bashrc
```
2. Install ZooKeeper Framework
Download zookeeper kunjungi link dibawah ini <br>
https://zookeeper.apache.org/releases.html<br>
lalu lalukan extrack atau juga bisa jalankan seperti dibawah ini :
```
tar -zxf zookeeper-3.4.6.tar.gz
```
lalu configurasi file ada di "conf/zoo.cfg” atau bisa juga edit dengan command dibawah ini :
```
vim conf/zoo.cfg
```
lalu edit seperti ini :
```
tickTime=2000
dataDir=/path/to/zookeeper/data
clientPort=2181
initLimit=5
syncLimit=2
```
lalu untuk menjalankan zookeeper
```
bin/zkServer.sh start
```
jika ingin menghentikan zookeeper
```
bin/zkServer.sh stop
```
3. Install Apache Storm
Downlaod apache storm bisa kunjungi halaman dibawah ini :<br>
https://storm.apache.org/downloads.html<br>
lalu lalukan extrack atau juga bisa jalankan seperti dibawah ini :
```
tar -zxf apache-storm-2.4.0.tar.gz
```
lalu configurasi file ada di "conf/storm.yaml" atau bisa juga edit dengan command dibawah ini :
```
storm.zookeeper.servers:
 - "localhost"
storm.local.dir: “/path/to/storm/data(any path)”
nimbus.seeds: ["localhost"]
```
```
lalu simpan dan keluar, lalu jalan command berikut :
```
```
bin/storm nimbus
```
```
bin/storm supervisor
```
```
bin/storm ui
```
lalu buka browser lalu ketikan di url http://localhost:8080, jika terjadi error 404 maka tambahkan 
```
ui.host: 0.0.0.0
ui.port: 8081
```
lalu untuk url diketikan http://localhost:8081, jika sudah selesai maka jalankan 
```
bin/storm nimbus
```
```
bin/storm supervisor
```
```
bin/storm ui
```
untuk pom.xml dependency
```
  <dependencies>
    <dependency>
      <groupId>org.apache.storm</groupId>
      <artifactId>storm-core</artifactId>
      <version>2.4.0</version>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>org.junit.jupiter</groupId>
      <artifactId>junit-jupiter-api</artifactId>
      <version>5.9.0</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
```
pom.xml plugin
```
<build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.2</version>
        <configuration>
          <source>1.8</source>
          <target>1.8</target>
        </configuration>
      </plugin>
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
        <version>1.3.2</version>
        <executions>
          <execution>
            <goals>
              <goal>exec</goal>
            </goals>
          </execution>
        </executions>
        <configuration>
          <executable>java</executable>
          <includeProjectDependencies>true</includeProjectDependencies>
          <includePluginDependencies>false</includePluginDependencies>
          <classpathScope>compile</classpathScope>
        </configuration>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
        <version>1.3.3</version>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>shade</goal>
            </goals>
            <configuration>
              <createDependencyReducedPom>false</createDependencyReducedPom>
              <transformers>
                <transformer
                        implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer" />
                <transformer
                        implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                  <mainClass>org.apache.storm.flux.Flux</mainClass>
                  <manifestEntries>
                    <Change></Change>
                    <Build-Date></Build-Date>
                  </manifestEntries>
                </transformer>
              </transformers>
              <!-- The filters below are necessary if you want to include the Tika
                  module -->
              <filters>
                <filter>
                  <artifact>*:*</artifact>
                  <excludes>
                    <exclude>META-INF/*.SF</exclude>
                    <exclude>META-INF/*.DSA</exclude>
                    <exclude>META-INF/*.RSA</exclude>
                  </excludes>
                </filter>
                <filter>
                  <!-- https://issues.apache.org/jira/browse/STORM-2428 -->
                  <artifact>org.apache.storm:flux-core</artifact>
                  <excludes>
                    <exclude>org/apache/commons/**</exclude>
                    <exclude>org/apache/http/**</exclude>
                    <exclude>org/yaml/**</exclude>
                  </excludes>
                </filter>
              </filters>
            </configuration>
          </execution>
        </executions>
      </plugin>
      <plugin>
        <artifactId>maven-assembly-plugin</artifactId>
        <configuration>
          <archive>
            <manifest>
              <mainClass>
                org.example.WordReaderTopology
              </mainClass>
            </manifest>
          </archive>
          <descriptorRefs>
            <descriptorRef>jar-with-dependencies</descriptorRef>
          </descriptorRefs>
        </configuration>
      </plugin>
    </plugins>
  </build>
```
```
  <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.target>1.8</maven.compiler.target>
        <maven.compiler.source>1.8</maven.compiler.source>
  </properties>
```
