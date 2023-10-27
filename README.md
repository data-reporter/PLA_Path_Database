# 解放軍活動軌跡資料集 PLA_Path_Database｜報導者Data Team

2023.10.26

## 專案說明
- 本資料集由[《報導者》](https://www.twreporter.org/)數據新聞小組整理而成，原始資料取自[台灣國防部即時軍事動態頁面](https://www.mnd.gov.tw/PublishTable.aspx?Types=%E5%8D%B3%E6%99%82%E8%BB%8D%E4%BA%8B%E5%8B%95%E6%85%8B&title=%E5%9C%8B%E9%98%B2%E6%B6%88%E6%81%AF)、[日本防衛省統合幕僚監部新聞稿](https://www.mod.go.jp/js/press/)。
- 本資料使用於報導者數位專題[【圖解】解放軍如何進逼第一島鏈：台海衝突下牽動的美日軍事布局](https://www.twreporter.org/a/taiwanyuji-first-island-chain-military-movement-multimedia)。
- 數據詳細處理方法論可見[Medium技術筆記〈AI、Python與手工業，我們如何處理台灣+日本超過400張共軍軌跡圖？〉](https://medium.com/twreporter/13b10f9a1c81)

## 研究方法概述

本專案所使用的解放軍活動軌跡包含「共機」及「共艦」資料，簡要資料收集及處理方法如下：

### 一、資料收集及概述：

**台灣國防部：**
- 國防部定時監測解放軍動態，若共機「逾越海峽中線及西南空域」即會提供航跡圖，本專案圖像以有航跡資料者為準。
- 由於國防部未例行公布共艦活動軌跡，本專案共艦資料皆以日本防衛省資料為準。
- 本專案關注時任美國眾議院議長裴洛西訪台後的變化，資料抓取時間為2022年8月1日至2023年9月15日，包含共317份活動圖、992條軌跡資料（1份報告可能有數條軌跡）。

**日本防衛省：**
- 例行公布共艦及共機資料。
- 日方例行公布資料中，還包含俄國機、艦擾日軌跡，本專案並未分析俄軍部分，但包含中俄聯合軍演之解放軍資料。
- 資料抓取時間為2022年8月1日至2023年8月31日，共計22份共機資料、99份共艦資料。
 

### 二、資料前處理：

台、日官方提供資料皆為JPG圖檔或PDF文件檔，團隊須先將圖檔轉換為地理圖資檔案，以便後續分析。資料處理過程包含以下步驟：

**台灣國防部：**
- 切除圖片邊界：國防部公布之資料為JPG圖檔、不同日公布之航跡圖長寬大小不一，或比例有些微差異，但由於地圖邊界相同，《報導者》透過影像辨識技術，批量將所有航跡圖切除白邊、並統一長度及寬度，使多張地圖得以疊合。
- 透過地理資訊軟體QGIS進行「空間對位（Georeferencing）」，辨識出地圖四個端點的坐標，作為還原軌跡的參考點。
- 參考《天下雜誌》，將所有圖檔匯入繪圖兼介面設計軟體Figma中，在各圖層中逐一人工描繪各段軌跡。
- 標示日期、機型及數量，並批量下載為SVG向量圖檔。
- 透過Python，以上述四端點坐標為標準、依照EPSG:3857座標系統（Web Mercator）還原軌跡坐標值，並以EPSG:4326（WGS84）儲存經緯度，以此將多筆svg檔轉換為地理圖資檔；同時，團隊整合該軌跡的日期、機型等屬性資料，以此進行GIS分析。

**日本防衛省：**
- 取出軌跡地圖：日本防衛省原始提供資料為pdf檔，我們透過Python偵測關鍵字「行動概要」，由此找到地圖軌跡的目標頁面，並儲存為PNG檔，特殊個案則另外人工處理。
- 挑出擁有「相同邊界」的地圖：由於日本幅員廣大，其公布的地圖比例尺不一，涵蓋的邊界範圍也不同，《報導者》先將占一定比例、擁有同樣邊界的資料歸於一類，採用上述台灣處理方法轉換為GeoJSON，並翻譯為中文。
- 客製化空間對位：剩餘之邊界不一的圖檔仍占一定數量，《報導者》則個別以地圖中的經緯線交點，或特定地形點位為參考點，循上述方法將之轉換為GeoJSON。
 

### 三、資料呈現：

將軌跡轉換為GeoJSON地理格式後，團隊即可將之繪製於地圖軟體上，並再以人工方式比對原圖、確保其位置無偏移狀況。

《報導者》基本上延續原圖標示方法，一條直線可能包含多架共機或多艘共艦。
日方記錄及公布軌跡時，可能包含最新資料及舊資料（如：同一艘船艦位置變化），《報導者》呈現時僅繪製一次，避免重複。
 

### 四、資料限制：

缺乏台灣海峽船艦軌跡：受限於可取得資料限制，日方公布船艦資料基本上以日本海域、台灣東部海域為主，台灣海峽船艦出沒軌跡未有完整可取用資料集。

由於軌跡是從官方圖檔復刻而來，各重繪環節都會使資料精準度打折，地圖相對適合從「宏觀」的小比例尺觀之，並不適合過度拉近為大比例尺進行解讀（位置可能會存在誤差）。

## 聯絡我們

若對資料有任何建議或疑問，可寄信至報導者Data小組信箱：**data@twreporter.org**

*《報導者》是台灣第一個由公益基金會成立的網路媒體，秉持深度、開放、非營利的精神，致力於公共領域調查報導，與社會共同打造多元進步的媒體環境。*
