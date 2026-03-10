# Inequality Headlines — Data explanation

This folder contains the processed data, stimuli, and analysis code for two studies examining how AI-reframed news headlines about economic inequality affect reader engagement and belief updating.


---

## Folder Contents

```
public_release/
├── study1_long_processed.csv          # Study 1 — long format (one row per participant × headline)
├── study1_predictions_processed.csv   # Study 1 — participant level (predictions & belief change)
├── study2_participant_processed.csv   # Study 2 — wide format (one row per participant)
├── study2_long_processed.csv          # Study 2 — long format (one row per participant × headline seen)
├── modified_titles_factchecked_experiment.json  # Study 1 stimuli: original & AI-reframed headlines
├── cleaned_articles_with_headlines.json         # Study 2 stimuli: articles, AI-reframed titles, URLs
├── cleaned_articles_with_headlines_unfiltered.json  # Study 2 stimuli (unfiltered version)
├── cleaned_control_articles.json                # Study 2 control articles (non-inequality topics)
├── supplementary_information.Rmd      # Supplementary heterogeneity analyses (reads processed data)
└── README.md                          # This file
```

---

## Study 1

### Design

Participants rated 20 news headlines (displayed one page at a time) on their anticipated click, share, and agreement likelihood. Headlines were either original news titles or AI-reframed versions designed to be more approachable to readers skeptical of inequality. After rating all headlines, participants read one randomly selected full article, and prior belief measures were re-administered.

**Condition assignment:** Each headline seen by a participant was independently assigned to either the `original` or `flipped` (AI-reframed) condition via counterbalancing across the 20-item set.

### Files

#### `study1_long_processed.csv`
One row per **participant × headline** (~20 rows per participant). This is the primary file for engagement analyses.

| Variable | Type | Description |
|---|---|---|
| `ProlificID` | string | Participant identifier (Prolific) |
| `statementText` | string | Headline text as seen by the participant |
| `click_rating` | integer (1–5) | "How willing would you be to **click** on this article?" |
| `share_rating` | integer (1–5) | "How willing would you be to **share** this on social media?" |
| `agreement_rating` | integer (1–5) | "How much do you think you would **agree** with this article?" |
| `condition` | string | `original` = original headline; `flipped` = AI-reframed headline |
| `item_nr` | integer | Headline item identifier (links to JSON stimulus file) |
| `Educational.Level` | string | Highest educational degree (see coding below) |
| `DemRep_C_num` | integer | Party identification (−3 = Strongly Democratic, +3 = Strongly Republican) |
| `Ideology_econ_num` | integer | Economic ideology (−2 = Very liberal, +2 = Very conservative) |
| `Ideology_soc_num` | integer | Social ideology (−2 = Very liberal, +2 = Very conservative) |
| `ideology` | numeric | Mean of `Ideology_econ_num` and `Ideology_soc_num` |
| `income_num` | integer | Household income category (1 = <$25k, 6 = $150k+) |
| `gender` | string | Gender identity |
| `Household` | integer | Number of people in household |
| `AttentionCheck2` | string | Attention check response (raw) |
| `top25pre` | numeric | % of wealth owned by top 25% (pre-exposure estimate) |
| `upper25pre` | numeric | % of wealth owned by upper-middle 25% (pre-exposure estimate) |
| `lower25pre` | numeric | % of wealth owned by lower-middle 25% (pre-exposure estimate) |
| `bottom25pre` | numeric | % of wealth owned by bottom 25% (pre-exposure estimate) |
| `top25post` | numeric | % of wealth owned by top 25% (post-exposure estimate) |
| `upper25post` | numeric | % of wealth owned by upper-middle 25% (post-exposure estimate) |
| `lower25post` | numeric | % of wealth owned by lower-middle 25% (post-exposure estimate) |
| `bottom25post` | numeric | % of wealth owned by bottom 25% (post-exposure estimate) |
| `inequality_subj_1` | integer (1–7) | "Differences in wealth in the US are too large." (pre-exposure) |
| `inequality_pol_1` | integer (1–7) | "The US government should take measures to reduce wealth differences." (pre-exposure) |
| `inequality_luck_1_1` | integer (1–7) | Luck vs. hard work attribution (1 = luck exclusively, 7 = abilities exclusively) (pre-exposure) |
| `inequality_subj_2` | integer (1–7) | Subjective inequality perception (post-exposure) |
| `inequality_pol_2` | integer (1–7) | Policy support (post-exposure) |
| `inequality_luck_2_1` | integer (1–7) | Luck vs. hard work attribution (post-exposure) |

#### `study1_predictions_processed.csv`
One row per **participant**. Contains the selected article, prediction accuracy, and belief change scores.

| Variable | Type | Description |
|---|---|---|
| `ProlificID` | string | Participant identifier |
| `selectedValue` | string | Headline text of the article the participant read |
| `condition` | string | `original` or `flipped` (condition of selected headline) |
| `item_nr` | integer | Item identifier of selected headline |
| `actualShare` | numeric | Actual % of other participants who chose to share this headline |
| `actualAgreement` | numeric | Actual % of other participants who agreed with this headline |
| `predictedShare` | numeric (1–5) | Participant's predicted share rating for selected headline |
| `predictedAgreement` | numeric (1–5) | Participant's predicted agreement rating for selected headline |
| `top25pre` | numeric | Pre-exposure: estimated % wealth held by top quartile |
| `upper25pre` | numeric | Pre-exposure: estimated % wealth held by upper-middle quartile |
| `lower25pre` | numeric | Pre-exposure: estimated % wealth held by lower-middle quartile |
| `bottom25pre` | numeric | Pre-exposure: estimated % wealth held by bottom quartile |
| `top25post` | numeric | Post-exposure: same as above |
| `upper25post` | numeric | Post-exposure |
| `lower25post` | numeric | Post-exposure |
| `bottom25post` | numeric | Post-exposure |
| `error_top25` | numeric | Absolute error: \|top25pre/100 − 0.85\| |
| `error_uppermid25` | numeric | Absolute error: \|upper25pre/100 − 0.10\| |
| `error_lowermid25` | numeric | Absolute error: \|lower25pre/100 − 0.04\| |
| `error_bottom25` | numeric | Absolute error: \|bottom25pre/100 − 0.01\| |
| `ineq_accuracy` | numeric | Objective accuracy score pre-exposure: 1 − mean(4 errors) |
| `ineq_accuracy_post` | numeric | Objective accuracy score post-exposure |
| `inequality_subj_1` | integer (1–7) | Prior subjective inequality perception |
| `inequality_pol_1` | integer (1–7) | Prior policy support |
| `inequality_luck_1_1` | integer (1–7) | Prior luck/ability attribution |
| `inequality_subj_2` | integer (1–7) | Posterior subjective inequality perception |
| `inequality_pol_2` | integer (1–7) | Posterior policy support |
| `inequality_luck_2_1` | integer (1–7) | Posterior luck/ability attribution |
| `DemRep_C_num` | integer | Party ID (−3 to +3) |
| `Ideology_econ_num` | integer | Economic ideology (−2 to +2) |
| `Ideology_soc_num` | integer | Social ideology (−2 to +2) |
| `ideology` | numeric | Mean ideology |
| `income_num` | integer | Income category (1–6) |
| `gender` | string | Gender identity |
| `Educational.Level` | string | Highest degree |

---

## Study 2

### Design

Participants completed a Reddit-style social media simulation viewing 20 headlines (10 inequality-related, 10 control topics), casting upvotes or downvotes on each. They then read the full article corresponding to one randomly selected headline. Belief measures were administered before and after.

**Condition assignment** (`condition`): `personal` = AI-reframed headlines shown; `original` = original headlines shown.
**Article exposure** (`selectedTitleSource`): `1` = the selected headline came from the inequality article pool; `2` = from the control pool.

### Files

#### `study2_participant_processed.csv`
One row per **participant**. Contains all survey responses, condition assignment, and article exposure metadata.

| Variable | Type | Description |
|---|---|---|
| `original_row` | integer | Row index in the processed dataset |
| `prolific` | string | Participant identifier (Prolific) |
| `condition` | string | `personal` = AI-reframed headlines; `original` = original headlines |
| `selectedTitle` | string | Headline text of the article participant read |
| `selectedTitleSource` | integer | `1` = inequality article; `2` = control article |
| `articleIndex` | integer | Index into the JSON article list for the selected headline |
| `json_index_selectedValue` | integer | JSON index of selected article (for matching to stimulus files) |
| `selectedValue_found_in` | string | Field used to match: `title` or `selected_title` |
| `articleDisplayStatus` | string | `found` = article displayed; `not_found` = article not available |
| `selectedTitleSourceStat` | numeric | Contrast-coded article condition: 0.5 = article shown, −0.5 = not shown |
| `conditionstat` | integer | Headline condition: 1 = AI-reframed (`personal`), 0 = original |
| `DemRep_C` | string | Party identification (text label) |
| `DemRep_C_num` | integer | Party ID numeric: −3 (Strongly Democratic) to +3 (Strongly Republican) |
| `income` | string | Household income category (text label) |
| `income_num` | integer | Income numeric: 1 (<$25k) to 6 ($150k+) |
| `Ideology_econ` | string | Economic ideology (text) |
| `Ideology_social` | string | Social ideology (text) |
| `Educational.Level` | string | Highest degree |
| `Household` | integer | Household size |
| `inequality_subj_1` | integer (1–7) | "Differences in wealth in the US are too large." (pre-exposure) |
| `inequality_pol_1` | integer (1–7) | "US government should reduce wealth differences." (pre-exposure) |
| `inequality_luck_1_1` | integer (1–7) | Luck vs. ability attribution (pre-exposure) |
| `inequality_pol_sp1_1` | integer (1–7) | Support for progressive taxation (pre-exposure) |
| `inequality_pol_sp1_2` | integer (1–7) | Support for affordable housing initiatives (pre-exposure) |
| `inequality_subj_2` | integer (1–7) | Subjective inequality (post-exposure) |
| `inequality_pol_2` | integer (1–7) | Policy support (post-exposure) |
| `inequality_luck_2_1` | integer (1–7) | Luck/ability attribution (post-exposure) |
| `inequality_pol_sp2_1` | integer (1–7) | Support for progressive taxation (post-exposure) |
| `inequality_pol_sp2_2` | integer (1–7) | Support for affordable housing (post-exposure) |
| `credibility_1` | integer (0–100) | "How much do you trust the information in this article is reliable?" |
| `title0`–`title19` | string | Headlines shown at each of the 20 positions in the simulation |
| `vote0`–`vote19` | string | Vote cast for each position: `upvote` or `downvote` |

#### `study2_long_processed.csv`
One row per **participant × headline position** (20 rows per participant). Primary file for engagement (vote) analyses.

Contains all participant-level columns above (excluding the wide `title#`/`vote#` columns) plus:

| Variable | Type | Description |
|---|---|---|
| `title` | string | Headline text at this position |
| `vote` | string | `upvote` or `downvote` |
| `title_position` | string | Which position in the feed (e.g., `title3`) |

---

## Variable Coding Reference

### Party Identification (`DemRep_C_num`)
| Label | Value |
|---|---|
| Strongly Democratic | −3 |
| Democratic | −2 |
| Lean Democratic | −1 |
| Lean Republican | +1 |
| Republican | +2 |
| Strongly Republican | +3 |

### Ideology (`Ideology_econ_num`, `Ideology_soc_num`)
| Label | Value |
|---|---|
| Very liberal | −2 |
| Liberal | −1 |
| Moderate | 0 |
| Conservative | +1 |
| Very conservative | +2 |
| Not sure | NA |

### Household Income (`income_num`)
| Label | Value |
|---|---|
| Less than $25,000 | 1 |
| $25,000–$49,999 | 2 |
| $50,000–$74,999 | 3 |
| $75,000–$99,999 | 4 |
| $100,000–$149,999 | 5 |
| $150,000 or more | 6 |
| Prefer not to say | NA |

### Education (`Educational.Level`)
1. Less than high school degree
2. High school graduate (diploma or GED equivalent)
3. Some college but no degree
4. Associate degree (2-year)
5. Bachelor's degree (4-year)
6. Master's degree
7. Doctoral degree
8. Professional degree (JD, MD)

### Headline Condition
| Study | Variable | Value | Meaning |
|---|---|---|---|
| Study 1 | `condition` | `original` | Original news headline |
| Study 1 | `condition` | `flipped` | AI-reframed headline |
| Study 2 | `condition` | `original` | Original headlines shown |
| Study 2 | `condition` | `personal` | AI-reframed headlines shown |
| Study 2 | `conditionstat` | 0 | Original condition |
| Study 2 | `conditionstat` | 1 | AI-reframed (personal) condition |

### Article Condition (Study 2 only)
| Variable | Value | Meaning |
|---|---|---|
| `selectedTitleSource` | 1 | Article from inequality pool |
| `selectedTitleSource` | 2 | Article from control pool |
| `selectedTitleSourceStat` | 0.5 | Inequality article shown (article condition) |
| `selectedTitleSourceStat` | −0.5 | Control article / article not shown |

---

## Stimuli

### Study 1: `modified_titles_factchecked_experiment.json`
Array of objects with fields:
- `item_nr`: integer item identifier
- `original`: original news headline
- `flipped`: AI-reframed headline
- `content`: full article text

### Study 2: `cleaned_articles_with_headlines.json`
Array of objects with fields:
- `url`: source URL
- `title`: original article title
- `selected_title`: AI-reframed headline (used in the `personal` condition)
- `domain`: news outlet domain
- `text` / `onlytext`: full article text
- `ratings`: object with topical labels (e.g., `"Progressive tax/redistribution policy": "Yes/No"`)
- `generated_titles`: array of candidate AI-reframed titles

### Study 2 control: `cleaned_control_articles.json`
Same structure as above; articles on non-inequality topics shown to all participants alongside the focal headlines.

---
