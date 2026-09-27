# ICU 每日查房

加護病房每床每日查房檢核工具：整合 SCCM **ICU Liberation（ABCDEF）bundle** 與 **VAP／CLABSI／CAUTI 組合式照護**，並自動計算月品質指標（組合式照護完整率、導管使用率、感染密度），可對應醫策會與院內感管的監測指標。

> ⚠️ **僅供臨床流程輔助與品質監測，不取代臨床判斷。** 組合式照護項目請依院內感管與醫策會最新版本調整。

## 功能

| 功能 | 說明 |
|---|---|
| 床位列 | 每床顏色標示當日狀態：完整、未填完、有未執行、未記錄或空床 |
| 管路設定 | 勾選呼吸器、持續鎮靜、中心導管（含今日新置放）、導尿管，只顯示適用的組合式照護 |
| 沿用前一天 | 新的一天自動沿用前次（14 天內）的在床與管路設定 |
| ABCDEF | 疼痛（CPOT／BPS／NRS）、SAT＋SBT、RASS 目標、CAM-ICU／ICDSC、早期活動、家屬參與 |
| VAP 組合式照護 | 疾管署／台灣感染管制學會 5 項；「每日中止鎮靜」「每日評估拔管」自動連動 B1、B2 |
| CLABSI | 維護組合 4 項；今日新置放時另顯示置放組合 4 項 |
| CAUTI | 導尿管照護組合 5 項 |
| 每日必查 | 營養、血糖、壓力性潰瘍預防、VTE 預防、抗生素、其他管路、皮膚、照護目標、轉出評估 |
| 不適用自動判斷 | 例如未使用呼吸器時 SBT 自動標為不適用 |
| 查房摘要 | 一鍵複製當床摘要，可貼到病歷 |
| 單位總覽 | 當日全床表格，點選任一列即進入該床 |
| 月品質指標 | 組合式照護完整率（全有或全無）、導管使用率、感染密度（‰）、資料完整度 |
| 匯出 | 本月資料可複製或下載成 CSV（含 BOM，Excel 可直接開啟） |
| 備份 | 複製全部資料，貼到另一台裝置匯入 |

## 品質指標計算方式

| 指標 | 分子 | 分母 |
|---|---|---|
| ABCDEF 完整率 | 6 個元素都完成或不適用的人日 | 住院人日 |
| VAP／CLABSI／CAUTI 組合式照護完整率 | 所有適用項目都完成的導管使用日 | 導管使用日 |
| 中心導管置放組合完整率 | 4 項都完成的置放次數 | 置放次數 |
| 導管使用率 | 導管使用日 | 住院人日 |
| 感染密度（‰） | 勾選「今日新診斷」的例數 × 1000 | 導管使用日 |

- 未填完視為不完整。
- 感染個案請依院內感管收案定義判定後再勾選。
- 指標名稱與定義請與醫策會 TCPI 及院內感管的定義核對。

## 使用方式

直接用瀏覽器開啟 `index.html` 即可，不需安裝或建置。

線上版（GitHub Pages）：https://yht5582-source.github.io/ICU-round/

## 部署到 GitHub Pages

1. 將 `index.html`、`README.md`、`.nojekyll` 推上 GitHub repo（免費帳號需為 Public）。
2. 到 **Settings → Pages**，Source 選 **Deploy from a branch**，Branch 選 `main`、資料夾選 `/ (root)`。
3. 約 1 分鐘後即可從上方網址開啟。

## 在地化設定

| 項目 | 位置 |
|---|---|
| 單位名稱、床號 | 網頁「單位總覽 → 單位設定與備份」 |
| ABCDEF 項目 | `<script>` 內 `const ABCDEF` |
| VAP／CLABSI／CAUTI 項目 | `const BUNDLES` |
| 中心導管置放組合 | `const INSERT` |
| 每日必查 | `const DAILY` |
| 配色 | `<style>` 開頭 `:root` 的色彩變數 |

每個項目的格式為 `{id:'v1', t:'項目名稱', h:'說明'}`。`when` 設定適用條件，`link` 設定連動其他項目。修改 `id` 會讓舊紀錄對不上，新增項目請用新的 `id`。

若院內網路封鎖外部連線，可刪除 Google Fonts 的三行 `<link>`，會自動改用系統字型。

## 資料與隱私

- 所有資料只存在該瀏覽器的 `localStorage`，不會上傳；不同電腦、不同瀏覽器的資料各自獨立。
- 多人共用同一份資料需要後端資料庫，本版本不支援；可用「備份」功能在裝置之間搬移資料。
- 清除瀏覽器資料會刪除紀錄，請定期匯出 CSV。
- 只記錄床號，請勿輸入姓名、病歷號等可識別個人資料。

## 注意事項

- 台灣 VAP 組合式照護原為 chlorhexidine 口腔照護；SHEA/IDSA/APIC 2022 改建議刷牙、不建議常規使用 chlorhexidine，請依院內規範。
- 若網頁會依病人數據給出具體處置建議，正式用於臨床前請確認是否屬於 TFDA 醫療器材軟體的管理範圍。

## 依據

1. SCCM ICU Liberation Bundle（A–F）；Devlin JW, et al. Clinical Practice Guidelines for the Prevention and Management of Pain, Agitation/Sedation, Delirium, Immobility, and Sleep Disruption in Adult Patients in the ICU (PADIS). *Crit Care Med* 2018;46:e825–e873，及 2025 focused update。
2. Schmidt GA, et al. Liberation from mechanical ventilation in critically ill adults (ATS/ACCP). *Am J Respir Crit Care Med* 2017;195:115–119。
3. 衛生福利部疾病管制署／台灣感染管制學會：侵入性醫療處置組合式照護（VAP、中心導管、導尿管）。
4. SHEA/IDSA/APIC Compendium of Strategies to Prevent Healthcare-Associated Infections in Acute-Care Hospitals: 2022 Updates（VAP/VAE、CLABSI、CAUTI）。*Infect Control Hosp Epidemiol* 2022–2023。
5. Compher C, et al. ASPEN/SCCM guideline for nutrition support in the adult critically ill patient, 2022；Singer P, et al. ESPEN practical and partially revised guideline: clinical nutrition in the ICU, 2023。
6. SCCM guidelines for glycemic control in critically ill adults, 2024；SCCM/ASHP guideline for the prevention of stress-related GI bleeding in critically ill adults, 2024；ASH 2018 guidelines for VTE prophylaxis in hospitalized medical patients。

## 授權

請依使用單位規定自行選擇授權方式（例如 MIT）。
