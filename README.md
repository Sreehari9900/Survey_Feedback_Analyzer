

# Survey Feedback Analyzer

![Python](https://img.shields.io/badge/Python-3.8%2B-1F3A5F?logo=python&logoColor=white)
![Dependencies](https://img.shields.io/badge/dependencies-none-2A9D8F)
![Type](https://img.shields.io/badge/type-Module%20End%20Assignment-E9C46A)

A command-line tool, written in pure Python, that cleans customer survey feedback and turns it into simple insights: word counts, average rating, the longest comment, the vocabulary used, and a rating-ranked view.

**Author:** Yallappagari Srihari
**Course:** Python Fundamentals, Module End Assignment 3

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Data Structure](#2-data-structure)
3. [Adding More Feedbacks](#3-adding-more-feedbacks)
4. [Text Cleaning](#4-text-cleaning)
5. [Word Count Insights](#5-word-count-insights)
6. [Final Summary and Insights](#6-final-summary-and-insights)
7. [Optional: Sorting by Rating](#7-optional-sorting-by-rating)
8. [How to Run](#8-how-to-run)
9. [Sample Output](#9-sample-output)
10. [Testing and Validation](#10-testing-and-validation)
11. [Design Decisions](#11-design-decisions)
12. [Project Structure](#12-project-structure)
13. [Concepts Demonstrated](#13-concepts-demonstrated)
14. [Possible Improvements](#14-possible-improvements)

---

## 1. Project Overview

Survey comments are written in many styles: capital letters, extra spaces, repeated punctuation. Before any analysis, the text has to be standardised. This project covers that full flow on a small dataset.

**Business questions answered**

| Question | Output |
|---|---|
| How many customers mention "good", "poor" or "excellent"? | Word-count function |
| What is the overall satisfaction level? | Average rating |
| Which customer wrote the most detailed comment? | Longest-feedback finder |
| What vocabulary do customers use? | Unique-word list |
| Who is happiest and who is least happy? | Rating-sorted view (optional) |

**Pipeline:** Load data, add feedbacks, clean text, count words, summarise, sort.

---

## 2. Data Structure

<p align="center"><img src="images/02_data_structure.png" alt="Dictionary of lists structure" width="90%"></p>

Data is held in a **dictionary of lists**. Each key is a column, and position `i` in every list describes the same respondent.

```python
feedback_data = {
    'S_No':     [1, 2, 3, ...],
    'Name':     ['Ravi', 'Meera', 'Sam', ...],
    'Feedback': [' Very GOOD Service!!!', 'poor support, not happy ', ...],
    'Rating':   [5, 2, 5, ...]
}
```

The project starts with 10 preloaded feedbacks. All four lists must always stay the same length.

---

## 3. Adding More Feedbacks

<p align="center"><img src="images/03_add_feedbacks.png" alt="Flow for adding feedbacks" width="90%"></p>

The user chooses how many feedbacks to add. For each one the program collects:

- **Name**
- **Written feedback**
- **Rating (1 to 5).** Invalid input is rejected and asked again.

`S_No` is generated automatically (`len(S_No) + 1`), so new entries continue from 11. One value is appended to each of the four lists.

---

## 4. Text Cleaning

<p align="center"><img src="images/04_text_cleaning.png" alt="Before and after text cleaning" width="90%"></p>

Every feedback goes through the same four rules:

| Rule | Technique |
|---|---|
| Remove punctuation (`. , ! ?`) | `.replace(mark, ' ')` |
| Convert to lowercase | `.lower()` |
| Collapse multiple spaces | `.split()` then `' '.join(...)` |
| Remove leading and trailing spaces | `.split()` ignores them automatically |

```python
def clean_text(text):
    for mark in ['.', ',', '!', '?']:
        text = text.replace(mark, ' ')
    return ' '.join(text.lower().split())
```

Punctuation is replaced with a **space** rather than deleted, so `good,service` becomes `good service` and not `goodservice`.

---

## 5. Word Count Insights

<p align="center"><img src="images/05_word_count.png" alt="Bar chart of word counts" width="90%"></p>

`count_word_in_feedbacks(word)` returns how many **feedbacks** contain a word. The match is case-insensitive and based on whole words.

```python
def count_word_in_feedbacks(word):
    word = word.lower()
    count = 0
    for text in feedback_data['Feedback']:
        if word in text.lower().split():
            count += 1
    return count
```

A feedback such as `good food and good ambience` contains "good" twice but is counted **once**.

| Word | Feedbacks (10 preloaded) |
|---|---|
| good | 3 |
| poor | 2 |
| excellent | 1 |

---

## 6. Final Summary and Insights

<p align="center"><img src="images/06_summary_insights.png" alt="Summary metric cards" width="90%"></p>

| Insight | Method | Result (10 preloaded) |
|---|---|---|
| Cleaned dataset | `print(feedback_data)` | Lowercase, punctuation-free text |
| Average rating | `sum(ratings) / len(ratings)` | **3.40** |
| Longest comment | Loop tracking the highest `len(text.split())` | **Kiran**, 7 words: *"poor response and poor handling of issue"* |
| Unique words | `set()` built from every feedback | **30** words |

---

## 7. Optional: Sorting by Rating

<p align="center"><img src="images/07_sorted_by_rating.png" alt="Feedbacks sorted by rating" width="90%"></p>

`zip()` combines the three lists row by row, and `sorted(..., reverse=True)` orders them from highest to lowest. The rating is placed first in each tuple so it drives the sort.

```python
combined = zip(feedback_data['Rating'], feedback_data['Name'], feedback_data['Feedback'])
for rating, name, text in sorted(combined, reverse=True):
    print(rating, "|", name, "|", text)
```

---

## 8. How to Run

<p align="center"><img src="images/08_how_to_run.png" alt="How to run the program" width="90%"></p>

**Requirements:** Python 3.8 or newer. No external libraries.

```bash
python survey_feedback_analyzer.py
```

When asked *"How many more feedbacks do you want to add?"*, enter `0` to analyse only the preloaded data, or enter a number to add your own entries.

---

## 9. Sample Output

Run with `0` extra feedbacks:

```
--- Word Count Insights ---
Feedbacks containing 'good': 3
Feedbacks containing 'poor': 2
Feedbacks containing 'excellent': 1

Average rating: 3.40

Longest feedback:
  Name    : Kiran
  Text    : poor response and poor handling of issue
  Words   : 7

Unique words (30):
['again', 'ambience', 'and', 'bad', 'be', 'better', ...]
```

---

## 10. Testing and Validation

Run with `0` extra feedbacks and compare against the expected values:

```python
assert count_word_in_feedbacks("good") == 3
assert count_word_in_feedbacks("GOOD") == 3          # case-insensitive
assert count_word_in_feedbacks("poor") == 2
assert count_word_in_feedbacks("excellent") == 1
assert count_word_in_feedbacks("goo") == 0           # partial words do not match
assert round(sum(feedback_data['Rating']) / len(feedback_data['Rating']), 2) == 3.4
```

**Manual test cases**

| Test | Input | Expected |
|---|---|---|
| Invalid rating | `9`, then `4` | Program asks again, accepts `4` |
| Non-numeric count | `abc`, then `1` | Program asks again |
| Messy text | `  WOW!!!   Great,,,  service... ` | `wow great service` |
| Repeated word | `Good good GOOD service` | "good" count rises by 1, not 3 |
| Serial numbers | Add 2 feedbacks | `S_No` ends with 11, 12 |

---

## 11. Design Decisions

- **Feedbacks, not occurrences:** the assignment asks how many feedbacks contain a word, so each feedback is counted at most once.
- **Whole-word matching:** `word in text.split()` avoids false matches such as "goo" inside "good".
- **Cleaning after input:** new feedbacks are cleaned together with the preloaded ones, so every analysis sees consistent text.
- **Input validation:** a helper keeps asking until a valid whole number in range is entered, so bad input cannot crash the program.
- **Strict `>` for the longest comment:** if two feedbacks tie, the earlier one is reported.

---

## 12. Project Structure

```
survey-feedback-analyzer/
├── survey_feedback_analyzer.py    # main program
├── README.md                      # this file
└── images/                        # illustrations used in this README
    ├── 01_banner.png
    ├── 02_data_structure.png
    ├── 03_add_feedbacks.png
    ├── 04_text_cleaning.png
    ├── 05_word_count.png
    ├── 06_summary_insights.png
    ├── 07_sorted_by_rating.png
    └── 08_how_to_run.png
```

---

## 13. Concepts Demonstrated

| Area | Where it is used |
|---|---|
| Dictionary of lists | Storing the survey data |
| `for` and `while` loops | Collecting input, cleaning, counting |
| Conditionals (`if`) | Rating validation, word matching, longest comment |
| String methods | `replace()`, `lower()`, `split()`, `join()` |
| User-defined functions | `clean_text()`, `count_word_in_feedbacks()` and the step functions |
| Sets | Unique-word list |
| `zip()` and `sorted()` | Rating-ranked output |

---

## 14. Possible Improvements

- Ignore common filler words (such as "and", "of") in the unique-word list
- Count the most frequent words, not only unique ones
- Handle negation, for example treating "not bad" differently from "bad"
- Save the cleaned data to a CSV file
- Add a simple sentiment label (positive, neutral, negative) based on rating
