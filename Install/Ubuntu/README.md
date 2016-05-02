# 3.1 Ubuntu

##Ubuntu安裝Docker

---

Docker 支援這些 Ubuntu 版本號:

- Ubuntu Xenial 16.04 (LTS)
- Ubuntu Wily 15.10
- Ubuntu Trusty 14.04 (LTS)
- Ubuntu Precise 12.04 (LTS)

在安裝Docker之前，他有幾項聲明:

- 需要64-bit的Ubuntu系統

- Kernel必須不小於於3.10

- 3.10次要或更新維護版本是可以接受的

若沒有這些前提，安裝後可能會造成Docker無法使用

如果你不知道你的內核

可以使用以下指令

```
$ uname -r
```

可以透過系統內建套件安裝

```
$ sudo apt-get update                  //更新Ubuntu的套件
$ sudo apt-get install docker-engine   //安裝Docker
```

快速安裝

```
curl http://files.imaclouds.com/scripts/docker_install.sh | sh
```

安裝後可以試試看如何開啟並建立Docker

```
$ sudo service docker start            //開啟Docker
$ sudo docker run hello-world          //Run一個Docker 確定是沒問題的
```


---