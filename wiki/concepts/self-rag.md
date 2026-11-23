---
title: "Self-RAG"
type: concept
source_ids:
  - "S001-v4"
  - "S004-v2"
  - "S005-v1"
last_checked: "2026-11-22"
---

# Self-RAG

## 定義

Self-RAG 是一種進階 RAG 設計。它訓練語言模型在生成文字時也預測反思標記，以決定是否需要檢索，並評估候選段落與生成內容。[S05，§3.1–3.2，頁 3–5](../sources/S05.md#evidence-01)

## 如何運作

1. **決定何時檢索**。每一生成段開始前，模型根據原始輸入及先前生成文字預測 `Retrieve`。若這一步不需要新查詢，模型可繼續生成。[S05，§3.1 演算法 1，頁 4](../sources/S05.md#evidence-02) 可依標記觸發，也可將 `Yes` 相對於 `Yes` 與 `No` 的機率設門檻。[S05，§3.3，頁 6；附錄 A.3，頁 19](../sources/S05.md#evidence-03)
2. **產生並評估候選**。觸發檢索後，模型針對每份取回段落分別產生續寫候選。用 `IsRel` 評估資料相關性、`IsSup` 評估段落對續寫的支撐、`IsUse` 評估回答有用性，再將生成機率和加權評論分數用於選擇續寫。[S05，§3.1 表 1、§3.3 式 3–4，頁 4、6](../sources/S05.md#evidence-04)

## 與其他做法的關係

S01 的原始 RAG 從輸入先取出前 K 個候選，再在整段輸出或 token 層級整合候選段落的生成機率。S05 在實驗中還比較了先取文件、把文件接到提示中的標準基線。這兩種對照說明 RAG 有不同做法，Self-RAG 加入的是生成途中可再檢索及用反思評分選擇續寫的設計。[S01，§2.1，頁 3](../sources/S01.md#evidence-03) [S05，§4.2，頁 7](../sources/S05.md#evidence-05) [S05，§3.3，頁 6](../sources/S05.md#evidence-04)

Self-RAG 的 `IsSup` 是模型用來選續寫的訊號。S04 的 Faithfulness 則是評估已生成答案中有多少主張獲上下文支持。兩者都關心證據支撐，使用時機和計算方式不同。[S05，§3.3，頁 6](../sources/S05.md#evidence-04) [S04，§3，頁 3](../sources/S04.md#evidence-02)

## 適用條件

論文報告的效果取決於所測模型、檢索來源與評估指標。例如在 ASQA，Self-RAG 13B 的引用 precision 高於 Ret-ChatGPT，recall 則較低。[S05，§5.1 表 2，頁 8](../sources/S05.md#evidence-05) 附錄也記錄模型誤判段落相關性與支撐性的例子。[S05，附錄 C.2、表 6，頁 21、24](../sources/S05.md#evidence-06)

## 相關 Wiki 頁面

- [RAG 基本原理](rag-basics.md)
- [RAG 評估](rag-evaluation.md)
- [S05 · Self-RAG](../sources/S05.md)
