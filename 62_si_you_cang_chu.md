# 6.2. 私有倉儲

##私有倉庫
---
###私有倉庫
---

有時候使用 Docker Hub 這樣的公共Repository可能不方便，使用者可以建立一個本機Repository供私人使用。

本節介紹如何使用本地Repository。

```docker-registry``` 是官方提供的工具，可以用於建立私有的Image Repository 。

**安裝執行 docker-registry**

**容器執行**

安裝了 Docker 後，可以透過取得官方 registry Image來執行。

```
$ sudo docker run -d -p 5000:5000 registry
```
這可以使用官方的 registry Image來啟動本機的私有Repository。

使用者可以透過指定參數來設定私有Repository位置，例如設定Image儲存到 Amazon S3 服務。

```
sudo docker run \
         -e SETTINGS_FLAVOR=s3 \
         -e AWS_BUCKET=acme-docker \
         -e STORAGE_PATH=/registry \
         -e AWS_KEY=AKIAHSHB43HS3J92MXZ \
         -e AWS_SECRET=xdDowwlK7TJajV1Y7EoOZrmuPEJlHYcNP2k4j49T \
         -e SEARCH_BACKEND=sqlalchemy \
         -p 8080:8080 \
         registry
.
```
此外，還可以指定本機路徑（如 /home/user/registry-conf ）下的設定檔案。

```
$ sudo docker run -d -p 8080:8080 -v /home/user/registry-conf:/registry-conf -e DOCKER_REGISTRY_CONFIG=/registry-conf/config.yml registry
```
假設Repository會被建立在Container的 /tmp/registry 下。可以透過 -v 參數來將Image檔案存放在本地的指定路徑。 例以下面的例子將上傳的Image放到 /opt/data/registry 目錄。

```
$ sudo docker run -d -p 8080:8080 -v /opt/data/registry:/tmp/registry registry
```
**本地安裝**

Ubuntu 或 CentOS 等發行版，可以直接透過套件庫安裝。

這邊只介紹Ubuntu

- Ubuntu
```
$ sudo apt-get install -y build-essential python-dev libevent-dev python-pip liblzma-dev swig
$ sudo pip install docker-registry
```
另一種方式可以到  [docker-registry](https://github.com/docker/docker-registry) 專案下載原始碼進行安裝。

```
$ sudo apt-get install build-essential python-dev libevent-dev python-pip libssl-dev liblzma-dev libffi-dev
$ git clone https://github.com/docker/docker-registry.git
$ cd docker-registry
$ sudo python setup.py install
```
再來修改設定檔案，主要修改 dev 模板段的 ```storage_path``` 到本地的儲存Repository的路徑。

```
$ cp config/config_sample.yml config/config.yml
```
