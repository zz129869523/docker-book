# 5.2. 守護態執行

##守護態執行

---

###守護態執行

---

更多的時候，需要讓 Docker Container在後臺以守護態（Daemonized）形式執行。此時，可以透過新增 -d 參數來實作。

下面的命令會在後臺執行Container。

EX:

```
$ sudo docker run -d ubuntu:14.04 /bin/sh -c "while true; do echo hello world; sleep 1; done"
//顯示
c18eb0e7e0a6281277c6135e5df5161ad70d03954b0949615cc94650ad745051
```
Container啟動後會返回一個唯一的 id，也可以透過 docker ps 命令來查看Container訊息。

```
$ sudo docker ps
//顯示
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
c18eb0e7e0a6        ubuntu:14.04        "/bin/sh -c 'while tr"   8 minutes ago       Up 8 minutes                            cranky_minsky
```
要取得Container的輸出訊息，可以透過```docker logs``` 命令。

```
$ sudo docker logs cranky_minsky
//顯示
hello world
hello world
hello world
. . .
```

---