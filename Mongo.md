## Mongo

### 导出数据(文件sql)

```  
mongoexport 
  -h10.10.241.157:27017 
  -utxweb 
  -ptxwebdb 
  -dweather 
  -cdevice 
  --csv 
  -f _id,sid,cpu,sn,uuid,os,ip,mb,client_time,date,addtime 
  --queryFile=query.json 
  -o /web/20160607-3063.csv  
```  
  
> query.json  

```  
{  
    "channel.$id": ObjectId("574fd8f7160ba061478b4b16"),  
    "date": ISODate("2016-06-06T16:00:00Z")  
}  
```  
  
### 导出数据(显式sql)  

```  
mysql 
  -h127.0.0.1 
  -uwuguolin 
  -pjiuyi 
  -P3308 
  -D receive_flow_oa 
  -e "select channel_num,sid,count(*) as total from device_score_lively_xyweather where channel_num = 400002 and date = '2016-07-17' group by sid"
> ~/Downloads/400002_20160717_live.csv  
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
        $gt: new Date(2016,4,13,23),  
        $lt: new Date(2016,4,14,8)  
    },  
    type: 1  
}).count()  
```  
