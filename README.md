# Book Scraper Project  

## Overview  
This project scrapes book details from [Books to Scrape](http://books.toscrape.com/) using Python.  
By analyzing pricing trends, ratings, and stock availability, we can understand book market dynamics and pricing strategies.  

## Objective  
- Extract **Title, Pricing, Availability, and Product URL** for approximately 1,000 books.  
- Store data in a structured CSV file (`books_data.csv`).  
- Implement error handling to manage missing data and HTTP failures.  
- Validate extracted data using a testing framework.  

## Technologies Used  
- **Programming Language**: Python  
- **Web Scraping**: Requests, BeautifulSoup  
- **Data Handling**: Pandas  
- **Logging**: Python’s logging module  
- **Storage**: CSV  

## Business Flow  
1️⃣ **Initiate Scraping** – Start from page one.  
2️⃣ **Send HTTP Request** – Validate the status code.  
3️⃣ **Extract Data** – Scrape details including title, pricing, rating, availability, and URL.  
4️⃣ **Handle Pagination** – Keep scraping until no more books exist.  
5️⃣ **Log Errors** – Record issues with HTTP failures and missing fields.  
6️⃣ **Store Data** – Save extracted results in `books_data.csv`.  
7️⃣ **Perform Testing** – Ensure accuracy through structured validation.  

## Implementation and Code Structure  
### Key Functions  
- `fetch_page(url)`  
   - Sends an HTTP request  
   - Validates response success  
   - Handles exceptions  
- `process_books(book_list, books)`  
   - Extracts book details  
   - Structures data into a dictionary  
   - Manages rating conversion  
- `scrape()`  
   - Iterates through all pages  
   - Calls helper functions  
   - Stops execution on failure  
- `save_to_csv(books)`  
   - Converts data into a **structured DataFrame** using Pandas  
   - Saves output into `books_data.csv`  

## Error Handling  
- **Missing Data** – If a book lacks price or rating, it's skipped and logged for review.  
- **HTTP Errors** – The scraper retries failed requests up to **3 times** before skipping the page.  
- **Unexpected Rating Format** – Defaults to `None` and records the issue in logs.  
- **Empty Pages** – Stops pagination when no books are found to avoid infinite loops.  

## Data Storage Structure (`books_data.csv`)  
| Title                   | Price  | Rating | Availability | Product URL                     |  
|-------------------------|--------|--------|--------------|---------------------------------|  
| A Light in the Attic    | 51.77  | Three  | In stock     | `a-light-in-the-attic_1000/index.html` |  
| Mystery Novel           | N/A    | Four   | Out of stock | `mystery-novel_2001/index.html` |  

## Testing and Validation  
### Test Cases Covered  
1. **Verify CSV File Exists** (`os.path.isfile("books_data.csv")`).  
2. **Confirm Correct File Format** (`.csv`).  
3. **Validate Column Structure** (Title, Price, Rating, Availability, URL).  
4. **Ensure Correct Data Types** (Price stored as `float`).  
5. **Handle Missing or Invalid Data** (`df.isnull().sum()`).  

## Challenges and Solutions  
1. **Handling Timeouts** – Added request timeout (`timeout=10`).  
2. **Rating Conversion Errors** – Used dictionary mapping (`One -> 1, Two -> 2`).  
3. **Avoiding Crashes** – Wrapped functions in try-except blocks to prevent failures.  

