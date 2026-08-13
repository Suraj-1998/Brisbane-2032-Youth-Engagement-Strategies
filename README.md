# Where should a sporting body build a generation of fans?

Brisbane hosts the 2032 Olympic and Paralympic Games. That gives Australian sporting
bodies an unusually long runway to grow youth participation — but a limited budget and
142 sports to spread it across.

This analysis asks a narrower question: **if you could only concentrate effort on a handful
of sports, which ones, and on what evidence?**

The answer turned out to be more concentrated than expected.

---

## Finding

**Around 84% of estimated 5–14 participation sits inside the top 20 sports.**

Spreading investment evenly across 142 sports would put most of the money where almost none
of the young people are. The practical recommendation is a focused priority set, chosen on
more than raw headcount.

Three further points shaped that recommendation:

- **Ranking on raw participation just rediscovers what is already big.** Sports with large
  adult bases dominate the top of the list regardless of how well they hold young people.
- **A sport with 300 participants can post a spectacular youth ratio and mean nothing.**
  Ratio-based measures need a floor before they say anything real.
- **Media attention and participation do not line up.** The sports the press writes about
  are not reliably the sports children play.

---

## Approach

### Data

| Source | Used for |
| --- | --- |
| AusPlay participation tables (Australian Sports Commission) | Participation by sport and age band |
| The Guardian Open Platform API | ~400 articles on Australian sport, youth participation and the 2032 Games |

Both are public. No personal or identifying data is used anywhere in this analysis.

### Method

**1. Cleaning and shaping.** Participation tables arrive with inconsistent sport naming and
mixed age-band definitions. Sports were normalised to a single label set and filtered to
those with plausible Olympic or Paralympic relevance.

**2. Feature engineering.** Raw participation counts answer "who is big", not "where is the
opportunity". Three derived measures were built instead:

- **Youth concentration** — what share of a sport's participants are aged 5–14
- **Adolescent retention** — whether a sport keeps participants through the 12–14 band
- **Gender balance** — how evenly participation is split

A **minimum participation threshold** was applied before any ratio was calculated, so small
sports could not produce unstable percentages that dominate a ranking.

**3. Segmentation.** Min-max scaling followed by k-means clustering, to collapse four separate
rankings into one grouping a decision maker can actually act on. Sports that rank fifth on one
measure and fortieth on another are not usefully described by any single list.

**4. Text analysis.** Articles collected through the Guardian API, cleaned with regular
expressions, then vectorised with TF-IDF and modelled with NMF to identify what the media
conversation about Australian sport is actually about — and where it diverges from
participation.

---

## Repository

```
notebooks/    Analysis, in order
data/         Place raw AusPlay files here (not committed — see below)
outputs/      Generated figures and tables
```

## Running it

```bash
git clone https://github.com/<your-username>/brisbane-2032-youth-engagement.git
cd brisbane-2032-youth-engagement
pip install -r requirements.txt
jupyter notebook
```

Two things are not in this repository and you will need to supply them:

- **AusPlay data files.** Download the participation tables from the Australian Sports
  Commission and place them in `data/`. They are redistributable under their own terms, so
  they are not committed here.
- **A Guardian API key.** Free from the Guardian Open Platform. Set it as an environment
  variable rather than pasting it into a notebook:

```bash
export GUARDIAN_API_KEY="your-key-here"
```

---

## Limitations

Worth stating plainly, because they affect how far the finding travels:

- AusPlay is **survey-based**, so participation figures are estimates with sampling error,
  not a census. Small sports carry proportionally more uncertainty.
- Age bands are **fixed by the source**, so "youth" is defined by what the survey collected
  rather than by what would be ideal for this question.
- The Guardian is **one masthead**. It is a reasonable proxy for one segment of national
  coverage, not for Australian sports media as a whole.
- Participation is not the same as **fandom**. This analysis measures who plays, which is a
  proxy for who might watch, not a direct measurement of it.

## Ethics

The recommendation concentrates resources, which by definition means directing them away
from sports outside the priority set. Analysis that informs funding decisions should say so
rather than presenting a ranking as though it were neutral. Gender balance was included as a
measure for the same reason — optimising only for total youth numbers would systematically
favour sports that already skew one way.

---

## Built with

Python · pandas · NumPy · scikit-learn · Plotly

---

Originally developed as coursework for a Master of Information Technology (Data Science) at
QUT, then rebuilt for this repository.

**Suraj Thirumalaimuthu** — Brisbane, Australia
[LinkedIn](https://www.linkedin.com/in/suraj-thirumalaimuthu-b1a306114/)
