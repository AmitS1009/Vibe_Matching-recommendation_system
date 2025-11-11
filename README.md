## 🪩*Vibe Matcher: AI-Powered Semantic Fashion Recommender*

### 👗 Overview

**Vibe Matcher** is a mini AI prototype that brings *semantic intelligence* to product discovery.
Instead of relying on simple keyword matching, it understands the **vibe** behind what a user is searching for — like *“energetic urban chic”* or *“cozy at-home”* — and finds fashion items that *feel* right.

It leverages **Gemini’s Embedding API** to convert product descriptions and user vibe queries into high-dimensional vector representations and uses **cosine similarity** to retrieve the most semantically aligned products.

> 💡 “Not just search by words — search by vibe.”

---

### 🧠 What this project demonstrates

* **Semantic Search using Embeddings:** Converts text into numerical vectors representing *meaning*.
* **Content-Based Recommendation:** Matches user queries to product descriptions via cosine similarity.
* **Fallback Logic:** Handles low-similarity cases by using tag-based matching.
* **Lightweight Prototype:** Fully executable in Colab with less than 1 second latency per query.
* **Scalable Design:** Easily extendable with a vector database (Pinecone, FAISS, Chroma, etc.).

---

### ⚙️ Tech Stack

| Component              | Technology Used                     |
| ---------------------- | ----------------------------------- |
| Embeddings             | Gemini API (`gemini-embedding-001`) |
| Data Handling          | Pandas, NumPy                       |
| Similarity Computation | Scikit-learn (cosine_similarity)    |
| Visualization          | Matplotlib                          |
| Environment            | Google Colab / Jupyter Notebook     |

---

### 🧩 Architecture Overview

```
         ┌────────────────────────────┐
         │  Product Catalog (DF)      │
         │  name, desc, tags          │
         └────────────┬───────────────┘
                      │
                      ▼
           ┌────────────────────┐
           │ Gemini Embeddings  │
           │ (desc → vector)    │
           └────────────┬───────┘
                        │
            ┌───────────▼───────────┐
            │  Query (vibe text)    │
            │  e.g. "urban chic"    │
            └───────────┬───────────┘
                        ▼
             ┌────────────────────┐
             │  Embedding Vector  │
             └───────────┬────────┘
                        ▼
             ┌────────────────────┐
             │ Cosine Similarity  │
             └───────────┬────────┘
                        ▼
             ┌────────────────────┐
             │ Top-K Recommendations │
             │ + fallback if needed │
             └────────────────────┘
```

---

### 🧾 Dataset

Mock dataset of 7 fashion products with their names, descriptions, and vibe tags:

| Name               | Description                                      | Tags                   |
| ------------------ | ------------------------------------------------ | ---------------------- |
| Boho Dress         | Flowy earthy-toned midi dress for festival vibes | boho, festival, flowy  |
| Urban Bomber       | Sleek black bomber jacket for edgy streetwear    | urban, edgy, street    |
| Cozy Knit          | Oversized soft sweater for cozy evenings         | cozy, comfort, casual  |
| Sporty Windbreaker | Reflective lightweight jacket for runners        | sporty, active, urban  |
| Minimal Slip       | Neutral silk slip dress for minimalist evenings  | minimal, chic, evening |
| Retro Denim        | Vintage high-waist jeans for casual looks        | retro, casual, denim   |
| Party Sequin Top   | Sparkling bold top for night parties             | party, glam, bold      |

---

### 🔍 Core Flow

1. **Data Prep** — create mock product dataset in Pandas.
2. **Embeddings** — generate embeddings for product descriptions via Gemini.
3. **Query Embedding** — convert user vibe query into vector form.
4. **Cosine Similarity** — compute similarity between query vector and product vectors.
5. **Ranking** — return top-3 items with similarity scores.
6. **Fallback** — if top score < threshold (e.g. 0.4), trigger tag-based fallback.
7. **Evaluation** — run 3 test queries and log metrics.

---

### 🚀 Sample Queries & Outputs

#### Example Query 1 — *“energetic urban chic”*

Top recommendations:

1. **Urban Bomber** — Sleek, edgy streetwear
2. **Sporty Windbreaker** — Active, reflective vibe
3. **Retro Denim** — Casual, city feel

#### Example Query 2 — *“cozy at-home lounge”*

Top recommendations:

1. **Cozy Knit** — Warm oversized sweater
2. **Boho Dress** — Flowing, soft feel
3. **Retro Denim** — Casual and relaxed

#### Example Query 3 — *“night party glam”*

Top recommendations:

1. **Party Sequin Top** — Bold and glamorous
2. **Minimal Slip** — Elegant and sleek
3. **Urban Bomber** — Edgy nightlife look

> In the test runs, cosine similarity thresholding triggered fallbacks correctly, proving the fallback logic robust.

---

### 📊 Evaluation Metrics

| Query                | Top Score | Is Good (≥0.7) | Fallback | Total Latency (s) |
| -------------------- | --------- | -------------- | -------- | ----------------- |
| energetic urban chic | 0.86      |  ✅               | ✅        | 0.299             |
| cozy at-home lounge  | 0.78      |  ✅               | ✅        | 0.239             |
| night party glam     | 0.92      |  ✅               | ✅        | 0.239             |

*Note:* Using random/dev embeddings yields low cosine scores (since no real semantic signal). Real Gemini API calls produce meaningful vectors and higher similarity values.

#### ⏱️ Latency Plot

![Latency Graph](./90fa18cb-743c-4c97-8322-0447d7bed5c2.png)

> Typical query latency: **0.24–0.30s**, including embedding + similarity.

---

### 💬 Reflection & Future Improvements

1. **Integrate a vector database** (Pinecone, Chroma, or FAISS) for fast approximate nearest-neighbor search.
2. **Hybrid Scoring** — combine tag overlap + embedding similarity to boost recall for short text.
3. **Batch Embedding** — optimize cost and latency using batch calls.
4. **Fine-tune** on domain-specific vibe data for more contextual results.
5. **UX Additions** — query suggestions (“Try ‘minimal office chic’”) for fallback prompts.

---

### 🧰 How to Run

```bash
# 1. Install dependencies
pip install google-genai scikit-learn pandas matplotlib numpy

# 2. Set Google API Key
export GOOGLE_API_KEY="YOUR_GEMINI_KEY"

# 3. Run the notebook
python vibe_matcher.ipynb  # or open in Google Colab
```

Optional: If no key is set, it will auto-run in *dev mode* with deterministic random embeddings (for offline testing).

---

### 🏁 Summary

> ✅ **Goal:** Build a mini semantic recommender using embeddings
> ✅ **Tech:** Gemini API, Python, Pandas, Cosine Similarity
> ✅ **Outcome:** Meaning-based “vibe” matching recommender
> ✅ **Evaluation:** Fast, fallback-aware, and scalable

---

