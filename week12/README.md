
## InfluxDB 설치 
  - InfluxDB download key using wget
```
wget -q https://repos.influxdata.com/influxdata-archive_compat.key
echo '393e8779c89ac8d958f81f942f9ad7fb82a25e133faddaf92e15b16e6ac9ce4c influxdata-archive_compat.key' | sha256sum -c && cat influxdata-archive_compat.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/influxdata-archive_compat.gpg > /dev/null
echo 'deb [signed-by=/etc/apt/trusted.gpg.d/influxdata-archive_compat.gpg] https://repos.influxdata.com/debian stable main' | sudo tee /etc/apt/sources.list.d/influxdata.list
```
  - Packages are up to date && install Influxdb
```
 sudo apt-get update && sudo apt-get install influxdb -y

```
  - InfluxDB as a background service on startup
```
sudo service influxdb start
```
  - InfluxDB is status (service)
```
sudo service influxdb status
```
  
## InfluxDB 데이터베이스 만들기

```
$ influx

>create database <데이터베이스이름>
확인 : show databases 
```
## influxdb import with python
```
pip install influxdb
```


# Grafana Installation

## 1. Install the prerequisite packages
```
sudo apt-get install -y apt-transport-https software-properties-common wget
```

## 2. Import the GPG key:
```
sudo mkdir -p /etc/apt/keyrings/
wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
```

## 3. To add a repository for stable releases, run the following command:
```
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

## 4. Run the following command to update the list of available packages:
```
sudo apt-get update && sudo apt-get install grafana -y

```
## 5. Run the following command to server start
```
sudo systemctl start grafana-server
```

### vim dustInfluxdb.py
```
import time
import requests, json
import influxdb import InfluxDBClient as influxdb
import serial

seri = serial.Serial('/dev/ttyACM0', baudrate = 9600, timeout = None)

while(True):
  time.sleep(1)
  if seri.in_waiting != 0:
    content = seri.readline()
    a = float(content.decode())
    data = [{
      'measurement' : 'dust',
      'tags':{
          'InhaUni' : '2222',
      },
      'fields':{
          'dust' : a,
      }
  }]
client = None
try:
  client = influxdb('localhost', 8086, 'root', 'root', 'dust')
except Exception as e:
  print("Exception write " + str(e))
finally:
  client.close()
print(a)
print("running influxdb OK")
```
