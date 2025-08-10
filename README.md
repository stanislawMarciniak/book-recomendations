# Semantic Book Recommender

A sophisticated book recommendation system that uses machine learning to classify books, analyze emotions, and provide semantic search capabilities through natural language queries.

## Overview

This project creates an intelligent book recommendation system by combining multiple AI techniques:
- **Text Classification**: Automatically categorizes books as Fiction/Nonfiction
- **Emotion Analysis**: Extracts emotional profiles from book descriptions
- **Semantic Search**: Enables natural language queries using vector embeddings
- **Interactive Dashboard**: Gradio-based web interface for book discovery

## Features

- 🔍 **Semantic Search**: Find books using natural language descriptions
- 📚 **Smart Categorization**: Automatic Fiction/Nonfiction classification
- 😊 **Emotion-Based Filtering**: Sort recommendations by emotional tone (Happy, Suspenseful, Sad, etc.)
- 🎨 **Interactive UI**: Clean, modern web interface built with Gradio
- 📊 **Rich Metadata**: Complete book information with covers, authors, and descriptions

## Demo

The system accepts queries like:
- "A story about forgiveness and redemption"
- "Books to teach children about nature"
- "Mystery novels set in Victorian England"
- "Self-help books for personal growth"

## Dataset

**Source**: Kaggle books dataset (6,810+ books)  
**Final Dataset**: 5,197 high-quality books after cleaning and filtering  
**Features**: 
- Book metadata (title, authors, ratings, publication info)
- Automatically generated categories
- Emotional profiles (7 dimensions: joy, anger, fear, sadness, surprise, disgust, neutral)
- Semantic embeddings for similarity search

## Architecture

### Data Processing Pipeline

1. **Data Exploration & Cleaning** (`data-exploration.ipynb`)
   - Downloaded and analyzed Kaggle dataset
   - Removed books with missing critical data
   - Filtered for descriptions with 25+ words
   - Created enhanced features and saved as `books_cleaned.csv`

2. **Text Classification** (`text-classification.ipynb`)
   - Used Facebook's BART-large-mnli for zero-shot classification
   - Achieved 77.8% accuracy on Fiction vs. Nonfiction classification
   - Applied to 1,454 books missing category labels
   - Output: `books_with_categories.csv`

3. **Emotion Analysis** (`sentiment-analysis.ipynb`)
   - Applied DistilRoBERT model for emotion classification
   - Analyzed 7 emotion categories across all book descriptions
   - Sentence-level analysis with maximum score aggregation
   - Output: `books_with_emotions.csv`

4. **Vector Search Setup** (`vector-search.ipynb`)
   - Created Chroma vector database with OpenAI embeddings
   - Implemented semantic similarity search
   - Built reusable recommendation function

### Application Components

- **Backend**: Flask application with Gunicorn server
- **Frontend**: Gradio dashboard with modern Glass theme
- **Search Engine**: Chroma vector database with OpenAI embeddings
- **Deployment**: Docker containerized for easy deployment

## Installation

### Prerequisites
- Python 3.9+
- OpenAI API key
- Required packages (see `requirements.txt`)

### Setup

1. **Clone the repository**
```bash
git clone git@github.com:stanislawMarciniak/book-recomendations.git
cd book-recomendations
```

2. **Install dependencies**
```bash
pip install -r requirements.txt
```

3. **Set up environment variables**
```bash
# Create .env file
echo "OPENAI_API_KEY=your_openai_api_key_here" > .env
```

### Running the Application

**Local Development**
```bash
python gradio-dashboard.py
```

## Usage

1. Navigate to the application URL
2. Enter a description of what you're looking for
3. Optional: Filter by category and emotional tone
4. Click "Find recommendations" to see results
