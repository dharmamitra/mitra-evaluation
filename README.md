# MITRA-zh-eval

Evaluation data and per-text scores for:

> Sebastian Nehrdich, Avery Chen, Marcus Bingenheimer, Lu Huang, Rouying Tang,
> Xiang Wei, Leijie Zhu, Kurt Keutzer. 2025. *MITRA-zh-eval: Using a Buddhist
> Chinese Language Evaluation Dataset to Assess Machine Translation and
> Evaluation Metrics.* NLP4DH 2025, pp. 129–137.
> https://aclanthology.org/2025.nlp4dh-1.12

Buddhist Chinese → English sentence pairs from 35 texts of the Taishō canon.
Each pair is aligned to a published human translation. The Chinese comes from
CBETA.

## Contents

| Path | Description |
|---|---|
| `data/zh-en/texts/<text_id>.tsv` | One file per text: `zh<TAB>en`, no header, in text order |
| `data/zh-en/zh2en_with_ids.tsv` | All 2,709 pairs in one file with header `text_id, row_in_text, zh, en` |
| `data/zh-en/texts.tsv` | One row per text: title, year of the reference translation, row count, and whether the text is in Table 1 and in the reported results |
| `results/per_text_*.tsv` | Per-text, per-system averages behind Figures 2–3 (GEMBA, chrF, BLEU, BERTScore, BLEURT) |

`data/zh-en/zh2en_with_ids.tsv` has the same rows, in the same order, as
`v2/evaluation/zh-en/zh2en.tsv` in
[mitra-parallel](https://github.com/dharmamitra/mitra-parallel), with text IDs
added.

## Which texts the paper used

The data contain 35 texts and 2,709 pairs. The paper uses two different
subsets:

| Subset | Texts | Pairs |
|---|---|---|
| All released data | 35 | 2,709 |
| Table 1 of the paper (the "2,662 datapoints, 32 texts") | 32 | 2,662 |
| **Reported results** (Figures 2–3, §5) | 32 | 2,593 |

The reported results take Table 1's texts, drop **T30n1568** (十二門論, 96
pairs) and add **T31n1614** (大乘百法明門論, 27 pairs), which §5.1 discusses.
Table 1 lists T30n1568 and not T31n1614. The table's printed "Total 2689" is
2,662 + 27, i.e. it counts T31n1614. T31n1610 (佛性論, 8 pairs) and T32n1660
(菩提資糧論, 12 pairs) are released but used in neither subset. The
`in_table1` and `in_reported_results` columns of `texts.tsv` mark each subset.

## Note on the retrieval (RAG) setup

The "+En" retrieval store for the RAG systems was built from Buddhist
Chinese–English parallel data that predates this benchmark. It was **not**
deduplicated against the benchmark. In our stored retrieval logs, the exact
reference translation of a test sentence appeared among its 10 retrieved
examples for 31 of the 2,593 pairs in the reported results (1.2%). 20 of these
are in T14n0515. Allowing near-duplicates (≥ 0.9 string similarity), the count
is about 1.5%. For T30n1568, which is not in the reported results, the exact
reference was retrieved for 35 of its 96 pairs. RAG scores for the affected
texts, T14n0515 above all, should be read with this in mind. Later Dharmamitra
corpora (mitra-parallel v2 and newer) are decontaminated against this
benchmark.

## License

TODO
