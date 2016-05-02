# 4.4. 存出和載入

##存取和載入

---

###儲存和載入映像檔

**儲存映像檔**

如果要建立Image到本地檔案，可以使用 ```docker save``` 命令。

```
$ sudo docker images
//顯示
REPOSITORY              TAG                 IMAGE ID            CREATED             SIZE
wolibohebadon/ubuntu    v2                  cbb6010622f8        52 minutes ago      408.1 MB
$ sudo docker save -o ubuntu_14.04.tar ubuntu:14.04
```
**載入映像檔**

可以使用 ```docker load```從建立的本地檔案中再匯入到本地Image庫，例如

```
sudo docker load --input ubuntu_14.04.tar
//或
sudo docker load < ubuntu_14.04.tar
```
可以匯入之前儲存的Image

---