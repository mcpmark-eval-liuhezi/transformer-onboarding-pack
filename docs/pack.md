# New Student Starter Pack: Paper Deep-Read & Beijing Field Trip

This pack covers the two halves of the new grad student's first month: the set reading
(**Attention Is All You Need**) and the **Beijing field trip**. All facts below were pulled
from the live sources (arXiv LaTeX API and Google Maps services) at pack-creation time.

---

## Part 1 — The Paper: "Attention Is All You Need" (arXiv 1706.03762)

### Section Outline

The paper is organized into the following sections:

1. Introduction
2. Background
3. Model Architecture
4. Why Self-Attention
5. Training
6. Results
7. Conclusion
8. Attention Visualizations

### Key Machine-Translation Results

These come from the **Results** section (subsection "Machine Translation"), Table
`tab:wmt-results`, for the Transformer (big) model:

| Task | BLEU | Notes |
|------|------|-------|
| WMT 2014 English-to-German | **28.4** | New state of the art, beating the best previously reported models (including ensembles) by more than 2.0 BLEU. Trained 3.5 days on 8 P100 GPUs. |
| WMT 2014 English-to-French | **41.8** | Per the abstract and the results table, a new single-model state-of-the-art BLEU, after training for 3.5 days on eight GPUs. Note: the body text of the Results section in this arXiv LaTeX version cites 41.0. |

For reference, the Transformer **base** model scores 27.3 EN-DE and 38.1 EN-FR.

### Architecture Note

Unlike the recurrent or convolutional sequence transduction models it replaced, the
Transformer retains the familiar encoder–decoder form but builds **both** stacks entirely
from stacked self-attention and point-wise fully connected feed-forward layers (with
residual connections and layer normalization) — no recurrence and no convolutions. Because
self-attention connects every pair of positions with a constant-length path, computation is
far more parallelizable, so the model trains dramatically faster while achieving higher
translation quality.

### Architecture Section Highlights (Section 3, "Model Architecture")

- **Encoder**: a stack of `N = 6` identical layers. Each layer has two sub-layers: a
  multi-head self-attention mechanism, and a simple position-wise fully connected
  feed-forward network. Residual connections around both sub-layers are followed by layer
  normalization: `LayerNorm(x + Sublayer(x))`. All sub-layers (and the embedding layers)
  produce outputs of dimension `d_model = 512`.
- **Decoder**: also a stack of `N = 6` identical layers. In addition to the two encoder-style
  sub-layers, each decoder layer inserts a third sub-layer that performs multi-head attention
  over the output of the encoder stack. Self-attention in the decoder is masked to prevent
  positions from attending to subsequent positions, so predictions for position `i` depend
  only on known outputs at positions less than `i`.
- **Scaled Dot-Product Attention**:
  `Attention(Q, K, V) = softmax(QK^T / sqrt(d_k)) V`
  Queries and keys have dimension `d_k`, values have dimension `d_v`. Scaling by
  `1/sqrt(d_k)` counteracts large dot-product magnitudes that would push the softmax into
  tiny-gradient regions. Dot-product attention is preferred over additive attention because it
  can be implemented with highly optimized matrix multiplication code.

---

## Part 2 — The Beijing Field Trip

### Base Location: Central Beijing

| Field | Value |
|-------|-------|
| Geocoded coordinates | **39.904211, 116.407395** (lat, lng) |
| Place ID | **ChIJuSwU55ZS8DURiqkPryBWYrk** |
| Formatted address | Beijing, China |

The origin used for driving distances was resolved by the service to
**2 Zheng Yi Lu, Dong Cheng Qu, Bei Jing Shi, China, 100051**.

### The Three Sights

Selected as the top three results actually returned by the places search (imperial palaces,
temples, gardens) centered on Beijing's coordinates. They are *not* the classic big names —
the live search surfaced these, so these are reported as returned.

#### 1. Yuanmingyuan Park (圆明园) — "Garden of Gardens" / Old Summer Palace

| Field | Value |
|-------|-------|
| Place ID | ChIJ09grWqdW8DURTB0kM62Vn_A |
| Address | 275X+67P圆明园 Haidian District, China, 100084 |
| Coordinates | 40.0080982, 116.2982148 |
| **Elevation** | **45.24 m** |
| Rating | 4.4 |
| Phone | 010 6262 8501 |
| Website | http://www.yuanmingyuanpark.cn/ |
| Opening hours | 7:00 AM – 5:00 PM daily |
| **Driving from central Beijing** | **21.3 km, 47 mins** |

Known for the haunting Dashuifa marble ruins, lotus ponds and lake islands; reviewers describe
it as a huge park (plan 2–3 hours of walking), less crowded than the Summer Palace and more
reflective. Seniors over 60 enter free.

#### 2. Palace of Tranquil Longevity

| Field | Value |
|-------|-------|
| Place ID | ChIJWYdbk9xS8DURc0dO_XHp3ks |
| Address | WCC2+34R, Dongcheng, Beijing, China, 100006 |
| Coordinates | 39.920248, 116.400277 |
| **Elevation** | **45.37 m** |
| Rating | 4.2 |
| Website | https://www.dpm.org.cn/ (Palace Museum) |
| **Driving from central Beijing** | **2.1 km, 10 mins** |

Located inside the Forbidden City complex; historically the retirement residence of Emperor
Qianlong after his abdication. Adjacent to the Stone Drum Museum. The Qianlong-era buildings
require an additional ticket for the Treasure Gallery.

#### 3. Beijing Ming Imperial Palace

| Field | Value |
|-------|-------|
| Place ID | ChIJmVHVhhPw8DURagkEBsWvvX4 |
| Address | China, Bei Jing Shi, Chang Ping Qu, G6辅路66F7+M7M, 102200 |
| Coordinates | 40.2242236, 116.2131599 |
| **Elevation** | **76.21 m** |
| Rating | 4.5 |
| Phone | 010 6974 7257 |
| **Driving from central Beijing** | **46.6 km, 49 mins** |

⚠️ Despite the imperial-palace name, this entry actually resolves to the **Ming Wax Palace
(明皇蜡像宫) near the Ming Tombs in Changping District** — not the Forbidden City in the city
center. It is roughly an hour's drive out of central Beijing. Do not confuse it with the
Palace Museum. If you want the actual Forbidden City, that appears separately in search
results (The Palace Museum, place ID ChIJq4HNm91S8DURZGAQm-3qQ94).

---

## Summary Tables

### Headline numbers

| Item | Value |
|------|-------|
| WMT 2014 EN-DE BLEU (Transformer big) | **28.4** |
| WMT 2014 EN-FR BLEU (Transformer big) | **41.8** |
| Beijing coordinates | **39.904211, 116.407395** |
| Beijing place ID | **ChIJuSwU55ZS8DURiqkPryBWYrk** |

### Sights at a glance

| Sight | Place ID | Elevation | Driving distance | Driving time |
|-------|----------|-----------|------------------|--------------|
| Yuanmingyuan Park | ChIJ09grWqdW8DURTB0kM62Vn_A | 45.24 m | 21.3 km | 47 mins |
| Palace of Tranquil Longevity | ChIJWYdbk9xS8DURc0dO_XHp3ks | 45.37 m | 2.1 km | 10 mins |
| Beijing Ming Imperial Palace | ChIJmVHVhhPw8DURagkEBsWvvX4 | 76.21 m | 46.6 km | 49 mins |
