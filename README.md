# Book Market Analysis: Data-Driven Insights for Book App Startups

## 📌 Project Overview
The COVID-19 pandemic significantly shifted global daily routines. With lockdowns restricting outdoor leisure activities like visiting cafes and shopping malls, many turned to reading as their primary hobby. This sudden surge in book consumption caught the attention of startups racing to develop new digital products for book lovers.

This project analyzes a relational database from a competing platform in the book application market. The goal is to extract key data insights regarding book popularity, publisher output, author performance, and user engagement metrics. These insights will serve as the strategic foundation for a data-driven value proposition for a new digital book product.

---

## 📊 Data Architecture & Schema
The project uses a relational database consisting of 5 tables:

*   **`books`**: Core book catalog details (`book_id`, `author_id`, `title`, `num_pages`, `publication_date`, `publisher_id`).
*   **`authors`**: Information on book creators (`author_id`, `author`).
*   **`publishers`**: Publishing house metadata (`publisher_id`, `publisher`).
*   **`ratings`**: Structured user ratings data (`rating_id`, `book_id`, `username`, `rating`).
*   **`reviews`**: Unstructured qualitative user text reviews (`review_id`, `book_id`, `username`, `text`).

---

## 🛠️ Tech Stack & Workflow
The workflow seamlessly integrates Python and SQL to handle data extraction:
*   **Language:** Python 3
*   **Libraries:** `pandas` (for data manipulation and presentation)
*   **Database Connectivity:** `sqlalchemy` (via a secure `postgresql` connection)

### SQL Execution Wrapper
To optimize the analytics workflow, a helper function was created to seamlessly stream SQL queries directly into Pandas DataFrames:

```python
import pandas as pd
from sqlalchemy import create_engine

# Database connection configuration (Credentials hidden for security)
db_config = {
    'user': 'practicum_student',
    'pwd': 'HIDDEN_PASSWORD',
    'host': 'rc1b-wcoijxj3yxfsf3fs.mdb.yandexcloud.net',
    'port': 6432,
    'db': 'data-analyst-final-project-db'
}

connection_string = 'postgresql://{}:{}@{}:{}/{}'.format(
    db_config['user'], db_config['pwd'], db_config['host'], db_config['port'], db_config['db']
)

engine = create_engine(connection_string, connect_args={'sslmode': 'require'})

# Helper function for quick SQL execution
def consult_sql(query):
    return pd.io.sql.read_sql(query, con=engine)