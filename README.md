PanicIntel is a multimodal crisis monitoring system built to analyze live news and estimate how serious an event is. Instead of depending on text alone, it combines several signals, including article text, article images, retrieval memory, and sentiment analysis, to produce a final crisis score. The system collects news from RSS feeds and the GDELT API, processes each item through a T5-based text encoder and a ViT-based image encoder, and then merges those features into one shared representation. It also compares the current event with previously stored events using a FAISS-based retrieval memory, which helps the model understand context and similarity with earlier crises. To improve ranking quality, the pipeline includes sentiment scoring and graph-based smoothing so that related events can influence each other slightly. The project is exposed through a FastAPI backend and a browser dashboard, making it easy to view live results and test custom inputs. This makes PanicIntel a strong end-to-end AI project because it combines machine learning, retrieval, web development, and real-time data processing in one system.


## Overview

The goal of PanicIntel is to detect and rank potentially critical news events in real time. Instead of relying only on text, the system uses multiple signals together. It ingests live news from RSS feeds and the GDELT API, extracts article text and images, scores each event with a multimodal model, compares it with similar past events using retrieval memory, and then combines all signals into a final GPI score. This makes the system more context-aware and more useful for crisis monitoring.

## Features

- Live news ingestion from RSS feeds and the GDELT API
- Multimodal scoring with T5 for text and ViT for images
- Retrieval-augmented scoring using FAISS
- Sentiment analysis using VADER
- Final crisis score generation using weighted signal fusion
- Graph-based smoothing across similar events
- FastAPI backend for API access
- Browser dashboard for visualizing results

## Project Structure

- `app.py` - FastAPI application and API endpoints
- `config.py` - model names, device selection, and scoring settings
- `model.py` - multimodal crisis scoring model
- `pipeline.py` - news ingestion, scoring, and final ranking pipeline
- `rag.py` - FAISS-based retrieval memory
- `train.py` - training loop and dataset handling
- `static/index.html` - dashboard interface
- `README.md` - project documentation

## News Sources

The system collects live news from:
- BBC World News RSS
- Reuters World News RSS
- Google News RSS for crisis-related topics
- GDELT Article API

These sources allow the pipeline to work with real-world, up-to-date content instead of a fixed dataset only.

## How It Works

1. The pipeline fetches live articles from RSS feeds and GDELT.
2. Each article is cleaned into a text representation.
3. The image, if available, is downloaded and processed.
4. The multimodal model scores the article using both text and image information.
5. The retrieval system compares the event with similar past events.
6. Sentiment analysis adds another signal.
7. All scores are combined into a final GPI value.
8. Similar events are smoothed together using graph-based propagation.
9. The results are shown in the dashboard and exposed through the API.

## Requirements

- Python 3.10+
- PyTorch
- Transformers
- FastAPI
- Uvicorn
- NumPy
- Requests
- Feedparser
- Pillow
- vaderSentiment
- FAISS

## Installation

Install the required packages:

```bash
pip install torch transformers fastapi uvicorn numpy requests feedparser pillow vaderSentiment faiss-cpu
