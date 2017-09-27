```sql
create external table `syslogrecord` (
`dateTime` string , `client` string , `messageID` string , `messageString` string
)
stored as parquet
location '/user/hive/syslog/v1/syslogrecord'
```

```
tail -f /var/log/syslog |nc -l 7088
```

```
sbt clean package
scp target/scala-2.10/spark-streaming-proof_2.10-1.0.jar userid@remotehost:/tmp/upload/
```

```
spark-submit --master local[2] --class spark.streaming.proof.SysLogReceiver /tmp/upload/sspark-streaming-proof_2.10-1.0.jar  172.28.128.11 7088
```