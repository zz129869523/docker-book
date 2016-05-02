# 5.3. 終止

##終止
---
###終止容器

可以使用 ```docker stop``` 來終止一個執行中的容器。

當Docker Container中指定的應用終結時，Container也自動終止。 例如對於上一章節中只啟動了一個終端機的Container，使用者透過 exit 命令或 Ctrl+d 來退出終端時，所建立的Container立刻終止。

終止狀態的Container可以用 ```docker ps -a``` 命令看到。

EX：

```
$ sudo docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                        PORTS               NAMES
ee3431ffe4b3        ubuntu:14.04        "/bin/sh -c 'while tr"   9 minutes ago       Up 9 minutes                                      kickass_swartz
4b4d2b481352        ubuntu:14.04        "/bin/sh -c 'while tr"   9 minutes ago       Up 9 minutes                                      cranky_panini
```
處於終止狀態的容器，可以透過 ```docker start``` 命令來重新啟動。

```
$ sudo docker start c10bdd5f2d28       //c10bdd5f2d28是你要開啟的id
```
此外，```docker restart``` 命令會將一個執行中的容器終止，然後再重新啟動它。

```
$ sudo docker restart 4b4d2b481352     //4b4d2b481352是你要重啟的id
```

---