# 4.5. 移除

##移除

---

##移除本地端映像檔

如果要移除本地端的Image，可以使用 ```docker rmi``` 命令。注意 ```docker rm ```命令是移除容器。

```
$sudo docker rmi wolibohebadon/ubuntu:v2
//顯示
$ sudo docker rmi wolibohebadon/ubuntu:v2
Untagged: wolibohebadon/ubuntu:v2
Deleted: sha256:cbb6010622f87b6d012f6b05202b3e1cca54688746b3a52dd9cdce3ea1184fb5
Deleted: sha256:d5137fa1b9f404280a7cedbce21318309ba9de17061fee9be40211ccd48b8929
Deleted: sha256:eedbe2998d7104f25da20b2b4fcd19f03572dbb656d7ee4f5e27e0c51196bc7b
Deleted: sha256:ce1215bc3de5d63bca766e5321323a681538f9b558554101722d39e20e0920bd
Deleted: sha256:daa9093d9660b8078b2072a9489d62d8720d5aee629d2d59d99b85de4e33b19a
Deleted: sha256:2a36e155695be823372b0c975a45bbec2a027f1d9d4b962e37bfbfdc0297203c
```
P.S.：在刪除映像檔之前要先用 ```docker rm``` 刪掉依賴於這個Image的所有Container。

---