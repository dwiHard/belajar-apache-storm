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
