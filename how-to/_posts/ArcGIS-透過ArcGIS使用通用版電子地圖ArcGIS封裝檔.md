---
title: 通用版電子地圖ArcGIS封裝檔使用方式
date: 2019-08-02 17:07:35
categories:
- ArcGIS
tags:
- 通用版電子地圖
- ArcGIS封裝檔
---

## 一、 通用版電子地圖ArcGIS封裝檔簡介

通用版電子地圖ArcGIS封裝檔是國土測繪中心製作公開的資料，允許使用者在電腦、行動裝置上離線瀏覽地圖。下載來的檔案解壓縮後，目錄結構會類似下圖，此為ArcGIS Cache Service的檔案結構。

  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/01/image1.png)

由於國土測繪沒有附上Cache Service的圖磚定義檔案(Conf.xml與conf.cdi)，所以使用者需要自己建立，或是直接[下載已經建立好的定義檔](https://drive.google.com/drive/folders/1BiopRK44EYJUWZTo1gX_88_2-hAQSbix?usp=sharing)，才能在ArcMap或是對應的軟體中開啟地圖資料。<!-- more -->

接下來會介紹如何自己建立圖磚定義檔案，並說明建立圖磚定義檔時，需要注意那些細節。

## 二、 建立圖磚定義檔需要注意的細節

圖磚定義檔建立時，需要確定以下幾件事情：

1.  **圖層座標系統。** <br>通用版電子地圖使用Web Mercator投影座標系統(EPSG:3857)。<br><br>
2.  **每一層(Level)的裁切比例尺與解析度。** <br>本文所使用的通用版電子地圖是依據Google Map的比例進行裁切。<br><br>
3.  **圖片格式**。<br>本文通用版電子地圖使用`jpg`格式作為圖磚的圖片格式。<br><br>
4.  **圖磚儲存方式**。<br>圖磚儲存方式可分為`EXPLODED`或是`COMPACT`兩種，EXPLODED直接將每張圖片儲存在資料夾內，COMPACT則是將一個的圖片壓縮成一個bundle檔案儲存。本文中的通用版電子地圖採用EXPLODED方式儲存圖片。

了解以上幾件事情後，就可以按照接下來的步驟，瀏覽電子地圖的內容囉。

## 三、 電子地圖使用方法：發佈為ArcGIS Server服務

#### 《1》 下載圖磚圖片檔案

1.  到國土測繪中心網站[<https://maps.nlsc.gov.tw/>](https://maps.nlsc.gov.tw/)
2.  點選下載專區
3.  找到以下兩個清單項目，點選右邊下載連結即可下載

  `[政府開放資料]臺灣通用電子地圖(套疊等高線)圖磚封裝檔(GIS用)`

  `[政府開放資料]臺灣通用電子地圖(不含等高線)圖磚封裝檔(GIS用)`

  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image1.png)

#### 《2》 建立Web Mercator座標系統的地圖圖框

1.  開啟ArcMap
2.  在Table Of Contents視窗中，對Layers圖框按滑鼠右鍵，選擇Properties

  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image2.png)

3.  定義地圖框坐標系統
    
    A. 在Data Frame Properties視窗中，切換到`Coordinate System`
    B. 在搜尋列中，輸入`web`，然後點選右邊的搜尋按鈕
    C. 找到如下圖所示的座標系統定義檔，然後按`確定`

  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image3.png)

#### 《3》 產生台灣全島範圍向量圖徵 (Featrue Class)

1.  加入 Streets底圖

  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image4.png)
  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image5.png)

2.  調整地圖範圍涵蓋台灣全島
3.  啟用`Draw`工具列

  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image6.png)

4.  使用矩形工具，在地圖上繪製台灣本島範圍

  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image7.png)
  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image8.png)

5.  使用`Convert Graphics To Features`工具，將矩形圖形轉換成Feature Class

  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image9.png)

6.  工具參數設定如下，本文中輸出的Feature Class命名為TaiwanExtent

  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image10.png)

7.  將TaiwanExtent圖層加入圖框中

  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image11.png)

8.  移除稍早所繪製的矩形圖形

  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image12.png)

#### 《4》 產生地圖文件檔案mxd

1.  移除底圖，TOC視窗中僅留下TaiwanExtent圖層

  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image13.png)

2.  將地圖縮放至TaiwanExtent圖層範圍

  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image14.png)

3.  將TaiwanExtent圖層邊框與填充色設為透明

  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image15.png)

4.  儲存地圖，本文將地圖文件檔取名為NLSC\_Basemap.mxd

#### 《5》 發佈地圖快取服務

1.  新增ArcGIS for Server連線，需要Publish以上的權限

  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image16.png)

2.  上方工具列中，點選File > Share As > Service

  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image17.png)

3.  選擇`Publish Service`，點選`下一步`

  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image18.png)

4.  選擇稍早建立的ArcGIS Server連線，並輸入此次要發佈的服務名稱。此名稱建議使用英文，本文使用`NLSC_Basemap`作為此服務名稱。然後點選下一步。

  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image19.png)

5.  選擇GIS服務要放在哪一個目錄內，本文將放在Basemap目錄內。然後點選Continue。

  ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image20.png)

6.  **設定Caching選項**

    A.  左側視窗中，選擇 `Caching`
    B.  右側視窗中，選擇 `Using tiles from a cache`
    C.  快取圖層定義檔設成 `ArcGIS Online/Bing Maps/Google Maps`
    D.  設定要產生的圖磚層數
    E.  選擇手動產生圖磚

    ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image21.png)

7.  **設定Caching > `Advanced Settings`選項**

    A.  由於國土測繪中心所給定的圖片為jpg格式，所以此處將圖片格式設定為jpeg
    B.  點選`Advanced`按鈕，開啟進階設定

    ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image22.png)
    
    C.  由於國土測繪中心使用每一個圖磚以一張圖片的方式，儲存在資料夾中，故此處將圖磚儲存方式設定為`EXPLODED`。
    
    ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image23.png)
    
    D.  完成Caching設定後，在Service Editor中點選`Analyze`按鈕，檢查服務設定上是否有錯誤或需要改進的地方。

    ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image24.png)
    
    ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image25.png)
    
    E.  如果沒有出現Error，則在Service Editor中，點選`Publish`按鈕發佈服務
    
    ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image26.png)
    
    F.  發佈過程中，出現要將TaiwanExtent這筆資料複製到主機上，點選`OK`繼續發佈過程
    
    ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image27.png)
    
    G.  出現服務發佈成功對話視窗，點選`OK`完成服務發佈。
    
    ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image28.png)

#### 《6》 複製圖磚檔案到ArcGIS Server主機上

1.  連線到ArcGIS Server主機

2.  預設情況下，在`C:\\arcgisserver\\directories\\arcgiscache`中，會找到剛才發佈的快取服務存放圖磚的資料夾位置。

    ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image29.png)

3.  點開此服務資料夾至Layers資料夾內，會看到如下圖的資料夾結構。

    ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image30.png)

4.  將從國土測繪中心網站下載的圖磚檔案，複製到`_alllayers`資料夾內即可。

    ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image31.png)

5.  從瀏覽器上瀏覽服務，即可看到通用版地圖。

    ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/03/image32.png)

## 四、 使用方法：透過ArcMap瀏覽電子地圖

#### 《1》 建立ArcGIS Raster Dataset資料夾結構

1.  下載圖磚定義檔[conf.cdi](https://drive.google.com/open?id=1sYqZG7zAz0TeG3brK7dHLuQpyx25oD5Y)與[Conf.xml](https://drive.google.com/file/d/1wmQRCnEzHaw0I2Ch5jPUNdlMoo0XSqby/view?usp=sharing)
2.  建立一個名稱為`Layers`的資料夾
3.  將`conf.cdi`與`Conf.xml`複製到Layers目錄內
4.  在Layers目錄中，建立一個名為 `_alllayers` 的資料夾
5.  把下載來的通用版電子地圖L0 ~ L15的資料夾移動到`_alllayers`資料夾內
6.  目前Layers資料夾目錄內容應該如下圖所示

    ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/04/image1.png)

#### 《2》 開啟ArcMap瀏覽地圖

1.  開啟ArcMap
2.  在Catalog視窗中，連線存放Layers資料夾的根目錄，此時會看到Layers為一個Raster Dataset格式

    ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/04/image2.png)

3.  將Layers拖曳至Table of Content視窗中，ArcMap會呈現地圖內容。
    **不過目前地圖框縮放比例與圖磚裁切比例不符，因此圖層在顯示上會產生模糊的情況。**

    ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/04/image3.png)

4.  **調整第圖框的縮放比例，讓圖層可以使用正確比例顯示。**

    A.  點選比例尺下拉選單，選擇`Customize The List…`
    
    ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/04/image4.png)
    
    B.  點選`Delete All`刪除現有顯示比例
    
    ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/04/image5.png)
    
    C.  點選`Load ArcGIS Online/Bing Maps/Google Maps`載入ArcGIS Online底圖圖磚比例

    ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/04/image6.png)
    
    D.  將`Only display these scales when zooming`打勾，並按`確定`
    
    ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/04/image7.png)
    
    E.  現在通用版電子地圖會清楚地呈現囉！
    
    ![](/how-to/media/ArcGIS/ArcGIS-透過ArcGIS使用通用版電子地圖ArcGIS封裝檔/04/image8.png)