# Student Support RAG & Monitoring System

A full-stack Retrieval-Augmented Generation (RAG) assistant for student support, featuring a comprehensive online monitoring and evaluation pipeline.

## 🌟 Overview

Offline evaluation only tells part of the story before a system is exposed to real users. This project closes that gap by adding **online monitoring**: it captures live chat traffic, persists conversations to a database, tracks token usage and operational costs, evaluates answer quality with an automated LLM-as-a-judge, and visualizes system performance through real-time dashboards.

## ✨ Key Features

* **RAG Chat Application:** Built with Streamlit to provide an interactive student-support assistant backed by a local FAQ dataset.
* **Automated Evaluation (LLM-as-a-Judge):** Scores generated answers for correctness, groundedness, and relevance against retrieved context after each query.
* **Request & Cost Tracking:** Captures detailed metadata (`LLMCallRecord`) including token usage, latency, and operational cost.
* **Database Persistence:** Stores complete chat history, metrics, and user feedback (thumbs up/down) in a PostgreSQL database hosted on Neon.
* **Monitoring & Dashboards:** Uses the Neon Console to monitor the PostgreSQL database, alongside a built-in Streamlit monitoring interface and a Grafana dashboard for application analytics.
* **Flexible Execution & Deployment:** Fully containerized with Docker Compose for local multi-service orchestration, while also supporting local Python execution and cloud deployment.

## 🛠️ Tech Stack

* **Frontend & UI:** Streamlit
* **Database & Storage:** PostgreSQL hosted on Neon
* **Monitoring & Visualization:** Neon Console (database monitoring), Grafana, custom Streamlit dashboard
* **Environment & Package Management:** Python, `uv`
* **Infrastructure:** Docker Compose

---

## 🚀 Getting Started

To run this project locally, via Docker Compose, or in the cloud, follow the step-by-step guide in [HOW-TO-RUN.md](HOW-TO-RUN.md).
