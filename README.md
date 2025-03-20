# Goodreads data analysis

Anonymized user and books data has been obtained from [this](https://huggingface.co/datasets/liyucheng/goodreads)
HuggingFace repository. Files are in the parquet format. Queries are performed using the Python 
[Polars](https://docs.pola.rs/) DataFrame library.

## Schema

- books/\*.parquet
```
Schema([('book_id', String),
        ('title', String),
        ('isbn13', String),
        ('isbn', String),
        ('author_ids', List(String)),
        ('author_names', List(String)),
        ('average_rating', String),
        ('ratings_count', String),
        ('text_reviews_count', String),
        ('publication_year', String),
        ('publication_month', String),
        ('publication_day', String),
        ('publisher', String),
        ('language_code', String),
        ('description', String),
        ('genres', List(String)),
        ('num_pages', String),
        ('format', String),
        ('work_id', String),
        ('original_title', String),
        ('original_publication_year', String),
        ('original_language_id', String)])
```

- behavior/\*parquet
```
Schema([('user_id', String),
        ('book_id', String),
        ('is_read', Boolean),
        ('rating', Int64),
        ('date_added', String),
        ('date_updated', String),
        ('read_at', String),
        ('started_at', String),
        ('reading_duration_days', Float64),
        ('review_text', String),
        ('n_votes', Int64),
        ('n_comments', Int64)])
```

## Examples

```
books_folder = "goodreads/books/*.parquet"
behavior_folder = "goodreads/behavior/*.parquet"

def shape_query_1(folder):

    q1 = (
        pl.scan_parquet(folder,
                        glob = True
                       )
          .select("book_id")
          .count()        
    )

    return q1.collect()

# shape_query_1(books_folder)
# Result: 2360655

# shape_query_1(behavior_folder)
# Result: 228648342
```
