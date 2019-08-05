---
title: ArcMap 台灣常見座標轉換流程
date: 2019-07-26 14:11:35
categories:
- ArcGIS
- ArcMap
tags:
- 座標轉換
---

在ArcToolbox中有個 「**Create Custom Geographic Transformation**」 工具，可以提供使用者自訂座標系統轉換參數。台灣的使用者可以透過該工具自訂TWD67、TWD97、WGS84三種常見座標系統的轉換參數，設定好的轉換參數檔案(\*.gtf)預設放在以下目錄，使用者可以自行複製到其他電腦使用。

<!--more-->

**C:\\Users\\&lt;user&gt;\\AppData\\Roaming\\ESRI\\Desktop&lt;版本&gt;\\ArcToolbox \\CustomTransformations**

設定完畢之後，定義為TWD67、TWD97、WGS84座標系統的地理資料，就可以使用 「**Project**」 工具，套用設定好的轉換參數進行座標系統轉換。因此使用ArcMap進行座標轉換流程可分為以下兩大步驟：

1.使用 「Create Custom Geographic Transformation」 建立轉換公式

2.使用 「Project」 對地理資料進行座標系統轉換

以下將針對上述兩步驟進行詳述。

## 建立轉換公式

### 建立TWD67 -- TWD97 座標轉換參數

1. 在ArcToolbox中開啟 「Create Custom Geographic Transformation」 工具，工具位於**Data Management Tools** > **Projections and Transformations**底下

  ![](/how-to/media/ArcGIS/ArcMap-台灣常見座標轉換流程/image2.png)

2. 依照以下資料輸入對應的參數值，並點選 「OK」 即可建立完成

  | 參數名稱                              | 參數值               |
  |-------------------------------------  |-------------------- |
  | Geographic Transformation Name        | TWD67 -- TWD97      |
  | Input Geographic Coordinate System    | TWD_1967_TM_Taiwan  |
  | Output Geographic Coordinate System   | TWD_1997_TM_Taiwan  |
  | Method                                | Coordinate Frame    |

  【轉換參數】

  | X Axis Translation (meters)   | X軸平移量(公尺)   | 730.160                             |
  |-----------------------------  |-----------------  |------------------------------------ |
  | Y Axis Translation (meters)   | Y軸平移量(公尺)   | 346.212                             |
  | Z Axis Translation (meters)   | Z軸平移量(公尺)   | 472.186                             |
  | X Axis Rotation (seconds)     | X軸旋轉量(秒)    | 7.968009465325332199694565793688    |
  | Y Axis Rotation (seconds)     | Y軸旋轉量(秒)    | 3.5498173155125282722429064796627   |
  | Z Axis Rotation (seconds)     | Z軸旋轉量(秒)    | 0.40634166830677981965825251394163  |
  | Scale Difference (ppm)        | 尺度參數          | 0.99998180                          |

  ![](/how-to/media/ArcGIS/ArcMap-台灣常見座標轉換流程/image3.png)

### 轉換方法與參數說明

本文所提及的轉換方法是根據Help中的說明，Coordinate Frame法與台灣地區常用的Bursa-Wolf法在程式引擎當中是一樣的，所以在設定時選擇Coordinate Frame法。

  ![](/how-to/media/ArcGIS/ArcMap-台灣常見座標轉換流程/image4.png)

轉換參數則是使用史天元老師等人於**測量工程第41卷第3期**所發表的 「TWD67與TWD97大地基準轉換方法研究」 一文中所提及的七參數Bursa-Wolf基準轉換參數，並將旋轉量單位徑換算為秒（因為Create Custom Geographic Transformation工具需要輸入秒）後所得的數值。在 「TWD67與TWD97大地基準轉換方法研究」 一文中，有提到**經計算所得的七參數會有誤差，因此轉換結果也會有誤差**。

### 建立TWD97 – WGS84 座標轉換參數

1. 在ArcToolbox中開啟 「Create Custom Geographic Transformation」 工具，工具位於***Data Management Tools* > *Projections and Transformations***底下

  ![](/how-to/media/ArcGIS/ArcMap-台灣常見座標轉換流程/image2.png)

2. 依照以下資料輸入對應的參數值，並點選 「OK」 即可建立完成

  | 參數名稱                              | 參數值                   |
  |-------------------------------------  |------------------------ |
  | Geographic Transformation Name        | TWD97 -- WGS84          |
  | Input Geographic Coordinate System    | TWD_1997_TM_Taiwan      |
  | Output Geographic Coordinate System   | GCS_WGS_1984            |
  | Method                                | GEOCENTRIC_TRANSLATION  |

  【轉換參數】

  | Name                          | Value   |
  |-----------------------------  |-------  |
  | X Axis Translation (meters)   | 0       |
  | Y Axis Translation (meters)   | 0       |
  | Z Axis Translation (meters)   | 0       |

### 轉換方法與參數說明

由EPSG 7.1版資料庫中查詢得知TWD97與WGS84的轉換方式名稱為 「TWD97 to WGS84」 ，編號是 「3830」 ，使用地區為 「台灣，中華民國，近陸與近海，台灣島、澎湖（澎湖群島）島」 ，轉換精度為 「1」 公尺。

![](/how-to/media/ArcGIS/ArcMap-台灣常見座標轉換流程/image5.png)

![](/how-to/media/ArcGIS/ArcMap-台灣常見座標轉換流程/image6.png)

註記當中說明了 「近似值有正負一公尺的水準，假設TWD97近似於WGS84的話」 。資料來源為 「OGP（International Association of Oil & Gas producers，國際油氣製造業協會）。

![](/how-to/media/ArcGIS/ArcMap-台灣常見座標轉換流程/image7.png)

座標轉換方法名稱 「地理中心轉移」 。轉換參數有三個， 「X軸轉移為0」 、 「Y軸轉移為0」 、 「Z軸轉移為0」 ，且該轉換是可進行逆向轉換的。

![](/how-to/media/ArcGIS/ArcMap-台灣常見座標轉換流程/image8.png)

由以上描述內容可得，TWD97經緯度基本上等同於WGS84經緯度，因為X軸、Y軸、Z軸的平移皆為0

## 座標轉換

1. 在ArcToolbox中開啟 「Project」 工具，工具位於 ***Data Management Tools \\ Projections and Transformations*** 底下

  ![](/how-to/media/ArcGIS/ArcMap-台灣常見座標轉換流程/image9.png)

2. 只要 「Input Coordinate System」 與 「Output Coordinate System」 互為`TWD67`、`TWD97`、`WGS84`，就可以在 「Geographic Transformation」 的下拉選單中，選擇建立好的轉換公式。

  ![](/how-to/media/ArcGIS/ArcMap-台灣常見座標轉換流程/image10.png)

  ![](/how-to/media/ArcGIS/ArcMap-台灣常見座標轉換流程/image11.png)

3. 按下 「OK」 完成座標轉換

  ![](/how-to/media/ArcGIS/ArcMap-台灣常見座標轉換流程/image12.png)

### 在ArcMap中加入不同座標系統的地理資料

使用ArcMap時如果加入不同座標系統的地理資料，ArcMap一般會跳出警告訊息，如下圖。

![](/how-to/media/ArcGIS/ArcMap-台灣常見座標轉換流程/image13.png)

如果此時按下 「Transformation」 按鈕，也可以指定要使用的轉換參數

![](/how-to/media/ArcGIS/ArcMap-台灣常見座標轉換流程/image14.png)

## TWD97與TWD67轉換結果比較

當比例尺要放到很大，會發現TWD97與TWD67地理資料會有誤差。利用 「Measure」 工具量測，視地區不同，誤差約一公尺左右。

![](/how-to/media/ArcGIS/ArcMap-台灣常見座標轉換流程/image15.png)