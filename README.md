# News-Feed-Parser 
Project Documentation: RSS News Feed Parser
1. Overview
The RSS News Feed Parser project is designed to collect and categorize news articles from various RSS feeds, store them in a MySQL database, and export them to a CSV file. The key goals of this project are:

Parse news articles from different RSS sources.
Classify the news articles into specific categories using simple natural language processing (NLP).
Store the processed articles in a MySQL database.
Export the final results into a CSV file for analysis or submission.
2. Implemented Logic
The project consists of the following key steps:
Step 1: Parsing RSS Feeds
feedparser Library: The feedparser library is used to parse RSS feeds from various URLs. It fetches the title, summary, published date, and link for each article.
Multiple Feeds: The system is designed to handle multiple feeds at once. For each URL in the feeds list, it fetches the feed entries and processes them.

Step 2: Data Cleaning & Processing
Date Parsing: The publication date, which is originally in string format, is converted into a Python datetime object. This ensures correct date formatting when saving to the database.

Error Handling: If a feed URL is invalid or inaccessible, it logs the error and continues with the next URL to prevent the process from failing completely.

Null Checks: Before processing, the script checks that each article contains all the required fields (title, summary, published, and link). If any of these are missing, the entry is skipped.

Step 3: Categorizing Articles Using NLP
spaCy Library: The spaCy library is used for basic natural language processing (NLP). It helps analyze the content of the article and classify it into one of the predefined categories.

Category Rules: The content of each article is scanned for certain keywords to categorize it:

Terrorism / Protest / Political Unrest / Riot: Articles containing keywords like "terrorism", "protest", or "riot".
Positive / Uplifting: Articles containing keywords related to positive or uplifting content.
Natural Disasters: Articles mentioning disasters, floods, or earthquakes.
Others: Articles that do not fall under the above categories are marked as "Others".
Step 4: Storing Data in MySQL
SQLAlchemy ORM: The project uses SQLAlchemy as an ORM (Object Relational Mapper) to manage interactions with the MySQL database. This allows seamless integration between Python and MySQL, reducing the need for raw SQL queries.

Database Table Design: The news_articles table contains the following columns:

id (Primary Key): A unique identifier for each article, using the source_url.
title: The title of the article.
content: A summary or the main content of the article.
publication_date: The publication date and time.
source_url: The URL to the article.
category: The category assigned to the article based on content analysis.
Step 5: Exporting Data to CSV
Pandas Library: After the articles are processed, the pandas library is used to convert the list of articles into a DataFrame. This DataFrame is then exported to a CSV file named news_articles.csv.

CSV Structure: The CSV contains the following columns: id, title, content, publication_date, source_url, and category. Each row represents an article.

3. Design Choices
Choice of Tools and Libraries
feedparser: Chosen for its ease of use when working with RSS feeds. It abstracts away the complexities of parsing different RSS formats and provides a consistent interface.

spaCy: The NLP functionality is powered by spaCy, which is lightweight and fast for the purpose of basic keyword-based text classification.

SQLAlchemy ORM: SQLAlchemy was selected to simplify database interactions by mapping Python objects to database tables. This makes it easier to manage data without writing raw SQL queries.

pandas: Chosen for its powerful data manipulation capabilities. It allows for an easy and efficient way to convert the processed articles into CSV format.

Error Handling and Robustness
Feed Errors: The script is designed to handle unreachable or invalid feeds. If a feed cannot be accessed, the error is logged, and the script proceeds to the next feed, ensuring that the process is not halted.

Null Data: Each article is validated before processing, and entries with missing fields are skipped. This prevents incomplete data from being stored in the database or CSV file.

Scalability Considerations
Multiple Feeds: The system is designed to handle multiple RSS feed sources. It can easily scale by adding more feeds to the list without needing significant changes to the logic.

Database Interaction: Using SQLAlchemy ensures that the database interaction is scalable and can be expanded in the future to support more complex queries, relationships, and data analysis.

Efficiency and Performance
Batch Processing: Articles are processed in batches, which reduces the overhead of interacting with the database for each individual article.

Simple Categorization: The categorization logic is based on keyword matching, which ensures fast and efficient classification without requiring advanced machine learning models.

4. Limitations
Basic Categorization: The categorization algorithm is based on simple keyword matching, which may not be as accurate as more sophisticated machine learning techniques. It could misclassify articles if the keywords are ambiguous or used out of context.

RSS Feed Dependency: The system depends on the availability and structure of external RSS feeds. If the feeds change format or become unavailable, the system might not work as expected.

5. Conclusion
The RSS News Feed Parser project effectively collects and processes news articles from multiple RSS feeds, categorizes them, and stores them in a MySQL database before exporting them to a CSV file. It is designed with simplicity, scalability, and performance in mind, making it easy to extend and modify for future needs.

