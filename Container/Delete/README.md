# 5.6. 刪除

##刪除
---
###刪除容器
---
可以使用```docker rm```來刪除一個處於終止狀態的Container。

EX：

```
$ sudo docker rm 9e5b1a1c60ae
9e5b1a1c60ae
```
如果要刪除一個執行中的容器，可以新增 -f 參數。Docker 會發送 ```SIGKILL``` 信號給容器。

---