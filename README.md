# FlavorFinder

A full-stack recipe discovery platform built for CS547: Information Retrieval at Worcester Polytechnic Institute (WPI). FlavorFinder combines classical information retrieval techniques with modern machine learning to enable advanced recipe search and personalized recommendations.

## About the Project

FlavorFinder lets users search a large recipe dataset by ingredients, tags, or recipe names and returns ranked results using multiple retrieval and recommendation strategies. Users can sign into a profile to receive personalized recommendations based on their history, or receive average-based suggestions as a guest.

## Team Members

- **Alex Mitchell**
- **Keon**
- **Shipra**
- **Parth Shroff**

## My Contributions

I was responsible for the machine learning and ranking components of the system:

**TF-IDF Embeddings and Ranked Retrieval**
Built the TF-IDF vectorization pipeline using scikit-learn and NLTK to transform recipe text fields (ingredients, tags, descriptions) into embeddings. These embeddings power the ranked retrieval layer that scores and orders the top 1,000 matching recipes for any search query.

**Collaborative Filtering**
Built a collaborative filtering matrix using user interaction history to identify similar users and surface recipes that users with similar taste profiles rated highly. This powers the profile-based recommendation path when a user is signed in.

## Tech Stack

| Layer | Technology |
|---|---|
| Web Framework | Django 4.2 |
| ML / Recommendations | TensorFlow 2.15, TensorFlow Recommenders 0.7.3 |
| Information Retrieval | scikit-learn, NLTK, TF-IDF |
| Collaborative Filtering | scipy, pandas, numpy |
| Database | SQLAlchemy / Django ORM |
| Language | Python 3.x, Jupyter Notebook |

## Architecture

The system runs four separate components that must be initialized before starting the server:

1. **Boolean search index** (`search_creation_script.py`) — builds the inverted index over the recipe dataset
2. **TF-IDF embeddings** (`lr_content_based.py`) — generates document embeddings for ranked retrieval
3. **Neural network model** (`cs547ModelAndPred.ipynb`) — trains and serializes the recommendation model
4. **Collaborative filtering matrix** (`cfiltering.ipynb`) — computes the user similarity matrix

At query time, the Django application combines these components: the search engine retrieves candidate recipes matching the query, the selected ranking algorithm (TF-IDF similarity, neural network prediction, or collaborative filtering) scores the candidates, and the top 1,000 results are returned to the user. A time slider further filters results by preparation time.

## Setup

**Install dependencies**

```bash
pip install -r requirements.txt
```

**Initialize all data components** (run in order)

```bash
python search_creation_script.py      # Boolean search index
python lr_content_based.py            # TF-IDF embeddings
# Run cs547ModelAndPred.ipynb         # Neural network model
# Run cfiltering.ipynb                # Collaborative filtering matrix
```

**Run the Django server**

```bash
python manage.py makemigrations
python manage.py migrate
python manage.py runserver
```

The server will be available at `http://127.0.0.1:8000`.

## Usage

- Enter any combination of ingredients, tags, or recipe names into the search bar
- Select a ranking algorithm from the dropdown (Boolean, TF-IDF, Neural Network, Collaborative Filtering)
- Use the time slider to filter by preparation time
- Sign in to a profile to enable personalized collaborative filtering recommendations
- Guest users receive recommendations based on average user ratings

## Course

CS547: Information Retrieval, Worcester Polytechnic Institute, Fall 2023
