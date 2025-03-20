# Goodreads data analysis

Anonymized user and books data has been obtained from [this](https://huggingface.co/datasets/liyucheng/goodreads)
HuggingFace repository. Files are in the parquet format. Queries are performed using the Python 
[Polars](https://docs.pola.rs/) DataFrame library.

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
