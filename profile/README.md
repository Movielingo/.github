# Movielingo :movie_camera: :book:

## :bulb: Introduction

**Movielingo** aims to revolutionize the way we learn languages. Ever found yourself binge-watching Netflix and wishing you could combine that with something productive, like learning a new language? Look no further! Movielingo combines language learning with movies and Netflix shows, to create an educational experience that's not just effective, but also fun and engaging!

Movilingo is a vocabulary-learning app based on movies. Our target group are people who want to improve their skills in a new foreign language. Ideally, they already have basic knowledge (A1) but not enough vocabulary to follow their favourite movie in a foreign language. The idea of the app is that users specifically learn the vocabulary that appears in the movie and that they do not yet know to understand the movie better. With this learning method, users increase their vocabulary and benefit from the advantages of passive learning.

A user should learn the vocabulary according to the [spaced repetition system](https://en.wikipedia.org/wiki/Spaced_repetition). Spaced repetition helps to remember words by showing them to a user at increasing intervals. Words a user struggles with appear more often, while familiar ones are reviewed less frequently. This optimized scheduling enhances your long-term memory, making it easier to recall words when needed.

## :dart: Why Movielingo?

* **Passive Learning**: Benefit from passive learning techniques to enhance language retention.
* **Spaced Repetition**: Benefit from the spaced repetition system which is the most effective technique to bring vocabulary into long-term memory.
* **Engaging Content**: Who says education can't be entertaining? Learn while you watch your favorite shows.
* **Ease of Use**: Simple and intuitive UI/UX, making it accessible for learners of all ages.
* **Open Source**: Movielingo is open source and therefore accessible to everyone.

## :gear: Technology Stack

* Flutter
* Firebase
* Python
* Spacy.io

## 🛠️ Repositories
- [Movielingo App](https://github.com/Movielingo/movielingo_app)
- [Vocabulary Service](https://github.com/Movielingo/VocabularyService)

## 💾 Database

![vocab_app-DB drawio](https://github.com/Movielingo/.github/assets/50672977/b8da2486-24d1-4dce-bba0-8e44482912ed)

### Design Decisions
1. Optimized Data Retrieval Strategy
- To achieve this we've minimized the use of sub-collections. This approach allows us to retrieve all necessary data through a single query to a primary collection, enhancing efficiency and reducing complexity.

2. Handling Seasons in Series
- For managing seasons within a series, we've adopted a unique approach:

- **Integrated Seasons Field**: Instead of creating separate sub-collections for each season, we've incorporated a seasons field directly within the series document. This field is a Map, an embedded object in the series document where we store additional information for each season's episode.

- **Centralized Vocabulary Collection**: The vocabularies for all seasons and their respective episodes are stored in a single, series-specific vocabulary collection. This design simplifies data management and storage by enabling us to retrieve needed vocabulary using only a single query.

- **Composite Index for Specific Retrieval**: We've implemented a `Composite Index`, named ”seriesVocabularySearchIndex”. This index allows for precise retrieval of vocabulary based on the series, season, episode, and language level.

- This strategic design enables us to maintain all series vocabularies in one sub-collection while still offering targeted access to vocabularies for specific seasons, episodes, and language levels.

3. Handling Full-Text Search
- In order to avoid relying on additional external paid services to perform a full-text search when a user wants to search movies by title, we implemented a 'semi-full-text-search' using trigrams.
- A trigram is a group of three consecutive characters taken from a string. For instance, the string "Hello" would be broken down into trigrams as ['Hel', 'ell', 'llo'].
- Each record in your database stores its trigram representation of the media title. When a search query is made, the search string is also converted into trigrams. The system then checks if the trigrams of the search string are present in the trigrams of the records. As Firestore creates an index for every document top-level-field, we can ensure that the search is efficient.

## 📋 Contribution List

#### Simple CRUD operations
- save user
- get user
- get all media
- filter media by genre/ level
- get movie vocabulary by language level
- get user's media
- update user settings
- delete user
- get movie vocabulary
- update user's vocabulary
- get all learned vocabulary for user
  

#### Advanced Queries/ Writes
- search movie by title => using trigrams to not have to use a paid service for full-text search
- save >1000 vocabulary entries using batch writes
- get all due user's media vocabulary by using composite indexes
- check whether the user already knows a specific word 

## :envelope: Contact

For more information, feel free to [contact us](mailto:constantin.unterkofler@code.berlin).

**Happy Learning & Watching! :tv: :books:**

