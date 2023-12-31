# 日本防衛省資料｜報導者Data Team

2023.10.25 更新

本資料集由報導者數據小組爬取[日本防衛省統合幕僚監部新聞稿](https://www.mod.go.jp/js/press/)整理而成，用於報導者專題[【圖解】解放軍如何進逼第一島鏈：台海衝突下牽動的美日軍事布局](https://github.com/data-reporter/PLA_Path_Database/tree/main/Taiwan#:~:text=%E3%80%90%E5%9C%96%E8%A7%A3%E3%80%91%E8%A7%A3%E6%94%BE%E8%BB%8D%E5%A6%82%E4%BD%95%E9%80%B2%E9%80%BC%E7%AC%AC%E4%B8%80%E5%B3%B6%E9%8F%88%EF%BC%9A%E5%8F%B0%E6%B5%B7%E8%A1%9D%E7%AA%81%E4%B8%8B%E7%89%BD%E5%8B%95%E7%9A%84%E7%BE%8E%E6%97%A5%E8%BB%8D%E4%BA%8B%E5%B8%83%E5%B1%80)。數據詳細處理過程可見[Medium](https://medium.com/twreporter/13b10f9a1c81)。

資料範圍：2022/08/01至2023/08/31

這裡的檔案包含：
- **jp_data_cleaned.csv**: 包含所有我們爬梳的報告，將軌跡圖資化的成果。
- **jp_data_cleaned.geojson**: 檔案內容與csv一致，但更便於使用者匯入GIS軟體。
- **Files_PLA_Flight**: 包含與共機活動有關的原始報告pdf檔，以及經《報導者》批量轉存的地圖png檔。
- **Files_PLA_Ship**: 同上，為共艦活動報告資料。
- **JP_Map**: 可透過儀表板探索資料。


## 欄位意義：
- **order**: 單純序號，不建議視為時序先後處理
- **type**: 地理圖徵為單一線段（LineString）或多條線段集合（MultiLineString）；需注意的是，因應內部呈現需要，《報導者》將所有幾何圖形皆改以「線段」方式儲存，取代了所有的多邊形（Polygon）。
- **src**: 餵入Figma進行描圖作業時，採用的圖片版本檔名
- **country**: 包含china, russia, both。本報導及資料集僅聚焦解放軍動向，未將俄國動向軌跡化，惟包含中國及俄國聯合軍演資料；會有both類別也是考量原始報告並未加以細分。
- **version**: 分為new和old。防衛省可能在新報告中，連帶標記日前公布過的軌跡，因此軌跡會重複描圖。如果欲去除重複，僅選擇new即可。需要特別注意的是，在處理遼寧艦及山東艦太平洋遠訓資料時，日方會連日更新資料，但前後軌跡位置可能出現差異，團隊因此將最後一次公布的各日軌跡視為new，其他較早公布的資料，皆以old來認定。因此使用者只要使用new篩選器，便可取得最終版本的軌跡。
- **category**: 軌跡圖形屬於箭頭（arrow）, 雙箭頭（bidirectional-arrow）, 橢圓（ellipse）, 圖組（group）。軌跡的文字框可能對應至一個或多個圖形，如果多個圖形共用一個文字內容，我們就會用group註記。
- **id_num**: 產製過程中，我們在Figma內命名圖層時使用的序號，結合對照表後可勾稽出具體內容。
- **id_content**: 經勾稽的內容，已從日文翻譯為中文。
- **group_detail**: 上述category如果屬於group，便會於此處詳述圖形特徵。如果有-stroke後綴，代表該原始圖案並非「填滿」狀況而只有「邊框」。如果圖形不是group類型，這裡就會是空值。
- **shape**: 綜合上述category及group_detail，描述該圖徵圖形。
- **data**: 區分資料類別為船艦（ship）或軍機（flight）。
- **unique_labels**: 該軌跡對應的機型或艦型，經過《報導者》翻譯，可能同時包含多種機艦。
- **file_name**: 活動報告的pdf檔案名稱。《報導者》基本上沿用防衛省的命名方式（如p20220801_02.pdf），惟少數人工補充資料為自行命名，我們會加上c（customized）的前綴。
- **first_page_content**: 原始pdf報告第一頁的內容（即活動概述），方便使用者理解資訊。
- **urls**: 原始報告的超連結，方便查證用。
- **if_宮古海峽**: 軌跡是否通過宮古海峽，經《報導者》GIS分析判斷。
- **if_遼寧艦**: 是否屬於2022年12月遼寧艦太平洋遠訓資料。
- **if_山東艦**: 是否屬於2023年4月遼寧艦太平洋遠訓資料。


註：解放軍動向基本上可從上述新聞稿連結取得，但部分資料（如測量艦進入領海事件）則會公布在[「お知らせ」頁面](https://www.mod.go.jp/j/press/news/index.html)中。

若對資料有任何建議或疑問，可寄信至報導者Data小組信箱：data@twreporter.org


