#資料卷

資料卷是一個可供一個或多個Container UFS，可以提供很多有用的特性：

- 卷可以在Container之間共享和重用

- 如果你對資料卷更新，並不會影響Image

- 對資料卷的修改會立刻生效

- 卷會一直存在，直到沒有Container

P.S.資料卷的使用，有點像 Linux下對目錄或檔案進行 mount。

[mount](http://linux.vbird.org/linux_basic/0230filesystem.php#harddisk-mount)

**建立一個資料卷**

在用 `docker run` 命令的時候，使用` -v `標記來建立一個資料卷並掛載到Container裡。在一次 run 中多次使用可以掛載多個資料卷。

下面建立一個web容器，並載入一個資料卷到容器的 `/webapp `目錄。

```
$ sudo docker run -d -P --name web -v /webapp training/webapp python app.py
```
注意：可以在 `Dockerfile` 中使用 `VOLUME` 來新增一個或者多個新的卷到由該Image建立的任意Container。

**掛載一個主機目錄作為資料卷**

使用 `-v` 標記也可以指定掛載一個本地主機的目錄到容器中去。

```
$ sudo docker run -d -P --name web -v /src/webapp:/opt/webapp training/webapp python app.py
```

上面的命令載入主機的 `/src/webapp`目錄到Container的`/opt/webapp` 目錄。這個功能在進行測試的時候十分方便。

**EX**：使用者可以放置一些程式到本地目錄中，來查看Container是否正常工作。本地目錄的路徑必須是絕對路徑，如果目錄不存在 Docker 會自動為你建立它。

**注意**：Dockerfile 中不支援這種用法，這是因為 Dockerfile 是為了移植Image和分享用的。然而，不同作業系統的路徑格式不一樣，所以目前還不能支援。

Docker 掛載資料卷的預設權限是讀寫，使用者也可以透過 `:ro` 指定為唯讀。

```
$ sudo docker run -d -P --name web -v /src/webapp:/opt/webapp:ro
training/webapp python app.py
```

加了 `:ro` 之後，就掛載為唯讀了。

掛載一個本地主機檔案作為資料卷

`-v` 標記也可以從主機掛載單個檔案到容器中
```
$ sudo docker run --rm -it -v ~/.bash_history:/.bash_history ubuntu /bin/bash
```

這樣就可以記錄在容器輸入過的命令了。

**注意**：如果直接掛載一個檔案，很多檔案編輯工具，包括 `vi` 或者 `sed --in-place`，可能會造成檔案 inode 的改變，從 Docker 1.1 .0起，這會造成回報錯誤訊息。所以最簡單的辦法就直接掛載檔案的父目錄。
