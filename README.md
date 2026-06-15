# HCIS L7 &middot; K6 Data Sources Quiz

A self-contained, multiple-choice revision quiz for **K6** of the Health and Care Intelligence Specialist (Level 7) apprenticeship standard. It runs entirely in the browser, loads its questions from a single JSON file, and costs nothing to host. There is no server, no database, and no learner data is collected or stored: every attempt is fresh and private to the learner's own browser.

This is one of a set of single-KSB quiz repos. Each KSB has its own repo, its own `index.html`, and its own question bank, so they can be released and revised one at a time.

## What K6 covers

The K6 requirement, verbatim from the standard, is:

> A wide range of health and care data sources (e.g. demographic, health, social care, economic, finance, local and national NHS and other relevant data sources) and their relative strengths, weaknesses and uses.

The bank in this repo works across the data-source families the EPAO amplification lists for K6, and across the cross-cutting ideas used to appraise any source:

- **Demographic and population data**: Census, ONS population estimates and projections, Nomis.
- **Primary care data**: GDPPR, GP Patient Survey (GPPS), QOF, GP Practice Records (GPPR).
- **Secondary care data**: HES, ECDS, MSDS, SUS PbR.
- **Community, mental health and social care data**: MHSDS, CSDS, IAPT, SALT, ASC-FR, ASCOF, CHC.
- **Public health**: UKHSA surveillance datasets, NIMS, Health Survey for England (HSE).
- **Economic and finance data**: Commissioning Data Sets (CDS), NHS Costing Returns (NCRS).
- **Wider determinants**: Nomis, DWP and Department for Education datasets.
- **Open data portals and benchmarking**: Fingertips, NHS England dashboards, ONS Secure Research Service, NHS Data Access Environment, Model Health System / Model Hospital.
- **Appraising a source**: coverage, granularity, timeliness, completeness, coding variation, linkage potential, access constraints, survey vs administrative data, operational vs financial data.

## What is in this repo

- `index.html` is the quiz itself (the engine and styling). You rarely need to touch this.
- `questions.json` is the K6 question bank. This is the file you edit to add or change questions.
- `README.md` is this file.

## How learners use it

Once deployed, give learners the page URL. They start the quiz, answer one question at a time, and get feedback with a short rationale after each answer (the answer is not shown until they commit). At the end they see a score for K6 and a list of the questions they missed, each with its rationale, as a ready-made revision list.

## Deploying it (GitHub Pages, free)

1. Put `index.html` and `questions.json` into a **public** GitHub repository.
2. In `index.html`, the config line near the top is already set to `const QUESTION_BANK_URL = "questions.json";` so the page loads the bank that sits beside it.
3. In the repo, go to **Settings**, then **Pages**, set the source to the `main` branch and the root folder, and save.
4. After a minute, the Pages panel shows your live URL, of the form `https://YOURNAME.github.io/REPO/`. That single link is what you give learners.

To update questions later, edit `questions.json` in the repo and commit. The live quiz picks up the change within a minute or two. You never need to touch `index.html` again.

## Editing the question bank

`questions.json` is a list of question objects. One looks like this:

```json
{
  "id": "K6-001",
  "ksb": ["K6"],
  "stem": "The question text goes here.",
  "options": ["First option", "Second option", "Third option", "Fourth option"],
  "answer": 1,
  "rationale": "The explanation shown to the learner after they answer."
}
```

What each field means:

- `id`: a short unique label. The convention here is `K6-NNN`.
- `ksb`: the KSB code in a list. For this repo it is always `["K6"]`, kept as a list so the engine matches the multi-KSB original.
- `options`: the answer choices. Four is the convention throughout this bank.
- `answer`: the position of the correct option, counting from zero, so `0` is the first option and `3` is the fourth. This is the single easiest thing to get wrong, so check each one.
- `rationale`: the feedback shown after answering, and the text that appears in the end-of-quiz review list. This is what turns the quiz into a revision aid rather than a test, so make it worth reading.

Three rules keep the file valid:

- Use straight double quotes (`"`), not curly ones. Do not draft questions in Word, which converts them silently and breaks the file. Use a plain text editor such as VS Code.
- Put commas between items, but never after the last item in a list or object.
- Validate before committing. If the file fails to parse, the quiz quietly falls back to its built-in sample and your changes will appear to do nothing. VS Code underlines JSON errors as you type, or you can paste the file into any free online JSON validator.

## Configuration

A small, clearly marked config block sits near the top of `index.html`.

- `QUESTION_BANK_URL`: set to `"questions.json"` to load the bank from the repo, or `null` to use the built-in sample.
- `QUIZ_LENGTH`: how many questions to draw per attempt. Set to `12` here, drawn at random from the full bank of 60. Raise or lower it to taste.
- `WEAK_THRESHOLD`: retained for compatibility with the multi-KSB engine but unused on this single-KSB results screen.
- `STRATIFY_BY_KSB`, `KSB_LIST`, `PER_KSB`: stratified sampling, switched off. There is nothing to stratify across when every item is K6; the settings are left in place only so this file stays close to the multi-KSB original.

To rebrand the look, change the `--accent` colour variable in the style block near the top of `index.html`. It is currently set close to the JGA teal.

## Testing locally

Opening `index.html` straight from your hard drive will not load `questions.json`, because browsers block local file reads for security, so it falls back to the built-in sample. To test the real bank on your own machine, run `python -m http.server` in the folder and open the address it prints. On the live Pages URL it always works.

## Sources

The questions are written against the K6 requirement and amplification in:

- Occupational standard ST0830 v1.0, *Health and care intelligence specialist* (Skills England; Crown copyright).
- *End-point assessment plan* ST0830/AP01 (Crown copyright 2020).
- *Knowledge Test Amplification, Health and Care Intelligence Specialist, Level 7*.
