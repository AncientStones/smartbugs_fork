# SmartBugs Wild - Analysis Fork

This is a fork of [SmartBugs Wild](https://github.com/smartbugs/smartbugs-wild) used as the dataset layer of an ongoing research project on automated DeFi smart contract vulnerability detection. No changes were made to the original SmartBugs codebase. The fork exists to keep the analysis work self-contained while the research is active.

The full pipeline and findings will be made available upon publication.

---

## Why this dataset

SmartBugs Wild contains 47,587 Solidity contracts scraped from Ethereum mainnet. Unlike the SmartBugs Curated benchmark, which is small, hand-annotated, and designed for tool validation, the Wild dataset reflects the actual distribution of vulnerability patterns in production-deployed contracts. That distinction matters for training a generative model: the goal is to learn what real vulnerable code looks like at scale, not what a carefully selected benchmark says it looks like.

---

## What was done

All contracts were analysed using two independent security tools via the SmartBugs framework, one specialised for arithmetic vulnerabilities and one providing broader symbolic execution coverage across multiple SWC identifiers. Results were parsed to structured JSON, combined, and deduplicated into a single analysis CSV.

---

## Key findings

**Vulnerability prevalence**

After deduplication, 39,277 contracts had at least one completed analysis. Of those, 54.8% carry at least one active vulnerability flag across the tools used. The vulnerable majority is consistent with the known state of early Ethereum contract development, where arithmetic overflow was endemic before Solidity 0.8.x introduced checked arithmetic by default.

**Symbolic execution coverage**

One of the two tools completed successfully on only 18.5% of contracts due to the computational cost of symbolic execution on complex real-world contracts. This is a meaningful finding in its own right: coverage rates on production mainnet contracts are substantially lower than what benchmark results suggest, and treating a missing result as equivalent to a clean result corrupts any downstream model that uses cross-tool consensus as a signal.

**Vulnerability combination patterns**

The 21,516 vulnerable contracts produce only 140 unique vulnerability combination patterns across all SWC dimensions analysed. This is a hard ceiling on what any model trained purely on historical mainnet data can learn about the DeFi attack surface. The long tail of multi-vulnerability combinations, particularly compound chains involving interactions between vulnerability classes, is absent from the historical record not because those combinations cannot exist in deployed contracts, but because they have not appeared yet.

---

## Status

Active. Results and methodology will be published in full upon completion.
