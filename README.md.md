# Student Support RAG & Monitoring System

A full-stack Retrieval-Augmented Generation (RAG) assistant designed for student support, equipped with a comprehensive online monitoring and evaluation pipeline[cite: 1]. 

## 🌟 Overview

Offline evaluation can only tell you so much before your system meets real users[cite: 1]. This project bridges that gap by implementing **online monitoring**—capturing live chat traffic, persisting conversations to a database, tracking token costs, evaluating response quality using an automated LLM-as-a-judge, and visualizing performance metrics on real-time dashboards[cite: 1].

## ✨ Key Features

* **RAG Chat Application:** Built with Streamlit[cite: 1] to provide an interactive student-support assistant backed by a local FAQ dataset[cite: 1].
* **Automated Evaluation (LLM-as-a-Judge):** Automatically scores generated answers for correctness, groundedness, and relevance against retrieved context after each query[cite: 1].
* **Request & Cost Tracking:** Captures detailed metadata (`LLMCallRecord`) for token usage, latency, and operational costs[cite: 1].
* **Database Persistence:** Stores complete chat history, metrics, and user feedback (thumbs up/down) in a PostgreSQL database[cite: 1].
* **Real-Time Dashboards:** Features both a built-in Streamlit monitoring view[cite: 1] and a fully provisioned Grafana dashboard[cite: 1] for visual analytics.
* **Flexible Execution & Deployment:** Fully containerized using Docker Compose[cite: 1] for local multi-service orchestration, with support for local Python execution[cite: 1] and cloud deployment[cite: 1].

## 🛠️ Tech Stack

* **Frontend & UI:** Streamlit[cite: 1]
* **Database & Storage:** PostgreSQL[cite: 1] (Dockerized / Container volumes[cite: 1])
* **Monitoring & Visualization:** Grafana[cite: 1], custom Streamlit dashboard[cite: 1]
* **Environment & Package Management:** Python, `uv`[cite: 1]
* **Infrastructure:** Docker Compose[cite: 1]

---

## 🚀 Getting Started

To run this project locally, via Docker Compose, or deploy it to the cloud, see the step-by-step [HOW-TO-RUN.md](HOW-TO-RUN.md) guide.