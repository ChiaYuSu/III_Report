<h1>{case}</h1>
- 查詢案例：{caseName}

---

<h2>特徵 1 – 熱度</h2>
<h3>特徵說明</h3>

- 根據現有案例的觀察可得出真實資訊與錯誤資訊之間具有不同的傳播特性。多數真實資訊案例在最大傳播量的月份結束後，後續月份的傳播量較少有再次出現高峰的情況；而多數錯誤資訊案例在最大傳播量的月份結束後，後續仍有一個以上的月份傳播量會再次出現高峰的情況，故依照此觀察現象設計特徵的計算公式

<h3>風險值計算方式</h3>

- 將有最多節點的月份設為基準月（星號），基準月的節點數量乘上 25% 作為臨界線（紅線），當單月節點數量（基準月除外）的數值超過臨界線，列為高風險；若無任何單月節點數量（基準月除外）超過臨界線，則列為低風險

<h3>風險值定義</h3>

- 高風險：任一節點高於臨界線（基準月除外）
- 低風險：所有節點皆低於臨界線（基準月除外）

<h3>熱度圖</h3>

- X 軸：案例傳播期間（以<b>一個月</b>作為間隔）
- Y 軸：節點數量
<div class="embed-responsive embed-responsive-16by9">
  <iframe
    class="embed-responsive-item"
    src="{feature1}"
    style="border: 0"
  ></iframe>
</div>

<h3>熱度分析</h3>
{quantity1}

<h3>風險值評估</h3>
<div class="alert" role="alert" style="background-color: #{cfbg1}; color: #{cfft1}">
  <h4 class="alert-heading" style="font-size: 18pt; font-weight: bold">{rf1_1} risk!</h4>
  <p>{cf1}</p>
</div>

---

<h2>特徵 2 – 時間跨度</h2>
<h3>特徵說明</h3>

- 根據現有案例的傳播圖觀察可得出真實資訊與錯誤資訊之間具有不同的傳播特性。在多數真實資訊案例中顯示，有被轉發的貼文通常於發佈後的三天之內就會出現被轉發的紀錄；而在多數錯誤資訊案例中，則出現有部分被轉發的貼文在三天之內無任何人進行轉發的動作，三天之後才有被轉發的紀錄，故依照此觀察現象設計特徵的計算方式

<h3>風險值計算方式</h3>

- 單一節點於 3 天之內未有任何上層連接節點，而 3 天之後卻出現上層連接節點；當案例中有一節點出現上述情形，則判斷為高風險

<h3>風險值定義</h3>

- 高風險：圖表中出現任一紅線與紅點
- 低風險：圖表中皆為藍線及藍點  

<h3>傳播圖</h3>

- X 軸：案例傳播期間
- Y 軸：層數
<div class="embed-responsive embed-responsive-16by9">
  <iframe
    class="embed-responsive-item"
    src="{feature2_1}"
    style="border: 0"
  ></iframe>
</div>

<h3>時間跨度大</h3>
{feature2_2}

<h3>風險值評估</h3>
<div class="alert" role="alert" style="background-color: #{cfbg2}; color: #{cfft2}">
  <h4 class="alert-heading" style="font-size: 18pt; font-weight: bold">{rf2_1} risk!</h4>
  <p>{cf2}</p>
</div>

---

<h2>特徵 3 – 白名單與查核驗證</h2>
<h3>特徵說明</h3>

- 此項特徵以社會認知的角度進行實驗。基於大眾對台灣主流媒體的信任所設置的白名單，紀錄各大主流媒體的 Facebook 主頁及網站頁面的域名，當資訊來源為主流媒體，該資訊可信度增加，列進「安全因素」當中。另外也利用台灣事實查核中心（TFC）與 MyGoPen 兩大查核網站為識別依據，當出現有關兩大查核網站網站、連結與字詞，則列進「風險因素」當中；利用貼文的評論內容衡量了大眾對於資訊是否存疑，當評論中出現存疑的詞彙也會列進「風險因素」當中

<h3>風險值計算方式</h3>

- <b>安全因素</b>與<b>風險因素</b>所得之分數進行相抵
    - 安全因素：將各大主流媒體的 Facebook URL 及網頁 URL 紀錄於白名單中，若爬蟲的原始資料出現白名單的資訊，會依照出現的類型列進「安全因素」當中並計次數，以下為「安全因素」的三種類型
        - Match URL
        - Match `related_link`
        - Match `author_id`
    - 風險因素：以台灣事實查核中心（TFC）與 MyGoPen 兩大查核網站為識別依據，若單篇案例的爬蟲原始資料出現事實查核機構的資訊，或是出現多數民眾認為消息不實所發表的評論，則該案例有風險是虛假消息。依照出現的類型列進「風險因素」當中並計次數，以下為「風險因素」的三種類型
        - Match URL
        - Match `body` of the article
        - Match `body` of the comment

<h3>風險值定義</h3>

- 高風險：安全因素 - 風險因素 < 0
- 中風險：0 ≤ 安全因素 - 風險因素 < 4
- 低風險：安全因素 - 風險因素 ≥ 4

<h3>安全因素</h3>
{feature3_1}

<h3>風險因素</h3>
{feature3_2}

<h3>風險值評估</h3>
<div class="alert" role="alert" style="background-color: #{cfbg3}; color: #{cfft3}">
  <h4 class="alert-heading" style="font-size: 18pt; font-weight: bold">{rf3_1} risk!</h4>
  <p>{cf3}</p>
</div>

---

<h2>特徵 4 – 意圖語意判別</h2>
<h3>特徵說明</h3>

- 在網路中的不實新聞及消息，除了標題會使用較聳動的字詞，還可能在文章一開始或結尾加上要求轉發及分享等語句，誘使不實內容能夠更大範圍的擴散出去

<h3>風險值計算方式</h3>

- 在網路中的錯誤訊息除了標題會使用較聳動的字詞，還可能在文章一開始或結尾加上要求轉發及分享等語句。利用案例的爬蟲原始資料將內容出現類似要求轉發、轉傳或分享等意圖的語句加以計數，作為權衡可能為錯誤訊息的風險依據之一

<h3>風險值定義</h3>

- 高風險：意圖語句總數 ≥ 10
- 中風險：3 ≤ 意圖語句總數 < 10
- 低風險：意圖語句總數 < 3

<h3>分享內容包含高風險字詞</h3>
{feature4_1}

<h3>風險值評估</h3>
<div class="alert" role="alert" style="background-color: #{cfbg4}; color: #{cfft4}">
  <h4 class="alert-heading" style="font-size: 18pt; font-weight: bold">{rf4_1} risk!</h4>
  <p>{cf4}</p>
</div>

---

<h2>特徵 5 – 首次貼文與首次留言的時間差 </h2>
<h3>特徵說明</h3>

- 正常情況下的新聞會由主流媒體所發佈，傳播的初期就會有最大的聲量，可觀察到社群平台上發佈留言與分享的時間會較於集中。因此推論當案例為錯誤訊息時，首次發文與首次留言的時隔會較長

<h3>風險值計算方式</h3>

- 正常情況下的新聞會由主流媒體所發佈，傳播的初期就會有最大的聲量，進而可觀察到社群平台上發佈留言與分享的時間會較於集中。因此推論當案例為錯誤訊息時，首次留言與首次分享的時隔會較長

<h3>風險值定義</h3>

- 高風險：時間差 > 60 分鐘
- 中風險：30 分鐘 ≤ 時間差 ≤ 60 分鐘
- 低風險：時間差 < 30 分鐘

<h3>時間差</h3>
{feature5_1}

<h3>風險值評估</h3>
<div class="alert" role="alert" style="background-color: #{cfbg5}; color: #{cfft5}">
  <h4 class="alert-heading" style="font-size: 18pt; font-weight: bold">{rf5_1} risk!</h4>
  <p>{cf5}</p>
</div>

---

<h2>特徵 6 – 貼文平均傳播時間</h2>
<h3>特徵說明</h3>

- 正常情況下的新聞由主流媒體所發佈，可發現討論度大多集中於傳播初期，貼文之間的時間間隔短且密集，因此推論錯誤訊息的貼文之間的時間間隔可能拉得較長且分散

<h3>風險值計算方式</h3>

- 貼文平均傳播時間 = Σ 兩個貼文之間的時間差 ÷ 時間差個數

<h3>風險值定義</h3>

- 高風險：平均傳播時間 > 5 小時
- 中風險：2 小時 ≤ 平均傳播時間 ≤ 5 小時
- 低風險：平均傳播時間 < 2 小時




<h3>時間差</h3>
{feature6_1}

<h3>風險值評估</h3>
<div class="alert" role="alert" style="background-color: #{cfbg6}; color: #{cfft6}">
  <h4 class="alert-heading" style="font-size: 18pt; font-weight: bold">{rf6_1} risk!</h4>
  <p>{cf6}</p>
</div>

---

<h2>特徵 7 – 首次貼文與最大分享量貼文的時間差</h2>
<h3>特徵說明</h3>

- 主流媒體的首次發文通常就代表著擁有最大的分享量，資訊的源頭也同時是最大分享量的來源者；或是當資訊被其他主流媒體所分享，因流量被分散導致擁有最大分享量的發文改為其他主流媒體，但因為新聞的即時性，兩者間的發佈時間不會相隔過久。錯誤資訊傳播的源頭不見得是可靠且擁有較高觸及率的，可能滿足特定因素時才會被大量分享，因此有首次發文與最大分享量發文的時間相隔較大的現象

<h3>風險值計算方式</h3>

-  利用案例的爬蟲原始資料，取出首次貼文的時間及最大分享量貼文的時間，皆以 UnixTimeStamp 的格式表示，單位為秒，相抵銷為兩者的時間差

<h3>風險值定義</h3>

- 高風險：時間差 ≥ 30 小時
- 中風險：時間差 = 0
- 低風險：時間差 < 30 小時

<h3>時間差</h3>
{feature7_1}

<h3>風險值評估</h3>
<div class="alert" role="alert" style="background-color: #{cfbg7}; color: #{cfft7}">
  <h4 class="alert-heading" style="font-size: 18pt; font-weight: bold">{rf7_1} risk!</h4>
  <p>{cf7}</p>
</div>

---

<h2>結論</h2>
<div class="alert" role="alert" style="background-color: #{cfbg8}; color: #{cfft8}">
  <h4 class="alert-heading" style="font-size: 18pt; font-weight: bold">{rf8_1} risk!</h4>
  <p>所以綜上特徵分析結果，{case2} 為{risk}風險。</p>
  <hr style="height:1px; border:none; border-top: 1px solid #{cfhr8}">
  <p>最終分數 - {value}</p>
</div>