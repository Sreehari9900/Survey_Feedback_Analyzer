<div align="center">

  <!-- Repository header banner -->
  <img src="https://capsule-render.vercel.app/api?type=rect&height=190&color=0:0F172A,100:2563EB&text=Survey%20Feedback%20Analyzer&fontColor=FFFFFF&fontSize=38&fontAlignY=42&desc=Clean%20text.%20Discover%20insights.&descAlignY=65&descSize=17" alt="Survey Feedback Analyzer banner" width="100%">

  <p>
    <strong>A beginner-friendly Python project for cleaning survey comments and extracting simple customer-feedback insights.</strong>
  </p>

  <p>
    <img src="https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white" alt="Python">
    <img src="https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white" alt="Jupyter Notebook">
    <img src="https://img.shields.io/badge/Dependencies-Core%20Python-2E8B57" alt="Core Python">
    <img src="https://img.shields.io/badge/Project-SurveyFeedbackAnalyzer-16A34A" alt="Project status">
  </p>
</div>

## 📌 Project Overview
Survey Feedback Analyzer is a text-based Python project that organizes customer survey responses, cleans unstructured feedback, and summarizes useful patterns. It was developed as a Python Fundamentals course project to practise foundational programming and data-handling skills.

The program stores survey information in a dictionary of lists and uses Python's built-in functions and string methods to standardize comments and calculate basic insights.

---

### 🎯 Problem Statement

Raw survey comments can contain inconsistent capitalization, punctuation, and extra spaces. The goal of this project is to turn those comments into cleaner, easier-to-analyze data and provide a quick summary of customer ratings and feedback.

The program:
* - Starts with 10 preloaded survey responses.
* - Allows users to add more responses with an automatically generated serial number.
* - Cleans feedback text before analysis.
* - Counts how many feedback entries contain a selected word.
* - Calculates the average rating, longest comment, and unique words.
* - Includes an optional feature to sort responses by rating.
  
The original assignment brief is available at [`docs/Problem_Statement.pdf`](docs/Problem_Statement.pdf).

---

### ✨ Key Features

Feature	Description

🗂️ Feedback storage	Stores serial number, name, comment, and rating in a dictionary of lists.

➕ Add responses	Accepts new feedback entries through user input.

🧹 Text cleaning	Removes selected punctuation, normalizes whitespace, and converts text to lowercase.

🔎 Keyword analysis	Counts feedback entries containing a specified whole word.

⭐ Rating summary	Calculates the average rating across responses.

📝 Comment analysis	Identifies the longest feedback comment by word count.

🔤 Unique vocabulary	Finds and alphabetically sorts unique words.

↕️ Optional sorting	Sorts feedback entries from highest to lowest rating.


### 🧭 Workflow
<p align="center">
</p>

Workflow summary: Input or load feedback → clean comment text → count selected keywords → calculate summary insights → review results.

---

### 🧰 Tools and Concepts

* - Language: Python

* - Environment: Jupyter Notebook

* - Data structure: Dictionary of lists
  
* - Input handling: input(), int()
    
* - Loops and conditions: for, range(), if
    
* - Text processing: replace(), split(), join(), lower()
    
* - Built-in functions and collections: sum(), len(), max(), set(), sorted(), zip()
    
* - Reusable logic: User-defined functions and lambda
    
* No third-party Python libraries are required for the core solution.

---

### 🧹 Text Cleaning Example

* Raw feedback	Cleaned feedback
* Very GOOD Service!!!	very good service
* poor support, not happy	poor support not happy
* GREAT experience! will come again.	great experience will come again
* Satisfied. But could be better.	satisfied but could be better

The cleaning process replaces selected punctuation with spaces, normalizes whitespace, trims extra spaces, and converts text to lowercase. This makes keyword matching more consistent.

---

### 📊 Sample Results

* The sample run contains 12 feedback entries: 10 preloaded responses and 2 added by the user.
* Insight	Sample result
* Feedbacks containing good	4
* Feedbacks containing poor	2
* Feedbacks containing excellent	1
* Average rating	3.42 / 5
* Longest feedback	poor response and poor handling of issue (7 words)
* Unique words	30


<p align="center"> 
  
</p>

What the sample suggests

* - The average rating is 3.42 out of 5.
* - Keyword counts provide a quick view of recurring positive and negative terms.
* - Reading comments alongside ratings provides context that a rating alone may not capture.
* - These figures reflect the repository's sample run and are not intended to represent a real customer population.

---

### 📁 Repository Structure

survey-feedback-analyzer

├── README.md

├── notebook/

│   └── Survey_Feedback_Analyzer.ipynb

├── docs/

│   └── Problem_Statement.pdf

---

### 📚 Key Learnings

- Why text should be cleaned before keyword analysis.
- How to store related tabular data using a dictionary of lists.
- How to collect input and append records dynamically.
- How to build reusable functions for repeated analysis.
- How sets can identify unique words and sorting can organize results.
- How to summarize text data with basic Python operations.

---

### 🔮 Possible Improvements

- Validate that ratings are integers between 1 and 5.
- Handle empty input and invalid values gracefully.
- Count and rank the most frequent words automatically.
- Exclude common filler words (stop words) from keyword analysis.
- Add visualizations for rating distributions and keyword frequency.
- Refactor the notebook into reusable functions or a small application.

--- 

### 👤 Author

**Y. Srihari**

**Aspiring Data Analyst**

**Python | SQL | Excel | Power BI**

<p align="center">
  <sub>Built as a learning project to practise Python fundamentals and basic text analysis.</sub>
</p>
