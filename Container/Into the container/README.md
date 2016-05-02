# 5.4. 進入容器

##進入容器
---
###進入容器
---

在使用 ```-d``` 參數時，Container啟動後會進入後臺。 某些時候需要進入Container進行操作，有很多種方法，包括使用 ```docker attach``` 命令或 ```nsenter``` 工具等。

**exec 命令**
```
$ sudo docker run -tdi ubuntu
//顯示
80787210307a297f886c851e803a142a8fcb5a0f0b7aec1d1a7e2c772284d652
$ sudo docker ps
//顯示
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
80787210307a        ubuntu              "/bin/bash"         13 seconds ago      Up 12 seconds                           boring_easley
$ sudo docker exec -ti boring_easley bash
//顯示
root@80787210307a:/# 
```
**attach 命令**

```docker attach``` 亦是Docker內建的命令。下面示例如何使用該命令。

```
sudo docker run -idt ubuntu
//顯示
31f9479fec8be34fb782b5bbb6f6f90d341596fb605d274c90b3ebec9b215912
$ sudo docker ps
//顯示
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
31f9479fec8b        ubuntu              "/bin/bash"         24 seconds ago      Up 23 seconds                           cranky_visvesvaraya
$ sudo docker attach cranky_visvesvaraya
//顯示
root@31f9479fec8b:/#  
```
但是使用 attach 命令有時候並不方便。當多個窗口同時 attach 到同一個Container的時候，所有窗口都會同步顯示。當某個窗口因命令阻塞時,其他窗口也無法執行操作了。

**nsenter 命令**

**安裝**

```nsenter``` 直接下載最新版2.28版來使用

```
$ curl https://www.kernel.org/pub/linux/utils/util-linux/v2.28/util-linux-2.28.tar.gz | tar -zxf-; cd util-linux-2.28
$ ./configure --without-ncurses
$ make nsenter && sudo cp nsenter /usr/local/bin
```
**使用**

```nsenter``` 可以存取另一個程式的命名空間。```nsenter``` 要正常工作需要有 root 權限。


```
$ sudo docker run -tdi ubuntu
//顯示
dc947049c99b805ba705319c02ce76385794b1f5b3e5526e54aca04428bf417d
$ sudo docker ps
//顯示
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
dc947049c99b        ubuntu              "/bin/bash"         2 minutes ago       Up 2 minutes                            high_swartz
$ echo $(docker-pid dc947049c99b)
//顯示
13830
$ sudo nsenter --target 13830 --mount --uts --ipc --net --pid
顯示
root@dc947049c99b:/# 
```
再使用上面的指令之前，請先執行下面的命令

```
$ wget -P ~ https://github.com/yeasy/docker_practice/raw/master/_local/.bashrc_docker;
$ echo "[ -f ~/.bashrc_docker ] && . ~/.bashrc_docker" >> ~/.bashrc; source ~/.bashrc
```
透過上面這個指令就可以定義很多Docker的命令

---