# 國防部共機軌跡資料｜報導者Data Team
2024.09.23 更新

本資料集由報導者數據小組爬取<a href="https://www.mnd.gov.tw/PublishTable.aspx?Types=%E5%8D%B3%E6%99%82%E8%BB%8D%E4%BA%8B%E5%8B%95%E6%85%8B&title=%E5%9C%8B%E9%98%B2%E6%B6%88%E6%81%AF">國防部即時軍事動態頁面</a>整理而成，用於報導者專題<a href="https://www.mnd.gov.tw/PublishTable.aspx?Types=%E5%8D%B3%E6%99%82%E8%BB%8D%E4%BA%8B%E5%8B%95%E6%85%8B&title=%E5%9C%8B%E9%98%B2%E6%B6%88%E6%81%AF](https://www.twreporter.org/a/taiwanyuji-first-island-chain-military-movement-multimedia)https://www.twreporter.org/a/taiwanyuji-first-island-chain-military-movement-multimedia">【圖解】解放軍如何進逼第一島鏈：台海衝突下牽動的美日軍事布局</a>。數據詳細處理過程可見[Medium](https://medium.com/twreporter/13b10f9a1c81)。

- 資料範圍：2022/08/01至2024/07/31

以3個時期分類每日共機軌跡（地理圖資檔）資料：
- Daily_Geojson_20220801-20230915：《報導者》2023年10月島鏈專題出刊時使用之資料集；2024年9月修正錯誤；內文亂碼對應aircraft_zh_type.csv；檔名為：民國年-月份-日期（1911+YYY -MM -DD）。
- Daily_Geojson_20230918-20240115：截至2024年1月15日改版前資料集
- Daily_Geojson_20240116-20240731：2024年1月16日改版以後之資料集，更新至2024年7月31日。
    - 改版說明：2024年1月16日起，國防部不再公布各機型之航機，改以活動範圍多邊形註記。
    - 欄位說明：
        - category：
            - polygon_#each 代表官方公布的共機活動範圍（多邊形）恰可對應一句資訊
            - polygon_#multi 代表一個封閉多邊形，對應兩句以上資訊
            - polygon_#separate 為《報導者》自行以海峽中線附近為界，將多邊形圖資拆開，使一個多邊形僅對應一句資訊
            - 分析時建議 #multi 與 #separate 應擇一，避免重複繪製
            - ballon代表為空飄氣球
            - distance：代表共機／空飄氣球與台灣本島之距離多少浬；若為distance資料，將註記參照點（distance_ref_location）如基隆、鵝鑾鼻等地；距離標的（distance_target）區分是針對氣球還是共機

其他：
- aircraft_zh_type：本資料處理初期出現中文編碼轉換問題，因此製作中文對照表將資料復原。原始資料出現部分機型名稱不一致的狀況，本表也可用於參照。
- Files_PLA_Flight：
    - （1）包含國防部原版地圖（Original_Images），收錄日期範圍為2020/09/18至2024/01/15，其中2022/08/05前的地圖最初是儲存在pdf檔中，報導者已將其轉為jpg檔。
    - （2）Original_Images_version_2收錄2024/01/16國防部改版後之示意圖。
    - （3）我們也提供經後製處理地圖（Processed_Images），包含切除邊界、右上角加上日期戳記、尺寸統一等；收錄範圍為2022/08/01-2023/09/15
    - （4）需注意的是，資料夾包含2020年9月至2024年1月15日所有圖檔，但本專案僅將一部分資料轉換為地理圖資（2022/07/31以前未轉換）。


註1：此處資料僅限國防部釋出的軌跡圖資，部分共機共艦無逾越海峽中線及西南空域，因此未納入本資料集。<br>
註2：2022年12月18日6時至19日6時，共機曾逾越中線及進入台灣周邊空域，惟<a href="https://www.mnd.gov.tw/Publish.aspx?p=80819">官方</a>未提供圖檔，故本資料集未收錄相關軌跡。

若對資料有任何建議或疑問，可寄信至報導者Data小組信箱：data@twreporter.org
