###一、hbase预分区
	1.分区表
	create 'level2_kline', 'cf', SPLITS => ['10', '20', '30', '40','50','60','70','80','90']
	
	2.分区压缩表
	create 'td_alert_info', { NAME => 'cf', COMPRESSION => 'SNAPPY'},SPLITS => ['10', '20', '30', '40','50','60','70','80','90']

    3.hive与hbase映射表
	CREATE external TABLE IF NOT EXISTS td_alert_info( rowkey string ,action string,
                              event_label string ) 
                              STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler' 
                              WITH SERDEPROPERTIES ("hbase.columns.mapping" = ":key,
                              cf:action,
                              cf:event_label") 
                              TBLPROPERTIES("hbase.table.name" = "td_alert_info");
