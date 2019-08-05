---
title: 使用免安裝版的PostgresSQL建立空間資料庫
date: 2019-07-26 14:11:35
updated: 2019-08-02 13:05:00
categories:
- PostgreSQL
tags:
- 地理資料庫
---

本文將介紹如何使用`PostgreSQL`，在本機電腦上建置一個可以隨時帶著走的地理資料庫，方便程式開發階段或是教學階段時使用。

<!--more-->

## 《1》 檢查ArcGIS支援哪一個版本的PostgreSQL

1. 先到[ArcGIS Help頁面](http://desktop.arcgis.com/en/system-requirements/latest/database-requirements-postgresql.htm)選擇你要使用的ArcGIS版本

  ![選擇你要使用的ArcGIS版本](http://i.imgur.com/uQFnqql.png)

2. 查詢有支援的最小版本

  ![查詢支援度](https://i.imgur.com/iaqPryV.png)

## 《2》 下載PostgresSQL

1. [連到PostgreSQL官方網站](https://www.postgresql.org/download/windows/)
 
2. 點選[zip archive](https://www.enterprisedb.com/download-postgresql-binaries)

3. 選擇適合的版本下載  

## 《3》 讓PostgreSQL具有儲存空間資料的能力
 
1. 在ArcMap預設安裝目錄下，找到DatabaseSupport資料夾，預設安裝路徑為`C:\Program Files (x86)\ArcGIS\Desktop版本號碼\DatabaseSupport`
 
2. 找到PostgreSQL資料夾，然後依據你下載的版本，進入該版本的資料夾，然後再進入Windows64資料夾
 
3. 複製資料夾中的`st_geometry.dll`以及`libst_raster_pg.dll`，到 **PostgresSQL資料夾/lib** 中
 
## 《4》 初始化你的PostgreSQL

將以下程式碼複製到文字檔中，然後副檔案改成.bat儲存。然後執行這個批次檔。

```bash
@ECHO ON
REM The script sets environment variables helpful for PostgreSQL
@SET PATH="%~dp0\bin";%PATH%
@SET PGDATA=%~dp0\data
@SET PGDATABASE=postgres
@SET PGUSER=postgres
@SET PGPORT=5432
@SET PGLOCALEDIR=%~dp0\share\locale

REM remark after first run
rem "%~dp0\bin\initdb" -U postgres -A trust

"%~dp0\bin\pg_ctl" -D "%~dp0/data" -l logfile start
ECHO "Click enter to stop"
pause
"%~dp0\bin\pg_ctl" -D "%~dp0/data" stop
```