# 投影片來源對應表

[《RAG 是什麼？》離線簡報](../slides/rag-intro.html)以已驗收 Wiki 為技術來源。第 1–6 頁先建立概念，第 7–9 頁的課程文件、制度與模型輸出皆是虛構教學示例。

| 頁 | 教學重點 | Wiki 概念頁 | 來源與原文定位 |
|---|---|---|---|
| 1．RAG 是什麼？ | 先找相關資料，再用找到的資料幫助語言模型回答。 | [RAG 基本原理](../wiki/concepts/rag-basics.md) | [S01（S001-v4） §1、圖 1，頁 1–2](../wiki/sources/S01.md#evidence-01) |
| 2．為什麼需要 RAG？ | RAG 增加了可核對的外部依據。 | [RAG 基本原理](../wiki/concepts/rag-basics.md) | [S01（S001-v4） §1、圖 1，頁 1–2](../wiki/sources/S01.md#evidence-01)、[S01（S001-v4） §2.2–2.3，頁 3](../wiki/sources/S01.md#evidence-02) |
| 3．檢索與生成怎麼配合？ | 檢索負責找資料，生成負責用資料回答。 | [RAG 基本原理](../wiki/concepts/rag-basics.md) | [S01（S001-v4） §1、圖 1，頁 1–2](../wiki/sources/S01.md#evidence-01)、[S01（S001-v4） §2.2–2.3，頁 3](../wiki/sources/S01.md#evidence-02) |
| 4．RAG 如何運作？ | 先讓文件可被查找，提問時再檢索、生成。 | [RAG 基本原理](../wiki/concepts/rag-basics.md)、[DPR](../wiki/concepts/dense-passage-retrieval.md) | [S01（S001-v4） §2.2–2.3，頁 3](../wiki/sources/S01.md#evidence-02)、[S01（S001-v4） §2.1，頁 3](../wiki/sources/S01.md#evidence-03)、[S02（S002-v3） §3.1，頁 2–3](../wiki/sources/S02.md#evidence-02) |
| 5．相關資料是怎麼找到的？ | 把段落轉成可比較的形式，找出分數最高的候選。 | [DPR](../wiki/concepts/dense-passage-retrieval.md) | [S02（S002-v3） §3.1，頁 2–3](../wiki/sources/S02.md#evidence-02)、[S02（S002-v3） §4.1、§5.1 表 2，頁 4–5](../wiki/sources/S02.md#evidence-04) |
| 6．有外部資料，就一定會答對嗎？ | 資料可補充模型知識，答案仍取決於證據是否被找到、送入並用對。 | [RAG 基本原理](../wiki/concepts/rag-basics.md)、[上下文中的證據位置](../wiki/concepts/context-position.md) | [S01（S001-v4） §1、圖 1，頁 1–2](../wiki/sources/S01.md#evidence-01)、[S01（S001-v4） §2.2–2.3，頁 3](../wiki/sources/S01.md#evidence-02)、[S03（S003-v3） §2.1、圖 3，頁 3–4](../wiki/sources/S03.md#evidence-01)、[S03（S003-v3） §2.3、圖 5，頁 5](../wiki/sources/S03.md#evidence-02) |
| 7．看 AI 文件問答助手跑一次 | 關鍵句是回答的依據，可回到原文件核對。 | [RAG 基本原理](../wiki/concepts/rag-basics.md) | [S01（S001-v4） §2.2–2.3，頁 3](../wiki/sources/S01.md#evidence-02) |
| 8．哪些回答主張有文件支持？ | 回答切合問題之外，還要逐項確認文件是否支持。 | [RAG 評估](../wiki/concepts/rag-evaluation.md) | [S04（S004-v2） §3 忠實度，頁 3](../wiki/sources/S04.md#evidence-02) |
| 9．怎麼知道回答站得住腳？ | 先確認取回什麼，再核對模型收到什麼和回答說了什麼。 | [RAG 基本原理](../wiki/concepts/rag-basics.md)、[上下文中的證據位置](../wiki/concepts/context-position.md)、[RAG 評估](../wiki/concepts/rag-evaluation.md)、[Self-RAG](../wiki/concepts/self-rag.md) | [S01（S001-v4） §1、圖 1，頁 1–2](../wiki/sources/S01.md#evidence-01)、[S03（S003-v3） §2.3、圖 5，頁 5](../wiki/sources/S03.md#evidence-02)、[S02（S002-v3） §4.1、§5.1 表 2，頁 4–5](../wiki/sources/S02.md#evidence-04)、[S04（S004-v2） §3 忠實度，頁 3](../wiki/sources/S04.md#evidence-02)、[S04（S004-v2） §3 式 1，頁 3](../wiki/sources/S04.md#evidence-03)、[S05（S005-v1） §3.1 演算法 1，頁 4](../wiki/sources/S05.md#evidence-02)、[S05（S005-v1） §3.1 表 1、§3.3，頁 4、6](../wiki/sources/S05.md#evidence-04)、[S05（S005-v1） 附錄 C.2 表 6，頁 21、24](../wiki/sources/S05.md#evidence-06) |

第 4 頁將一般應用資料流和 S01 原始模型分開標示。第 5 頁的 Chunking 與 Embedding 只介紹基本作用與 S02 所支持的向量檢索做法；策略效果比較待補證。第 6 頁的位置效應限定 S03 的實驗條件。第 9 頁的 Self-RAG 是延伸閱讀，反思標記仍可能誤判。

## 原件與版本

| 來源代號 | 清冊版本 ID | 原件 |
|---|---|---|
| S01 | S001-v4 | [RAG PDF](https://arxiv.org/pdf/2005.11401v4) |
| S02 | S002-v3 | [DPR PDF](https://arxiv.org/pdf/2004.04906v3) |
| S03 | S003-v3 | [Lost in the Middle PDF](https://arxiv.org/pdf/2307.03172v3) |
| S04 | S004-v2 | [Ragas PDF](https://arxiv.org/pdf/2309.15217v2) |
| S05 | S005-v1 | [Self-RAG PDF](https://arxiv.org/pdf/2310.11511v1) |

保留專案目錄結構即可離線回查來源頁與對應表。論文 PDF 由 arXiv 提供，開啟時需要網路。簡報的顯示和互動所需資源都內嵌於 HTML。
