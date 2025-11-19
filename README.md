Personalized News Feed Ranking System

This repository contains an end-to-end implementation of a personalized news ranking system. The project includes data preparation, embedding generation, model training, and a production-style inference API capable of ranking articles for any user.

This project is structured to reflect real workflows in ML engineering, including modularized pipelines, serialized models, and a serving layer.

⸻

Features
	•	User and article embeddings using TF-IDF and PCA
	•	Click-through prediction model using LightGBM
	•	Training pipeline that builds embeddings, trains the ranker, and saves artifacts
	•	FastAPI inference service for real-time recommendations
	•	Modular and production-oriented code structure
	•	Easy to extend to deep learning, vector databases, or large-scale data

⸻

Project Structure

news_ranker/
│
├── data/
│   ├── users.csv
│   ├── articles.csv
│   └── interactions.csv
│
├── models/
│   ├── embed_model.pkl
│   └── ranker.pkl
│
├── src/
│   ├── prepare_data.py
│   ├── embedding_model.py
│   ├── ranker.py
│   ├── train_pipeline.py
│   └── serve.py
│
├── requirements.txt
└── README.md


⸻

Dataset Format

users.csv

user_id,age,location
1,25,US
2,32,UK

articles.csv

article_id,title,category
101,"AI beats humans","tech"
102,"Sports season highlights","sports"

interactions.csv

user_id,article_id,clicked
1,101,1
1,102,0
2,101,0

The interaction file represents binary click feedback used to train the ranking model.

⸻

Installation

Clone the repository:

git clone https://github.com/yourusername/news_ranker.git
cd news_ranker

Install dependencies:

pip install -r requirements.txt


⸻

Training the Model

Run the full training pipeline:

python src/train_pipeline.py

This will:
	1.	Load CSV data
	2.	Generate article embeddings
	3.	Build user embeddings
	4.	Train the ranking model
	5.	Save serialized models to models/

⸻

Running the Inference API

Launch the FastAPI server:

uvicorn src.serve:app --reload

Example request:

GET http://127.0.0.1:8000/recommend/1?top_k=5

Example response:

{
  "user_id": 1,
  "recommendations": [
    [101, 0.84],
    [102, 0.22]
  ]
}


⸻

How It Works

Embeddings

Articles are encoded using TF-IDF followed by PCA dimensionality reduction.
User embeddings are computed as the mean of embeddings of clicked articles.

Ranking Model

LightGBM is used to estimate the probability that a user will click on each article.
The service returns the highest scoring articles for a given user.

⸻

Extending the Project

This project can be expanded in several useful ways:
	•	Replace TF-IDF with transformer embeddings
	•	Add vector search using FAISS or Milvus
	•	Implement negative sampling to improve model robustness
	•	Add session-based or sequence-based ranking models
	•	Deploy the service using Docker or Kubernetes
	•	Schedule batch scoring using Airflow or Prefect

⸻

License

This project is available under the MIT License.

⸻
