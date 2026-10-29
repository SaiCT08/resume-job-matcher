# Resume-Job Matcher

A Python prototype that scores how well a resume matches a job description, using semantic meaning instead of only keyword matching. A refined version of this idea was later used to screen applicants during my internship at Cquent Systems.

## How it works

Each resume gets a composite score from three parts:

- **Semantic similarity (60%)**: resumes and job descriptions are embedded with Sentence-Transformers, and FAISS (an exact inner-product index on normalized vectors, so cosine similarity) compares them
- **Keyword overlap (25%)**: TF-IDF weighted overlap between the job description's terms and the resume
- **Skill coverage (15%)**: share of the job's required skills found in the resume, from a skill list

Scores are normalized to 0 to 100 across the candidates, and the output lists the skills each resume is missing.

## Usage

```bash
pip install -r requirements.txt
python -m spacy download en_core_web_sm

# Score one resume against a job description
python resume_matcher_pipeline.py score --resume resume.txt --jd job.txt

# Rank a folder of resumes against a job description
python resume_matcher_pipeline.py rank --resumes_dir resumes/ --jd_path job.txt --out_csv results.csv
```

Resumes and job descriptions are plain `.txt` files. An optional `--skills` file (one skill per line) replaces the built-in skill list.

## Built with

Python, Sentence-Transformers, FAISS, scikit-learn, spaCy, pandas
