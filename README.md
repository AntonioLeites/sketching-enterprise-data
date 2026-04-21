
# sketching-enterprise-data

**Applying probabilistic data structures and streaming algorithms to enterprise data problems.**

---

## Why this repository exists

Enterprise systems — ERPs, MES, IoT platforms, data lakes — produce torrents of events. Sensor readings in a factory, material movements in a warehouse, transactions in finance, queries against a data warehouse. A modest industrial plant can easily generate millions of records per day; a large logistics operation generates billions.

The default answer to this volume is *"store everything, query later"*. Data lakes, columnar databases, partitioned tables, indexes. These work, and they work well — until they don't. Some questions are genuinely easier to answer by **not** storing everything.

This repository is a personal exploration of that second path. It collects notebooks, notes and small experiments on **probabilistic data structures** and **streaming algorithms** — Count-Min Sketch, HyperLogLog, Bloom filters, Space-Saving, MinHash, and their extensions into graphs and knowledge representation — applied to the kinds of problems that actually show up in enterprise settings.

The bias is toward usefulness. Each notebook tries to answer two questions honestly:

1. What can this structure do that a `GROUP BY` cannot?
2. At what scale does it start to matter?

Sometimes the answer to the second question is *"at a scale larger than your company will ever reach"*, in which case the recommendation is: use `GROUP BY`. That honesty is part of the point.

---

## Philosophy

Probabilistic data structures share a single insight:

> *You do not need to remember every event. You need to answer questions about those events.*

Those are different problems, and the second one often has a much smaller and more elegant solution. The price is that answers are approximate rather than exact — with known, provable error bounds. For most real-world applications, the trade-off is wildly favorable: a 99.9%-correct answer in a kilobyte is a better deal than an exact answer in a gigabyte you do not have.

The same philosophy has recently been extended into quantum computing (see Zhao et al., *arXiv:2604.07639*, April 2026 — *"quantum oracle sketching"*), suggesting that this way of thinking about data is not just a technical trick but a durable way of approaching scale.

---

## Structure

The repository is organized in three conceptual layers, which roughly correspond to increasing sophistication and decreasing certainty:

### 1. Fundamentals

Didactic notebooks introducing each structure with small, traceable examples that can be reproduced by hand, followed by scale-up experiments on synthetic data.

- `01-count-min-sketch-basics.ipynb` — the classic CMS for frequency queries; companion to the [https://www.linkedin.com/pulse/how-count-things-you-cant-afford-remember-antonio-leites-4ksce/](#).
- *(planned)* `02-hyperloglog-basics.ipynb` — counting distinct items.
- *(planned)* `03-bloom-filters-basics.ipynb` — set membership.
- *(planned)* `04-space-saving-topk.ipynb` — tracking top-K without full counts.

### 2. Enterprise applications

Notebooks that take plausible enterprise scenarios and evaluate when sketching genuinely wins, when it breaks even with classical methods, and when it loses.

- *(planned)* `cms-vs-groupby-benchmark.ipynb` — at what data scale does CMS start to pay off?
- *(planned)* `process-signature-monitoring.ipynb` — detecting plant-wide operating patterns that precede quality issues.
- *(planned)* `streaming-topk-with-decay.ipynb` — heavy hitters with sliding windows and exponential decay.

### 3. Graph sketching

The most exploratory layer: applying streaming and sketching techniques to knowledge graphs and relational data. This is where enterprise data tends to live in its natural form, and where mature classical algorithms struggle with scale.

- *(planned)* `graph-sketches-for-knowledge-graphs.ipynb` — Count-Min over triples, HyperLogLog per predicate.
- *(planned)* `minhash-lsh-for-entity-resolution.ipynb` — finding similar entities without pairwise comparison.
- *(planned)* `streaming-embeddings.ipynb` — incremental node embeddings from event streams.

---

## How to read this repository

Each notebook is designed to be self-contained. Clone the repo, install the minimal dependencies listed in each notebook's first cell, and run top to bottom. No hidden state, no external services.

The notebooks are written in a style closer to a technical notebook than to a software package: code is interleaved with explanation, trade-offs are discussed openly, and when a technique does not actually help, the notebook says so.

---

## References and further reading

Foundational papers on the structures explored here:

- Cormode, G., & Muthukrishnan, S. (2005). *An improved data stream summary: the Count-Min sketch and its applications.* Journal of Algorithms, 55(1), 58–75.
- Flajolet, P., Fusy, É., Gandouet, O., & Meunier, F. (2007). *HyperLogLog: the analysis of a near-optimal cardinality estimation algorithm.* Discrete Mathematics and Theoretical Computer Science.
- Bloom, B. H. (1970). *Space/time trade-offs in hash coding with allowable errors.* Communications of the ACM, 13(7), 422–426.
- Metwally, A., Agrawal, D., & El Abbadi, A. (2005). *Efficient computation of frequent and top-k elements in data streams.* ICDT.
- Broder, A. Z. (1997). *On the resemblance and containment of documents.* Compression and Complexity of Sequences.

Extensions into quantum computing:

- Zhao, H. et al. (2026). *Exponential quantum advantage in processing massive classical data.* arXiv:2604.07639.

Broader context on streaming and sketching:

- Muthukrishnan, S. (2005). *Data streams: algorithms and applications.* Foundations and Trends in Theoretical Computer Science.
- Woodruff, D. P. (2014). *Sketching as a tool for numerical linear algebra.* Foundations and Trends in Theoretical Computer Science.

---

## About

This is a personal repository maintained by **Antonio Leites**. The content here reflects personal exploration and does not represent official positions or product offerings.

Feedback, corrections and suggestions are welcome via issues or direct message on [LinkedIn](https://www.linkedin.com/in/antonioleites/).

---

## License

- **Code** (Python in notebooks, scripts): MIT License — see [LICENSE](LICENSE)
- **Content** (explanations, diagrams, written material): Creative Commons Attribution 4.0 International (CC-BY-4.0) — see [LICENSE-content.md](LICENSE-content.md)

Use freely. When reusing the content in publications, courses, or articles, please attribute to Antonio Leites with a link to this repository.

