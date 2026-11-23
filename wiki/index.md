# RAG 知識庫

RAG（Retrieval-Augmented Generation，檢索增強生成）課程作業的導覽入口。

| 分類 | 頁面或待建主題 |
|---|---|
| 基本原理 | [RAG 基本原理](concepts/rag-basics.md)，從檢索到生成，以及與純參數式生成的差異。 |
| 文件準備與索引 | 文件切分策略比較待補證；[DPR](concepts/dense-passage-retrieval.md) 已介紹嵌入與索引。 |
| 檢索與重排序 | [稠密段落檢索（DPR）](concepts/dense-passage-retrieval.md)，介紹雙編碼器、檢索命中率及其在 RAG 中的角色。混合檢索與候選排序待建。 |
| 上下文與生成 | [上下文中的證據位置](concepts/context-position.md)，介紹長上下文位置效應與檢索、生成的分段診斷。證據引用與證據不足時的回答待建。 |
| 評估與故障診斷 | [RAG 評估](concepts/rag-evaluation.md)，分開評估檢索上下文、答案的證據支撐與切題程度。 |
| 進階變體 | [Self-RAG](concepts/self-rag.md)，從檢索觸發、反思標記到分段生成。 |

## 頁面導覽

- [公開來源清冊](source-catalog.md)
- [操作流程](../docs/workflow.md)
- [操作日誌](log.md)
- [整體驗收與簡報大綱](../docs/final-wiki-validation.md)
- [維護規範](../AGENTS.md)

## 來源頁

- [S01 · Lewis 等人的 RAG 論文](sources/S01.md)，記錄原始架構與可查核的實驗證據。
- [S02 · Karpukhin 等人的 DPR 論文](sources/S02.md)，記錄稠密檢索方法、BM25 比較與抽取式問答架構。
- [S03 · Liu 等人的 Lost in the Middle 論文](sources/S03.md)，記錄受控位置實驗與開放域問答案例。
- [S04 · Es 等人的 Ragas 論文](sources/S04.md)，記錄三項無參考答案評估指標及 WikiEval 結果。
- [S05 · Asai 等人的 Self-RAG 論文](sources/S05.md)，記錄按需檢索、候選選擇與實驗結果。
