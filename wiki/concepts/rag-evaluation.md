---
title: "RAG 評估"
type: concept
source_ids:
  - "S001-v4"
  - "S002-v3"
  - "S003-v3"
  - "S004-v2"
  - "S005-v1"
last_checked: "2026-11-22"
---

# RAG 評估

## 定義

評估 RAG 時，可以分開問三件事：給模型的資料是否聚焦、回答的主張是否有證據、回答是否解決使用者的問題。以下是 S04 的 arXiv v2 論文定義。[S04，§3，頁 2–4](../sources/S04.md#evidence-01)

| 指標 | 檢查什麼 | 論文的計分方法 |
|---|---|---|
| Context Relevance（上下文相關性） | 給模型的資料有多少是回答所需的 | 評估模型選出的關鍵句數 ÷ 上下文總句數。[S04，§3，頁 3–4，式 2](../sources/S04.md#evidence-04) |
| Faithfulness（忠實度） | 回答的各項主張能否由所給資料推得 | 評估模型判為有支持的主張數 ÷ 答案總主張數。[S04，§3，頁 3](../sources/S04.md#evidence-02) |
| Answer Relevance（答案相關性） | 回答是否切題 | 從答案反向產生多個問題，取它們與原問題的嵌入餘弦相似度平均。[S04，§3，頁 3，式 1](../sources/S04.md#evidence-03) |

## 如何診斷

1. **先查檢索和組裝**。S02 對每題檢查前 20 段是否至少有一段包含標註答案，再用命中的題目數除以總題數。S04 的 Context Relevance 回答「所給上下文的句子有多少是回答所需的」。只取回一段含答案的資料，也可能同時帶入大量冗餘。[S02，§5.1 與表 2，頁 5](../sources/S02.md#evidence-04) [S04，§3，頁 3–4](../sources/S04.md#evidence-04)
2. **再查回答**。逐項對照回答主張與模型實際收到的證據，另查回答是否切題。S03 的多文件實驗保留答案文件並改變其位置，所測條件下模型表現仍會變動。[S04，§3，頁 3](../sources/S04.md#evidence-02) [S04，§3，頁 3](../sources/S04.md#evidence-03) [S03，§2.3 與圖 5，頁 5](../sources/S03.md#evidence-02)

## 適用條件

忠實度衡量對所給資料的支撐關係；若資料本身有誤，仍需查核來源事實。答案相關性衡量切題。S01 的 ROUGE-L 是另一種生成評分，報告的是特定 Open MS-MARCO NLG 評估結果。[S04，§3，頁 3](../sources/S04.md#evidence-02) [S04，§3，頁 3](../sources/S04.md#evidence-03) [S01，§4.2 與表 2，頁 6](../sources/S01.md#evidence-05)

S04 的驗證比較 WikiEval 的成對判斷與人工偏好。三項分數所衡量的對象不同，表 1 的一致率也有其資料集與評審條件。[S04，§4–5 與表 1，頁 4–5](../sources/S04.md#evidence-05)

Self-RAG 在推論過程中用模型自己預測的反思標記為續寫候選評分，例如以 `IsSup` 估計候選是否獲段落支持。Ragas 的 Faithfulness 則取已生成的回答，拆成主張並逐項判斷上下文支撐。前者用於解碼選擇，後者用於量測回答品質。[S05，§3.3，頁 6](../sources/S05.md#evidence-04) [S04，§3，頁 3](../sources/S04.md#evidence-02)

## 相關 Wiki 頁面

- [RAG 基本原理](rag-basics.md)
- [稠密段落檢索（DPR）](dense-passage-retrieval.md)
- [上下文中的證據位置](context-position.md)
- [S04 · Ragas](../sources/S04.md)
- [Self-RAG](self-rag.md)
