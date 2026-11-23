---
title: "稠密段落檢索（DPR）"
type: concept
source_ids:
  - "S001-v4"
  - "S002-v3"
last_checked: "2026-11-22"
---

# 稠密段落檢索（DPR）

## 定義

Dense Passage Retrieval（DPR）是一種稠密檢索方法。它用兩個編碼器，分別把問題和文件段落轉成向量，再以向量內積為每個候選段落打分。[S02，§3.1，頁 2–3](../sources/S02.md#evidence-02)

## 如何運作

1. **建立索引**。先算好所有段落的向量，存入可搜尋的向量索引。[S02，§3.1，頁 2–3](../sources/S02.md#evidence-02)
2. **取回候選**。將問題轉成向量，取回分數排名前 K 的段落。[S02，§3.1，頁 2–3](../sources/S02.md#evidence-02)
3. **交給下游模型**。S02 的問答系統由閱讀器從候選段落抽取答案片段。Lewis 等人的原始 RAG 則以預訓練的 DPR 初始化檢索器，由 BART 根據輸入與檢索段落生成輸出。DPR 在這個架構中負責找段落。[S02，§6.1，頁 7](../sources/S02.md#evidence-05) [S01，§2.2–2.3，頁 3](../sources/S01.md#evidence-02)

## 限制與待查問題

比較檢索器時要看資料集和指標。S02 的單資料集 DPR 在 Natural Questions 的前 20 段命中率比 BM25 高，在 SQuAD 卻較低。這個指標只計算前 20 段有沒有包含答案的段落。整體問答表現以另一個指標評估。[S02，§5.1 與表 2，頁 5](../sources/S02.md#evidence-04) [S02，§6.2，頁 7–8](../sources/S02.md#evidence-05)

## 相關 Wiki 頁面

- [RAG 基本原理](rag-basics.md)
- [S01 · Lewis 等人的 RAG 論文](../sources/S01.md)
- [S02 · Karpukhin 等人的 DPR 論文](../sources/S02.md)
- [上下文中的證據位置](context-position.md)，接續檢查取回的段落如何影響實際作答。
- [RAG 評估](rag-evaluation.md)，比較 Top-20 命中率與上下文相關性衡量的問題。
