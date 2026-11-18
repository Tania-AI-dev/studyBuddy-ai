# Study Buddy — AI-Powered Study Assistant

An AI-powered study assistant that transforms PDF learning materials into interactive flashcards and quizzes using Large Language Models (LLMs), semantic search and Natural Language Processing.

## Overview

Study Buddy helps students study more effectively by automatically generating flashcards from their study materials and evaluating their answers intelligently.

Users can upload PDF documents, generate topic-specific flashcards, revise concepts through interactive flashcards and test their understanding through timed quizzes.

Unlike simple keyword-based quiz applications, Study Buddy combines semantic similarity with LLM-based evaluation to assess whether a student's answer communicates the correct concept, even when the wording differs.

## Features

- **PDF Processing:** Upload PDF documents and extract their text using PyPDF.
- **Text Chunking:** Divide extracted content into manageable chunks with overlapping context.
- **Semantic Search:** Use Sentence Transformers and FAISS to retrieve relevant content based on topic similarity.
- **AI Flashcard Generation:** Generate question-and-answer flashcards using Qwen 2.5 3B Instruct.
- **Duplicate Filtering:** Identify and remove semantically similar questions using embedding similarity.
- **Interactive Revision:** Study with interactive flashcards and review questions and answers.
- **Timed Quizzes:** Test knowledge through timed question-and-answer sessions.
- **Intelligent Answer Evaluation:** Combine embedding similarity and LLM-based judgement to evaluate student responses.
- **Performance Tracking:** Display quiz scores, response times, streaks and questions requiring revision.

## Technology Stack

| Category | Technologies |
|---|---|
| Programming Language | Python |
| Backend | Flask |
| Frontend | HTML, CSS, JavaScript |
| Language Model | Qwen 2.5 3B Instruct |
| Embeddings | Sentence Transformers |
| Vector Search | FAISS |
| NLP Framework | Hugging Face Transformers |
| PDF Processing | PyPDF |
| Deployment / Tunnelling | ngrok |
| Development Environment | Kaggle Notebooks |

## System Architecture

1. **Document Upload:** The user uploads a PDF document through the web interface.
2. **Text Extraction:** PyPDF extracts text from the uploaded document.
3. **Text Chunking:** Extracted text is divided into smaller chunks with overlapping context.
4. **Embedding Generation:** Sentence Transformers (`all-MiniLM-L6-v2`) converts the text chunks into normalized vector embeddings.
5. **Semantic Retrieval:** FAISS performs similarity searches to retrieve relevant chunks when a user specifies a topic.
6. **Flashcard Generation:** Qwen 2.5 3B Instruct generates flashcards from the selected content.
7. **Duplicate Removal:** Embedding similarity is used to filter near-duplicate questions.
8. **Answer Evaluation:** Student answers are evaluated using semantic similarity, with LLM-based judgement for ambiguous cases.

## Intelligent Answer Evaluation

Study Buddy uses a hybrid evaluation strategy rather than relying entirely on embedding similarity.

- Similarity score ≥ 0.90: Answers are accepted as correct.
- Similarity score < 0.35: Answers are classified as incorrect.
- Intermediate similarity scores: The LLM evaluates whether the student's answer conveys the same key idea as the reference answer.

The LLM evaluation also considers factual accuracy and distinctions such as increase versus decrease, true versus false, and before versus after.

## Installation and Execution

This project was developed and tested in Kaggle Notebooks.

### 1. Open the notebook

Import `studybuddy.ipynb` into a Kaggle Notebook.

### 2. Install dependencies

Run the installation cell or install the packages listed in `requirements.txt`.

### 3. Configure ngrok

Create an ngrok authentication token and add it to Kaggle Secrets using the name:

`NGROK_TOKEN`

The notebook retrieves this secret using Kaggle's `UserSecretsClient`.

### 4. Run the notebook

Execute the notebook cells in their original order.

The Flask application starts on port 5000, and ngrok exposes the application through a temporary public URL.

### 5. Start studying

Open the generated ngrok URL to access Study Buddy and upload a PDF document.

**Note:** The current implementation is designed for the Kaggle environment. Running it independently requires adapting Kaggle-specific secret management and the ngrok configuration.

## Technical Highlights

- Semantic retrieval using normalized sentence embeddings and FAISS inner-product similarity.
- Context-aware flashcard generation using an instruction-tuned language model.
- JSON parsing and retry handling for structured LLM outputs.
- Semantic duplicate detection to reduce repetitive flashcards.
- Hybrid answer grading combining vector similarity and LLM reasoning.
- Background processing for document ingestion and flashcard generation.

## Future Improvements

- Add OCR support for scanned PDF documents.
- Introduce persistent storage for uploaded documents and learning progress.
- Add user authentication and personalised learning histories.
- Improve deployment beyond the Kaggle environment.
- Add support for additional document formats.

## Author

Developed as an AI application project exploring the practical integration of Large Language Models, NLP, semantic search and web development.

