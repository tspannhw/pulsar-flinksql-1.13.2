### pulsar-flinksql-1.13.2

```
sqllib

avro-1.10.0.jar					flink-sql-avro-1.12.1.jar
flink-json-1.12.1.jar				pulsar-flink-sql-connector_2.11-1.12.4.6.jar

cd /Users/tspann/Documents/servers/flink112
./bin/start-cluster.sh
./bin/sql-client.sh embedded --library /Users/tspann/Documents/servers/flink112/sqllib


CREATE TABLE iotjetsonjson
(
  `id` STRING, uuid STRING, ir STRING,
  `end` STRING, lux STRING, gputemp STRING, 
  cputemp STRING, `te` STRING, systemtime STRING, hum STRING,
 memory STRING, gas STRING, pressure STRING, 
 `host` STRING, diskusage STRING, ipaddress STRING, macaddress STRING, 
  gputempf STRING, host_name STRING, camera STRING, filename STRING, 
    `runtime` STRING, cpu STRING,cputempf STRING, imageinput STRING,
    `networktime` STRING, top1 STRING, top1pct STRING, 
  publishTime TIMESTAMP(3) METADATA,
  WATERMARK FOR publishTime AS publishTime - INTERVAL '5' SECOND
) WITH (
  'connector' = 'pulsar',
  'topic' = 'persistent://public/default/iotjetsonjson',
  'value.format' = 'json',
  'scan.startup.mode' = 'earliest',
  'service-url' = 'pulsar://pulsar1:6650',
  'admin-url' = 'http://pulsar1:8080'
);


CREATE TABLE default_catalog.default_database.scada 
(
   uuid STRING, 
	systemtime STRING,  
	ipaddress STRING, host STRING, 
	host_name STRING, macaddress STRING, 
	endtime STRING, runtime STRING, 
	starttime STRING,
  publishTime TIMESTAMP(3) METADATA,
  WATERMARK FOR publishTime AS publishTime - INTERVAL '5' SECOND
) WITH (
  'connector' = 'pulsar',
  'topic' = 'persistent://public/default/mqtt-2',
  'value.format' = 'json',
  'service-url' = 'pulsar://pulsar1:6650',
  'admin-url' = 'http://pulsar1:8080',
  'scan.startup.mode' = 'earliest'
);


CREATE TABLE pulsar (
  `physical_1` STRING,
  `physical_2` INT,
  `eventTime` TIMESTAMP(3) METADATA,
  `properties` MAP<STRING, STRING> METADATA ,
  `topic` STRING METADATA VIRTUAL,
  `sequenceId` BIGINT METADATA VIRTUAL,
  `key` STRING ,
  `physical_3` BOOLEAN
) WITH (
  'connector' = 'pulsar',
  'topic' = 'persistent://public/default/topic82547611',
  'key.format' = 'raw',
  'key.fields' = 'key',
  'value.format' = 'avro',
  'service-url' = 'pulsar://localhost:6650',
  'admin-url' = 'http://localhost:8080',
  'scan.startup.mode' = 'earliest' 
)

CREATE TABLE iotjetsonjson2
(
  `id` STRING, uuid STRING, ir STRING,
  `end` STRING, lux STRING, gputemp STRING, 
  cputemp STRING, `te` STRING, systemtime STRING, hum STRING,
 memory STRING, gas STRING, pressure STRING, 
 `host` STRING, diskusage STRING, ipaddress STRING, macaddress STRING, 
  gputempf STRING, host_name STRING, camera STRING, filename STRING, 
    `runtime` STRING, cpu STRING,cputempf STRING, imageinput STRING,
    `networktime` STRING, top1 STRING, top1pct STRING, 
  publishTime TIMESTAMP(3) METADATA,
  WATERMARK FOR publishTime AS publishTime - INTERVAL '5' SECOND
) WITH (
  'connector' = 'pulsar',
  'topic' = 'persistent://public/default/iotjetsonjson',
  'value.format' = 'json',
  'scan.startup.mode' = 'earliest',
  'service-url' = 'pulsar://pulsar1:6650',
  'admin-url' = 'http://pulsar1:8080',  
  'key.format' = 'raw',
  'key.fields' = 'uuid',
  'scan.startup.mode' = 'earliest' 
);


CREATE TABLE iotjetsonjson3
(
  `id` STRING, uuid STRING, ir STRING,
  `end` STRING, lux STRING, gputemp STRING, 
  cputemp STRING, `te` STRING, systemtime STRING, hum STRING,
 memory STRING, gas STRING, pressure STRING, 
 `host` STRING, diskusage STRING, ipaddress STRING, macaddress STRING, 
  gputempf STRING, host_name STRING, camera STRING, filename STRING, 
    `runtime` STRING, cpu STRING,cputempf STRING, imageinput STRING,
    `networktime` STRING, top1 STRING, top1pct STRING, 
  publishTime TIMESTAMP(3) METADATA,
  WATERMARK FOR publishTime AS publishTime - INTERVAL '5' SECOND
) WITH (
  'connector' = 'pulsar',
  'topic' = 'persistent://public/default/iotjetsonjson',
  'value.format' = 'json',
  'service-url' = 'pulsar://pulsar1:6650',
  'admin-url' = 'http://pulsar1:8080'
);

CREATE TABLE iotjetsonjson4
(
  uuid STRING, 
  camera STRING, 
  ipaddress STRING, 
   `networktime` STRING,
  `end` STRING, 
  gputemp STRING, 
  cputemp STRING, 
  `te` STRING, 
  systemtime STRING, 
 memory STRING, 
 `host` STRING,
 diskusage STRING,
 macaddress STRING, 
  gputempf STRING,
  host_name STRING, 
  filename STRING, 
    `runtime` STRING, 
    cpu STRING,
    cputempf STRING,
    imageinput STRING,
    `networktime` STRING, 
    top1 STRING,
    top1pct STRING, 
  publishTime TIMESTAMP(3) METADATA,
  WATERMARK FOR publishTime AS publishTime - INTERVAL '5' SECOND
) WITH (
  'connector' = 'pulsar',
  'topic' = 'persistent://public/default/iotjetsonjson',
  'value.format' = 'json',
  'service-url' = 'pulsar://pulsar1:6650',
  'admin-url' = 'http://pulsar1:8080'
);

"networktime": 24.937471389770508, "top1pct": 12.030029296875, "top1": "disk brake, disc brake", "cputemp": "29.0", "gputemp": "29.0", "gputempf": "84", "cputempf": "84", "runtime": "5", "host": "nvidia-desktop", "filename": "/home/nvidia/nvme/images/out_video0_wrr_20220111163943.jpg", "imageinput": "/home/nvidia/nvme/images/img_video0_ghy_20220111163943.jpg", "host_name": "nvidia-desktop", "macaddress": "70:66:55:15:b4:a5", "te": "5.482345104217529", "systemtime": "01/11/2022 11:39:48", "cpu": 8.7, "diskusage": "24600.9 MB", "memory": 33.6}

{"uuid": "xav_uuid_video0_pqd_20220111164311", "camera": "/dev/video0", "ipaddress": "192.168.1.235", "networktime": 24.987648010253906, "top1pct": 17.3095703125, "top1": "mountain bike, all-terrain bike, off-roader", "cputemp": "29.0", "gputemp": "29.0", "gputempf": "84", "cputempf": "84", "runtime": "6", "host": "nvidia-desktop", "filename": "/home/nvidia/nvme/images/out_video0_hhh_20220111164311.jpg", "imageinput": "/home/nvidia/nvme/images/img_video0_lhu_20220111164311.jpg", "host_name": "nvidia-desktop", "macaddress": "70:66:55:15:b4:a5", "te": "5.5451154708862305", "systemtime": "01/11/2022 11:43:16", "cpu": 8.3, "diskusage": "24600.9 MB", "memory": 33.5}


select top1, top1pct, cputempf, gputempf, cpu, filename, memory, systemtime, publishTime, ipaddress from iotjetsonjson4;
```

### Postgresql Sink 2.9.1

* https://github.com/tspannhw/FLiP-CloudIngest
* https://github.com/streamnative/pulsar-flink
* https://github.com/tspannhw/FLiP-SQL


