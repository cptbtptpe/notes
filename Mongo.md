## Mongo

### 导出数据(文件 sql)

```  
mongoexport 
  -h 1 0.1 0.2 4 1.1 5 7:2 7 0 1 7 
  -utxweb 
  -ptxwebdb 
  -dweather 
  -cdevice 
  --csv 
  -f _id,sid,cpu,sn,uuid,os,ip,mb,client_time,date,addtime 
  --queryFile=query.json 
  -o /web/2 0 1 6 0 6 0 7-3 0 6 3.csv  
```  
  
> query.json  

```  
{  
    "channel.$id": ObjectId("5 7 4fd 8 f 7 1 6 0ba 0 6 1 4 7 8b 4 b 1 6"),  
    "date": ISODate("2 0 1 6-0 6-0 6 T 1 6:0 0:0 0 Z")  
}  
```  
  
### 导出数据(显式 sql)  

```  
mysql 
  -h 1 2 7.0.0.1 
  -uwuguolin 
  -pjiuyi 
  -P 3 3 0 8 
  -D receive_flow_oa 
  -e "select channel_num,sid,count(*) as total from device_score_lively_xyweather where channel_num = 4 0 0 0 0 2 and date = '2 0 1 6-0 7-1 7' group by sid"
> ~/Downloads/4 0 0 0 0 2 _ 2 0 1 6 0 7 1 7_live.csv  
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
        $gt: new Date(2 0 1 6,4,1 3,2 3),  
        $lt: new Date(2 0 1 6,4,1 4,8)  
    },  
    type: 1  
}).count()  
```  
