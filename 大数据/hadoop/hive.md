##HIVE学习
###1.向指定分区插入数据
    insert OVERWRITE  table XX partition(dt='') select * from xx;
