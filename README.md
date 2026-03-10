# Hindi Fluency Experiment — Team Brainiacs

**IIIT Hyderabad | BRSM Course Project**

| Member | Roll No |
|--------|---------|
| Pranav Vyas | 2025202015 |
| Yogendra Patel | 2025201098 |
| Rinkesh Verma | 2025201070 |

---

## What this project is about

We're studying how Hindi speakers search through their mental vocabulary. When someone tries to list as many animals as possible in 60 seconds, they don't just randomly pull words out — they go through mental "patches" (farm animals, then jungle animals, then pets) and switch between them. This project tries to measure and understand that process.

This project investigates how native and non-native Hindi speakers organize and retrieve words from their mental lexicon. By combining Verbal Fluency Task (VFT) timing data with Spatial Arrangement Method (SpAM) coordinates, we visualize and statistically measure the "semantic density" and retrieval speed across different linguistic groups.

The two main tasks we used:
- **VFT (Verbal Fluency Task):** Participants had 60 seconds per category to type every Hindi word they could think of. We recorded each word and the exact time it was typed.
- **SpAM (Spatial Arrangement Method):** After the VFT, participants dragged those same words around a canvas, placing similar words close together and different ones far apart.

Together, these give us both a *time* picture (how fast words come out) and a *space* picture (how words are mentally organised).

---

## Dataset

The main file is `final_dataset.csv` — a merged dataset combining VFT timing, SpAM coordinates, and participant demographics.

**Key columns:**

| Column | Description |
|--------|-------------|
| `subject_id` | Unique participant ID |
| `domain` | Semantic category (animals, foods, body-parts, colours, furniture-practice) |
| `word` | The word the participant typed |
| `language` | Script used: `hindi`, `hinglish`, or `english` |
| `latency_ms` | Time in ms since the previous word (inter-response time / IRT) |
| `x_norm`, `y_norm` | Normalised SpAM canvas coordinates (0 to 1) |
| `Hi_Read`, `Hi_Write` | Self-reported Hindi reading/writing proficiency (1–5 scale) |
| `state_ut` | Participant's home state |
| `first_language` | Mother tongue |
| `age`, `gender`, `dominant_hand` | Demographics |

**Sample stats:**
- 35 participants, 14 states
- 930 non-English word entries, 474 unique words
- Mean IRT: 6,686 ms (SD: 5,649 ms)

**Note:** English-tagged entries were excluded from analysis. Hindi and Hinglish were both kept since they still reflect access to the Hindi mental lexicon.

---

## Native vs. Non-Native grouping

We classified participants from **Kerala, Telangana, and Andhra Pradesh** as **Non-Native** Hindi speakers. These states are part of the Dravidian language family (Malayalam, Telugu), which is structurally very different from Hindi — different phonology, different grammar, different script, almost no shared vocabulary.

Participants from other states (Gujarat, Maharashtra, Bihar, etc.) were grouped as **Native**, even if Hindi isn't their mother tongue. Their languages (Gujarati, Marathi, Punjabi) are Indo-Aryan like Hindi and share a lot of vocabulary and structure, so cognitively they're much closer to native Hindi speakers.

This gives us: **32 Native, 3 Non-Native**.

---

## Hypotheses

| # | Hypothesis | Led by |
|---|-----------|--------|
| H1 | Native speakers produce more words and retrieve them faster | Yogendra |
| H2 | Native speakers cluster words more tightly in SpAM | Yogendra |
| H3 | Non-Natives switch semantic patches more often | Yogendra |
| H4 | First words recalled are placed closer to the SpAM centroid (prototypicality) | Yogendra |
| H5 | Non-Natives have a higher word repeat rate | Rinkesh |
| H6 | IRT differences between groups are domain-dependent | Rinkesh |
| H7 | Larger spatial jumps correlate with longer IRTs | Rinkesh |
| H8 | There is an "exit pause" before a cluster switch | Rinkesh |
| H9 | Higher Hindi proficiency predicts more words and shorter IRT | Pranav |
| H10 | IRT increases over the course of a trial (semantic satiation) | Pranav |

---

## Project structure

```
HindiFluencyExperiment_TeamBrainiacs/
│
├── data/
│   └── final_dataset.csv          # Main merged dataset
│
├── analysis/
│   ├── REPORT_PHASE1_updated.Rmd  # R Markdown for Phase 1 analysis
│   └── figures/                   # Generated plots
│
├── reports/
│   ├── Report1.pdf                # Submitted Report 1
│   └── Brainiacs_Report1.pdf      # Final compiled report
│
└── README.md
```

---

## How to run the analysis

You need R with the following packages:

```r
install.packages(c("tidyverse", "ggplot2", "dplyr", "readr", "stringr", "scales", "tidyr"))
```

Then knit `REPORT_PHASE1_updated.Rmd` with the dataset in the same working directory:

```r
rmarkdown::render("REPORT_PHASE1_updated.Rmd")
```

Make sure `final_dataset.csv` is in the same folder as the Rmd file, or update the path at the top of the file.

---

## Phase 2 plan (coming up)

Report 1 was all descriptive — visualisations and preliminary stats. Report 2 will run the actual inferential tests:

- **t-tests / Mann-Whitney U** for group comparisons (H1, H2, H3, H5, H8)
- **Pearson / Spearman correlation** for distance-time coupling (H7) and proficiency (H9)
- **One-way ANOVA / Kruskal-Wallis** for domain differences (H6) and proficiency levels (H9)
- **Linear mixed models** for recall-order effects (H4, H10)
- **Benjamini-Hochberg correction** to control false discovery rate across all 10 hypotheses
- **Permutation tests** where the independence assumption doesn't hold

---

## References

- Hills, T. T., Jones, M. N., & Todd, P. M. (2012). Optimal foraging in semantic memory. *Psychological Review*, 119(2), 431–440.
- Dautriche, I. et al. (2016). Words cluster phonetically beyond phonological regularities. *Cognition*, 163, 128–145. https://colala.berkeley.edu/papers/dautriche2016wordform.pdf
- Zemla, J. C., & Austerweil, J. L. (2018). Estimating semantic networks of groups and individuals from fluency data. *Computational Brain & Behavior*, 1(1), 36–58. https://osf.io/preprints/psyarxiv/2bazx_v1
- Benjamini, Y., & Hochberg, Y. (1995). Controlling the false discovery rate. *Journal of the Royal Statistical Society: Series B*, 57(1), 289–300.
