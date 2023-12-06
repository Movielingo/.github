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

![vocab_app-Page-1 drawio(3)](https://github.com/Movielingo/.github/assets/64266832/04fec50e-78e4-4fb7-91b1-2e2d94ca1be2)


### Design Decisions
1. Optimized Data Retrieval Strategy
- To achieve this we've minimized the use of sub-collections. This approach allows us to retrieve all necessary data through a single query to a primary collection, enhancing efficiency and reducing complexity.
- We tried to minimize the amount of database queries needed. As a rule of thumb, we aimed to have 1 query per screen.

2. Handling Seasons and Episodes in Series
- For managing seasons and episodes within a series, we came up with the following approach:

- **Integrated Seasons Field**: Instead of creating separate sub-collections for each season or episode, we've incorporated an episodeDetails field directly within the series document. This field is an array of maps. Every map entry stores additional information for each season's episode.

- **Centralized Vocabulary Collection**: The vocabularies for all seasons and their respective episodes are stored in a single, series-specific vocabulary collection. This design simplifies data management and storage by enabling us to retrieve needed vocabulary using only a single query.

- **Composite Index for Specific Retrieval**: When a user decides to learn a specific movie or series episode, the respective vocabulary is stored in the user's subcollection named "UserVocabularies". All vocabulary from different series and movies is stored in the same collection, allowing us to handle requests like "get all users' due vocabulary" with a single database query using composite indexes.

3. Handling Users who want to learn multiple languages and Users who have different mother tongues
- For every language that a user can learn with our app we created a separate media collection. We store the vocabulary for users with different mother tongues (translation language) in the same media collection.
- We store all the different translation languages that we offer for a media item in the media document as an array.
- This allows us to filter media collections and vocabularies effectively without having to run queries on multiple different collections and still being able to filter for media language, language level, media title and media genres.
   

5. Handling Full-Text Search
- In order to avoid relying on additional external paid services to perform a full-text search when a user wants to search movies by title, we implemented a 'semi-full-text-search' using trigrams.
- A trigram is a group of three consecutive characters taken from a string. For instance, the string "Hello" would be broken down into trigrams as ['Hel', 'ell', 'llo'].
- Each record in your database stores its trigram representation of the media title. When a search query is made, the search string is also converted into trigrams. The system then checks if the trigrams of the search string are present in the trigrams of the records. As Firestore creates an index for every document top-level-field, we can ensure that the search is efficient.

## 📋 Contribution List

#### CRUD operations
- user_service (Constantin)
  - firebase authentication
  - create user
  - get user information from firebase authentication
  - get user
  - delete user
  - update user
- media_service (emely)
  - get media by id
  - get all media by translation language => optional genres filter 
  - get all movies by translation language => optional genres filter 
  - get all series by translation language => optional genres filter 
  - get movie vocabulary by language level, translation language
- user_media_service (emely, constantin)
  - add episode to user media collection
  - add movie to user media collection
  - get user's media
  - update user's media progress
  - get due vocabulary session for user's media
  - get total amount of users due vocabulary for the day
  - update user's vocabulary
  

#### Advanced Queries/ Writes (emely)
- search media by title => using trigrams to not have to use a paid service for full-text search
- save >1000 vocabularies entries using batch writes => when creating media doc and when adding media to user
- get total amount of user's due vocabularies by using composite indexe
- get vocabulary session for user's media by using composite indexe
- updating user vocabularies by using transactions

## :envelope: Contact

For more information, feel free to [contact us](mailto:constantin.unterkofler@code.berlin).

**Happy Learning & Watching! :tv: :books:**

