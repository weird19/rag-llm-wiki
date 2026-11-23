# LLM Wiki 整體驗收

日期：2026-11-22（Asia/Taipei）

**結論：修正後通過。** 現有證據可支撐下列 9 頁初學者簡報；文件切分策略比較留待補證。本次驗收使用清冊中的五份本機原件，簡報大綱是後續製作建議。

## 實際執行的來源與結構檢查

以 pdftotext 抽取每份 PDF 的各頁。核對首頁標題和版本、來源頁的 metadata、清冊網址與取得日期、原件路徑及「已 Ingest」狀態。五份 PDF 均為唯讀，SHA-256 均與入庫日誌相同。

| 來源頁 | 清冊 ID | arXiv 版本 | PDF 頁數 | 引用它的概念頁 | 已定位的證據區塊 |
|---|---|---|---:|---:|---:|
| [S01](../wiki/sources/S01.md) | S001-v4 | 2005.11401v4 | 19 | 5 | 5 |
| [S02](../wiki/sources/S02.md) | S002-v3 | 2004.04906v3 | 13 | 4 | 5 |
| [S03](../wiki/sources/S03.md) | S003-v3 | 2307.03172v3 | 18 | 3 | 4 |
| [S04](../wiki/sources/S04.md) | S004-v2 | 2309.15217v2 | 8 | 3 | 5 |
| [S05](../wiki/sources/S05.md) | S005-v1 | 2310.11511v1 | 30 | 3 | 6 |

- **機械式 Lint**：最終複驗通過 18 份 Markdown 的 263 條本機連結，其中 116 條指向引用錨點。引用代號、概念 metadata 與清冊一致。10 個知識頁均有索引及其他知識頁連入，五個概念頁標題互異。檢查範圍為本機 Markdown 與 PDF。
- **語意檢查**：實讀五個概念頁的主題與範圍，未發現重複概念頁。查對 25 個來源證據區塊的原文位置，另對下列主要主張查驗數字、方法及適用條件。有效連結只表示可以到達目標，主張是否有原文支持由此項判定。
- **範圍確認**：原件仍為五篇，驗收暫存文字已清除，`slides/` 為空。已執行項目在複驗後無未通過項，Chunking 比較為明列的證據缺口。

## 重要主張抽查

| 主張 | 原文查核 | 結果與範圍 |
|---|---|---|
| 原始 RAG 的檢索與生成分工 | [S01 §2.2–2.3，頁 3](../wiki/sources/S01.md#evidence-02)、[§2.1](../wiki/sources/S01.md#evidence-03)、[S02 §3.1，頁 2–3](../wiki/sources/S02.md#evidence-02) | 通過。DPR 以雙編碼器及內積取回候選，S01 以預訓練 DPR 初始化檢索器，BART 負責條件生成。RAG-Token 使用由輸入取得的同一組候選。 |
| 原始 RAG 的生成分數 | [S01 §4.2 表 2，頁 6](../wiki/sources/S01.md#evidence-05) | 通過。Open MS-MARCO NLG 的 ROUGE-L 為 RAG-Sequence 40.8、BART 38.2。這是該任務的文字生成分數。 |
| DPR 與 BM25 的 Top-20 比較 | [S02 §5.1 表 2，頁 5](../wiki/sources/S02.md#evidence-04) | 修正說明後通過。單資料集 DPR 與 BM25 在 Natural Questions 為 78.4%／59.1%，在 SQuAD 為 63.2%／68.8%。以題目為分母，且比較結果隨資料集而變。 |
| 找到證據後仍可能答錯 | [S03 §2.1 圖 3](../wiki/sources/S03.md#evidence-01)、[§2.3 圖 5](../wiki/sources/S03.md#evidence-02)、[§3.2 圖 7](../wiki/sources/S03.md#evidence-03)、[§5 圖 11](../wiki/sources/S03.md#evidence-04) | 通過。受控問答始終提供含答案的文件，位置仍影響所測模型。鍵值查找有達滿分的模型。開放域案例的作答正確率比檢索召回率更早趨緩。各結論依所測任務及模型解讀。 |
| Ragas 的三項指標及驗證結果 | [S04 §3 式 1](../wiki/sources/S04.md#evidence-03)、[式 2](../wiki/sources/S04.md#evidence-04)、[§4–5 表 1](../wiki/sources/S04.md#evidence-05) | 通過。v2 定義與 Wiki 相符。0.95、0.78、0.70 分別是 WikiEval 上三項指標與人工成對偏好的一致率。 |
| Self-RAG 的觸發與續寫選擇 | [S05 §3.1 表 1、§3.3 式 3–4](../wiki/sources/S05.md#evidence-04)、[附錄 A.3，頁 19](../wiki/sources/S05.md#evidence-03)、[附錄 C.2 表 6，頁 21、24](../wiki/sources/S05.md#evidence-06) | 修正摘要的引用範圍後通過。門檻使用 Yes 與 No 的機率。反思標記參與候選選擇，附錄表 6 有誤判例。 |
| Self-RAG 的引用成效 | [S05 §4.3 與 §5.1 表 2，頁 7–8](../wiki/sources/S05.md#evidence-05) | 通過。ASQA 中 13B 的引用 precision／recall 為 70.3／71.3，Ret-ChatGPT 為 65.1／76.6，兩者各有一項較高。 |

## 問題、修正與複驗

| 修正前 | 原因 | 修改與複驗 |
|---|---|---|
| RAG 基本原理以「§2.1–2.3」連到 S01 的檢索與生成證據區塊。 | §2.1 的機率整合另有專屬錨點。 | 該句收窄至 §2.2–2.3，檢索時機的兩半各自引 S01、S05。回查頁 3 及 §3.1 演算法 1。 |
| S05 摘要以全 §3（頁 3–6）連到訓練證據區塊。 | 該區塊涵蓋 §3.1–3.2，推論評分位於 §3.3。 | 分別連到訓練、推論及實驗設定的證據。核對原文頁 3–7 與錨點。 |
| 評估頁將 Top-20 命中率寫作「前 20 段是否至少有一段包含標註答案」。 | 這句描述單題是否命中，整批指標還需要分母。 | 加上命中題數除以總題數，回查 S02 §5.1 表 2 及來源頁。 |
| 原文定位腳本按擷取文字的順序找 S03 圖 7 和 S04 式 2，並要求 S05 PDF 首頁標題字元完全一致。 | 多欄和數式的文字抽取會改變順序；S05 的小型大寫字與逗號不同於清冊標題排版。 | 對圖和式改查同頁範圍中的標記，對 PDF 標題比對先正規化大小寫、逗號及空白。重新執行，五份原件、25 個證據區塊均通過。另將初次檔名萬用字元搜尋改用 rg 的 `-g` 篩選。 |

## Cross-source Query 實測

1. **RAG 如何分工？DPR 的角色？** 檢索器找候選段落，生成器依原始問題及段落生成。S01 以預訓練 DPR 初始化檢索器，從維基百科向量索引取前 K 段，BART 計算條件輸出。DPR 分別編碼問題與段落，以內積排序。[RAG 基本原理](../wiki/concepts/rag-basics.md) · [DPR](../wiki/concepts/dense-passage-retrieval.md) · [S01 §2.2–2.3](../wiki/sources/S01.md#evidence-02) · [S02 §3.1](../wiki/sources/S02.md#evidence-02)
2. **已取回正確證據，為什麼仍答錯？** 先確認證據是否保留在實際模型輸入中。若證據已在輸入，模型仍可能用不好。S03 只變動答案文件的位置，所測多文件問答設定常見中段表現較差。檢索失敗則是候選中缺少足夠證據，應分開診斷。[上下文中的證據位置](../wiki/concepts/context-position.md) · [S01 §2.2–2.3](../wiki/sources/S01.md#evidence-02) · [S02 §5.1 表 2](../wiki/sources/S02.md#evidence-04) · [S03 §2.1](../wiki/sources/S03.md#evidence-01) · [S03 §2.3 圖 5](../wiki/sources/S03.md#evidence-02)
3. **如何分別評估三種品質？** 用 S02 Top-20 檢查含答案段落的命中題比例，也可用 S04 Context Relevance 看輸入中必要句子的比例。Faithfulness 查上下文支持的主張比例，Answer Relevance 則從答案反推問題，比對這些問題與原問題的平均嵌入餘弦相似度。切題和忠於上下文各自回答不同的品質問題。[RAG 評估](../wiki/concepts/rag-evaluation.md) · [S02 §5.1](../wiki/sources/S02.md#evidence-04) · [S04 §3 Context Relevance](../wiki/sources/S04.md#evidence-04) · [Faithfulness](../wiki/sources/S04.md#evidence-02) · [Answer Relevance](../wiki/sources/S04.md#evidence-03)
4. **一般 RAG 和 Self-RAG 如何比較？** S01 的原始 RAG 先取候選再整合生成機率。S05 在每生成一段前用 `Retrieve` 或機率門檻決定是否查詢，對各取回段落分別生成續寫，再用 `IsRel`、`IsSup`、`IsUse` 與生成機率選擇候選。這是推論內的自評；S04 的 Faithfulness 用於評估已生成的答案。[Self-RAG](../wiki/concepts/self-rag.md) · [RAG 評估](../wiki/concepts/rag-evaluation.md) · [S01 §2.1](../wiki/sources/S01.md#evidence-03) · [S05 §3.1、§3.3](../wiki/sources/S05.md#evidence-04) · [附錄 A.3](../wiki/sources/S05.md#evidence-03) · [S04 §3](../wiki/sources/S04.md#evidence-02)
5. **Chunking 策略的證據夠嗎？** 不足。Wiki 記錄 S02 使用不重疊的 100 詞區塊，但沒有可用來比較不同長度、重疊或切分方式的對照結果。S03 變動的是文件位置與數量。文件切分策略的效益保留為待補證。[DPR](../wiki/concepts/dense-passage-retrieval.md) · [上下文中的證據位置](../wiki/concepts/context-position.md) · [S02 §4.1、§5.1](../wiki/sources/S02.md#evidence-04) · [S03 §2.1 圖 3–4](../wiki/sources/S03.md#evidence-01)

## 初學者 HTML 簡報規劃

建議用「作業何時截止？」貫穿 9 頁。示例以教學情境呈現，表中來源支撐的是觀念或研究結果。

| 頁 | 主題與教學目標 | 主要知識點 | Wiki 概念頁 | 來源 |
|---|---|---|---|---|
| 1 | 為什麼要檢索？說出 RAG 的目的 | 課程公告提供模型可使用的當次上下文 | [RAG 基本原理](../wiki/concepts/rag-basics.md) | S01 §1 |
| 2 | 看懂 RAG 資料流 | 問題 → 檢索候選 → 利用段落生成答案 | [RAG 基本原理](../wiki/concepts/rag-basics.md) | S01 §2.2–2.3 |
| 3 | 認識向量檢索 | 問題向量、段落向量、內積與前 K 段 | [DPR](../wiki/concepts/dense-passage-retrieval.md) | S02 §3.1、S01 §2.2 |
| 4 | 判斷資料是否取回 | Top-20 以題目為單位。100 詞是 S02 的實驗設定，切分策略優劣待補證 | [DPR](../wiki/concepts/dense-passage-retrieval.md) | S02 §4.1、§5.1 |
| 5 | 找到仍答錯時能分段診斷 | 未取回、未送入、已送入但未有效使用；展示移動證據位置的受控設計 | [上下文中的證據位置](../wiki/concepts/context-position.md) | S01 §2、S03 §2.1、§2.3 |
| 6 | 分開量測檢索與回答 | Top-20、Context Relevance、Faithfulness、Answer Relevance 各量測什麼 | [RAG 評估](../wiki/concepts/rag-evaluation.md) | S02 §5.1、S04 §3 |
| 7 | 練習檢查一則回答 | 用示例核對主張是否受公告支持、是否答到問題；評審一致率的意義 | [RAG 評估](../wiki/concepts/rag-evaluation.md) | S04 §3、§5 表 1 |
| 8 | 認識按需檢索 | 原始 RAG 的檢索時機、Self-RAG 的 Retrieve 門檻及反思標記 | [Self-RAG](../wiki/concepts/self-rag.md) | S01 §2.1、S05 §3.1、§3.3 |
| 9 | 用一條查核路徑總結 | 用「候選 → 實際輸入 → 回答主張」定位問題，示範從 Wiki 回查原文 | [上下文中的證據位置](../wiki/concepts/context-position.md) · [RAG 評估](../wiki/concepts/rag-evaluation.md) | S02 §5.1、S03 §2.3、S04 §3 |

**下一階段可使用此大綱生成離線 HTML。** 瀏覽器呈現、導覽、離線使用及投影片引用抽查屬於生成階段的驗收項目。可保留清冊的五篇來源，文件切分策略比較維持待補證。
