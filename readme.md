# 📄 ATS Resume Checker

A Streamlit app that estimates how well your resume would perform in an Applicant Tracking System (ATS) and tells you exactly what to improve. It uses Google's Gemini Flash model for the analysis.

## Features

- Upload a resume as **PDF, DOCX or TXT**
- Optional **job description** for a tailored keyword match
- **ATS score out of 100** with a five-part breakdown (keywords, achievements, formatting, structure, language)
- Prioritised **improvements**, found vs. missing **keywords**, and **bullet rewrites**
- Local checks for email, phone, LinkedIn, standard sections and length
- Downloadable report (Markdown)

## How the score works

Gemini rates each category from 0 to 100. The overall score is then calculated in code using fixed weights, so it stays consistent:

| Category | Weight |
|---|---|
| Keyword match | 30% |
| Achievements & impact | 25% |
| ATS-friendly formatting | 20% |
| Sections & structure | 15% |
| Language & clarity | 10% |

> This is an AI-generated estimate, not the output of a real ATS. Treat it as guidance.

## Run locally

1. Install Python 3.10 or newer.
2. Clone the repo and install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Get a free API key from [Google AI Studio](https://aistudio.google.com/app/apikey).
4. Provide the key in one of three ways:
   - Paste it into the app's sidebar, or
   - Set an environment variable: `export GEMINI_API_KEY="your-key"`, or
   - Create `.streamlit/secrets.toml` (never commit this file):
     ```toml
     GEMINI_API_KEY = "your-key"
     ```
5. Start the app:
   ```bash
   streamlit run app.py
   ```

## Deploy on Streamlit Community Cloud

1. Push this repo to GitHub (it must contain `app.py`, `requirements.txt` and `README.md`).
2. Go to [share.streamlit.io](https://share.streamlit.io) and sign in with GitHub.
3. Click **Create app**, choose your repository, branch `main`, and main file `app.py`.
4. Open **Advanced settings → Secrets** and add:
   ```toml
   GEMINI_API_KEY = "your-key"
   ```
5. Click **Deploy**.

Optional secret: `GEMINI_MODEL = "gemini-3.8-flash"` to change the model. The default is `gemini-3.8-flash`; check [Google's model list](https://ai.google.dev/gemini-api/docs/models) if it ever stops working.

## Project structure

```
.
├── app.py             # Streamlit app
├── requirements.txt   # Python dependencies
└── README.md
```

## Notes and limitations

- Scanned or image-only resumes cannot be read. An ATS cannot read them either, so export a text-based PDF or use DOCX.
- Resume text is sent to Google's Gemini API. Do not upload documents you are not comfortable sharing.
- If a model name is retired, change it in the sidebar or set `GEMINI_MODEL`.
- Free API keys have rate limits; wait a minute and retry if you hit one.
