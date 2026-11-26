# NLP Study Assistant

A Streamlit study assistant for university and high-school students (Arabic and English). It answers questions, summarizes, explains, quizzes and debugs code, and can read study material from PDFs and images. Powered by **Llama 3.3 70B** through the Groq API.

**Stack:** Python, Streamlit, Groq API (llama-3.3-70b-versatile), PyMuPDF, Tesseract OCR

## Features
- **Shortcut commands:** `/summarize`, `/explain`, `/quiz`, `/keypoints`, `/debug`. Each expands into a task-specific prompt with its own temperature and token limit.
- **File input:** upload a PDF (text extraction with PyMuPDF) or an image (OCR in English and Arabic). Extracted text is checked for quality and a warning is shown if it looks garbled.
- **Chat memory:** 10-turn sliding window kept in the session.
- **Reliability:** a 30 requests/minute sliding-window rate limiter and retry with exponential backoff on 429 and 5xx errors (up to 3 attempts), plus a batch handler for large request lists.
- **Output validation:** checks that a response is non-empty, well-formed and relevant to the question.
- **Tracing:** every request is logged (action, latency, success) in a collapsible panel, with a prompt debugger that shows exactly what was sent to the model.
- **Dark academic UI** built with custom CSS.

## Run it
```bash
pip install -r requirements.txt
# Tesseract OCR must be installed on your system (with the Arabic language pack for Arabic images)
streamlit run app.py
```
Paste your own Groq API key in the sidebar. The key is only held in the session and is never stored in the code.
