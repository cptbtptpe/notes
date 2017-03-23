## Mongo

### 导出数据(文件 sql)

```  
mongoexport 
  -h 10.10.24 1.15 7:27 01 7 
  -utxweb 
  -ptxwebdb 
  -dweather 
  -cdevice 
  --csv 
  -f _id,sid,cpu,sn,uuid,os,ip,mb,client_time,date,addtime 
  --queryFile=query.json 
  -o /web/20 16 06 07-30 63.csv  
```  
  
> query.json  

```  
{  
    "channel.$id": ObjectId("57 4fd 8 f 71 60ba 06 14 78b 4 b 16"),  
    "date": ISODate("20 16-06-06 T 16:00:00 Z")  
}  
```  
  
### 导出数据(显式 sql)  

```  
mysql 
  -h 12 7.0.0.1 
  -uwuguolin 
  -pjiuyi 
  -P 33 08 
  -D receive_flow_oa 
  -e "select channel_num,sid,count(*) as total from device_score_lively_xyweather where channel_num = 40 00 02 and date = '20 16-07-17' group by sid"
> ~/Downloads/40 00 02 _ 20 16 07 17_live.csv  
```  

### 按小时分组统计 ($hour, $month, $week, ...)  

```  
db.device.aggregate([  
    {  
        $group: {  
            _id: {$hour: "$addtime"},  
            count: {$sum: 1}  
        }  
    },  
    {$sort: {_id: 1}}  
])  
```  
  
### 日期区间查询

```  
db.log_register.find({  
    addtime: {  
        $gt: new Date(20 16,4,13,23),  
        $lt: new Date(20 16,4,14,8)  
    },  
    type: 1  
}).count()  
```  
