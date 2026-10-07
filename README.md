# ISS Lab

Undergraduate Intern at ISS Lab, Korea University (26.08 ~) — Network Security & AI Security.

## Security Paper Review

Analysis notes on recent IEEE S&P / USENIX Security papers, written to build the habit of empirically validating protocol- and system-level security vulnerabilities. Each deck follows the same structure: background → attack (or defense) structure → threat model → experiments and evaluation → existing defenses → limitations → related papers or open questions I want to explore next.

| Date | Paper | Venue | Focus |
| --- | --- | --- | --- |
| 26.08 | [DNS Cache Poisoning Like it's 2006](./Security%20Paper%20Review/analysis_dns_cache_poisoning_2026.pdf) | USENIX Security '26 | Recovering BIND 9's Xoshiro128** PRNG state from observable TXID/RRset-order leakage to defeat both TXID and UDP-port randomization at once |
| 26.09 | [Adversarial Hubness in Multi-Modal Retrieval](./Security%20Paper%20Review/analysis_adversarial_hubness_2026.pdf) | IEEE S&P '26 | Intentionally engineering hubness in a multi-modal embedding space so that a single optimized image/audio input is retrieved by thousands of otherwise unrelated queries |
| 26.09 | [Opossum Attack: Application Layer Desynchronization using Opportunistic TLS](./Security%20Paper%20Review/analysis_opossum_attack_2026.pdf) | USENIX Security '26 | Exploiting the coexistence of implicit and opportunistic TLS on a single server — using only timing and message-order manipulation, with no cryptographic break — to desynchronize requests and responses |
| 26.10 | [Who Taught the Lie? Responsibility Attribution for Poisoned Knowledge in RAG](./Security%20Paper%20Review/analysis_Who_Taught_the_Lie.pdf) | IEEE S&P '26 | A black-box defense (RAGOrigin) that traces the poisoned texts responsible for a RAG misgeneration using only the user-reported (question, incorrect response) — narrowing the attribution scope over similarity-ranked segments, then combining retrieval and generation signals (ES/SC/GC) into a responsibility score split into poisoned/benign by K-means |

## Independent Follow-up: From Reading to Reproduction

Reading [Adversarial Hubness in Multi-Modal Retrieval](./Security%20Paper%20Review/analysis_adversarial_hubness_2026.pdf) motivated me to reproduce and extend its core attack on my own — an independent personal project, separate from ISS Lab's assigned research. Working across CLIP, OpenCLIP, and ImageBind (8 models total), I reproduced the paper's central attack (the adversarial hub), compared a self-built detector against the official implementation of a follow-up detection paper, and independently tested an extended hypothesis the original paper did not examine — whether representational similarity between models predicts transfer-attack success.

The full write-up and results are kept in a separate repository:

**[dhsama51/adversarial-hubness-reproduction](https://github.com/dhsama51/adversarial-hubness-reproduction)**

Similarly, while analyzing [Who Taught the Lie?](./Security%20Paper%20Review/analysis_Who_Taught_the_Lie.pdf), I found an edge case in the termination condition of RAGOrigin's attribution scope narrowing (Eq. 4 / Algorithm 1) — it has no iteration cap and can terminate early before a deeper poison is ever scanned. I verified this directly with a lightweight reproduction (SQuAD, Qwen2.5-1.5B, single consumer GPU):

**[dhsama51/ragorigin-reproduction](https://github.com/dhsama51/ragorigin-reproduction)**
