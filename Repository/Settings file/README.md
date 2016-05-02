#6.3. 設定檔案

##倉庫設定檔案
---

Docker 的 Registry 利用設定檔案提供了一些Repository的模組（flavor），使用者可以直接使用它們來進行開發或生產部署。

###模組

在 config_sample.yml 檔案中，可以看到一些現成的模組：

- `common`：基礎設定
- `local`：儲存資料到本地檔案系統
- `s3`：儲存資料到 AWS S3 中
- `dev`：使用 local 模組的基本設定
- `test`：單元測試使用
- `prod`：生產環境設定（基本上跟s3設定類似）
- `gcs`：儲存資料到 Google 的雲端
- `swift`：儲存資料到 OpenStack Swift 服務
- `glance`：儲存資料到 OpenStack Glance 服務，本地檔案系統為後備
- `glance-swift`：儲存資料到 OpenStack Glance 服務，Swift 為後備
- `elliptics`：儲存資料到 Elliptics key/value 儲存

