---
title: ArcGIS Enterprise 系統安裝概要
date: 2019-08-02 15:56:35
categories:
- ArcGIS
- ArcGIS Enterprise
tags:
- 軟體安裝
---

ArcGIS Enterprise是一套完整的**雲端地理資訊平台**，它包含多個基礎元件、針對特定需求的Server Role與擴充模組，以因應不同客戶的實際應用需求。

由於軟體元件眾多，為了讓讀者能快速安裝好一台最基本的ArcGIS Enterprise，以下針對必須要安裝的基礎元件進行詳細說明，讓讀者能了解安裝過程中，每一個設定的意義。

<!-- more -->

## 軟體安裝順序

ArcGIS Enterprise產品包含4個基礎元件，分別是`ArcGIS for Server`、`Portal for ArcGIS`、`ArcGIS Data Store`、`ArcGIS Web Adaptor`。

{% note info %} 
設定時，`一定要先設定ArcGIS for Server，再設定ArcGIS Data Store` ，其他元件的設定順序則沒有強制性。 
{% endnote %}

筆者慣用的軟體安裝與更新順序如下，提供給讀者參考：

1. Portal for ArcGIS
2. ArcGIS for Server
3. ArcGIS Data Store
4. ArcGIS Web Adaptor

## 元件概述

ArcGIS Enterprise基礎元件功能概述如下：

| 產品名稱  | 功能描述  |
|--------------------   |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  |
| ArcGIS for Server     | **主要用途是提供網路服務功能。** <br>在管理介面中，您可以任意開啟或關閉指定的網路服務；您也可以為ArcGIS Server 站臺加入多台機器，提高網站的效能及應變能力。    |
| Portal for ArcGIS     | **主要用途是提供入口網站後台的功能。** <br>透過Portal for ArcGIS，您快速整合ArcGIS for Server所提供的網路服務、建立線上地圖，並藉由多元的應用程式樣板，達到敏捷開發與快速應變的能力。  |
| ArcGIS Data Store     | **主要用途是作為Portal for ArcGIS入口網站的資料庫。** <br>它內建`圖徵圖層`、`3D場景快取圖層`，以及`大量時空數據資料`的儲存結構定義檔，讓使用者可以透過入口網站Portal for ArcGIS，輕鬆將手邊數據資料分享呈多元的網路服務。<br>資料本體儲存在ArcGIS Data Store的網路服務，在項目說明頁面會出現`(託管)`的字樣。   |
| ArcGIS Web Adaptor    | **主要用途是作為反向代理伺服器使用。** <br>ArcGIS Web Adaptor是佈署在網頁伺服器(如IIS、Apache Tomcat)上的應用程式，可以將來自客戶端的請求轉送至Portal for ArcGIS或ArcGIS for Server的電腦，讓您可以使用80 (http)或443 (https)連接埠公開ArcGIS for Server以及 Portal for ArcGIS。<br>如果網頁伺服器支援使用`組織身份儲存庫`(例如Active Directory, **AD**; Lightweight Directory Access Protocol, **LDAP**)和安全性原則的功能，便能提供單一登入，或其他自訂身分驗證的體驗。  |

## ArcGIS Enterprise帳號說明

安裝ArcGIS Enterprise過程中，您需要建立多組帳號，以下就安裝過程所建立的帳號進行概述。

| 給什麼程式用 | 說明 | 用途 | 原廠預設值 |
|-------------|-----|------|------------|
| Windows 作業系統 | 作業系統使用者 | 啟動和停止 ArcGIS Server、 Portal for ArcGIS、 ArcGIS Datastore的`作業系統服務程序` <br> 讀寫 ArcGIS Server的站台設定檔、 Portal for ArcGIS的網站設定檔 、ArcGIS Datastore的設定檔<br> 讀取ArcGIS圖層或網路服務的原始數據資料 <br> 讀寫ArcGIS Server、Portal for ArcGIS 、ArcGIS Datastore的log檔 | arcgis |
| ArcGIS for Server | 主要站臺管理員 | 最初用來登入ArcGIS Server管理介面的帳號 <br> 可用來新增ArcGIS for Server站臺使用者帳號 | siteadmin |
| Portal for ArcGIS | 初始管理員 | 第一個登入Portal for ArcGIS的管理員帳號 <br> 可以管理Portal for ArcGIS入口網站 | 沒有預設值 |