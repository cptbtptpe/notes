
## Docker 技巧

### 持久化容器

```shell
sudo docker export <CONTAINER ID> > ~/Downloads/export.tar

# Use it
cat ~/Downloads/export.tar | sudo docker import - export:latest
```

### 持久化镜像

```shell
sudo docker save <IMAGE ID> > ~/Downloads/save.tar

# Use it
sudo docker load < ~/Downloads/save.tar
```