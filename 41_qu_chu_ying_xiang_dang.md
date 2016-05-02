# 4.1. 取出映像檔

##取得映像檔

---

使用 ```docker pull ``` 命令從Repository取得所需要的Image。

下面的例子是從我自己的Docker Hub倉儲下載一個Image。

pull後面是你在Docker Hub上的名稱 Id/Repository。

```
$ sudo docker pull wolibohebadon/ca22006

latest: Pulling from wolibohebadon/ca22006 //最新的下載image位置在wolibohebadon/ca22006
//顯示
759d6771041e: Download complete
8836b825667b: Download complete
c2f5e51744e6: Download complete
a3ed95caeb02: Download complete
4afafbda1c91: Download complete
d969199cf5fa: Download complete
a8b48361e793: Download complete
c9dfe10bdabc: Download complete
```

另一個例子是從Docker Hub倉儲下載一個Ubuntu14.04作業系統的映像檔。


```
$ sudo docker pull ubuntu:14.04
//顯示
14.04: Pulling from library/ubuntu
943c334059c7: Pull complete 
a1acf99303d2: Pull complete 
27616aacb7b3: Pull complete 
35d12cd1c9fc: Pull complete 
a3ed95caeb02: Pull complete 
```

下載完畢後，就可以使用這個印象檔，可以建立一個容器,讓他去執行bash

```
$ sudo docker run -ti ubuntu:14.04 /bin/bash   //執行後會進入docker內
//顯示
root@1133d5eb031f:/#
```

---