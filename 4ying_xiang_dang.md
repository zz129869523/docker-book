# 4.映像檔

##映像檔

---

在前面我有先提到Docker是由三個部分所組成，首先是映像檔。

Docker 在執行Container前需要有本地端存在對應的Image，如果Image不存在本地端，Docker會從Image Repository下載（預設是 Docker Hub 公共註冊伺服器中的Repository）。

這邊會提到三件事：

- 如何從Repository取得Image
- 管理本地主機上的Image
- 介紹Image實作的基本原理

---