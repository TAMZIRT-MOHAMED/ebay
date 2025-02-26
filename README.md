# eBay Scraper
![Neutral Creative Professional LinkedIn Article Cover Image (1)](https://github.com/user-attachments/assets/3bbbabb3-8602-4301-a64c-b6f826338b44)

## Description
This project is a web scraper for extracting product listings from eBay's Electronics category. It uses Python's `requests` and `BeautifulSoup` libraries to fetch and parse data from eBay. The scraper navigates eBay's product listing pages, collects relevant product URLs, and extracts detailed information such as product names, prices, and availability.

Additionally, the project implements a structured data pipeline that processes and stores the extracted data in a MySQL database using SQLAlchemy. The stored data can be further visualized and analyzed using Jupyter Notebook.

## Features
- **Web Scraping**: Extracts product URLs from eBay's Electronics section.
- **Detail Extraction**: Collects product information including name, price, and description.
- **Robust Requests**: Implements retry logic to handle network issues and avoid IP blocking.
- **Data Transformation**: Uses `pandas` to clean and prepare data.
- **Flexible Storage**: Saves data in multiple formats (CSV, JSON, or MySQL).
- **Database Integration**: Utilizes SQLAlchemy for efficient MySQL database management.
- **Visualization**: Enables data exploration and visualization through Jupyter Notebook.
- **Extensibility**: Easy to modify for scraping additional categories or data fields.

## Requirements
Ensure you have the following Python libraries installed:
```sh
pip install requests beautifulsoup4 lxml pandas mysql-connector-python SQLAlchemy jupyter
```

## Usage
1. **Clone the repository**:
    ```sh
    git clone https://github.com/yourusername/ebay-scraper.git
    cd ebay-scraper
    ```

2. **Run the scraper**:
    Open the `ebayscraping.ipynb` Jupyter Notebook and execute the cells to run the scraper and process the data.

3. **Database Configuration**:
    Ensure you have a MySQL database set up and update the database connection details in the notebook:
    ```python
    username = 'root'
    password = urllib.parse.quote_plus('YourPassword')
    host = 'localhost'
    port = '3306'
    database = 'ebayData'
    ```

4. **Data Visualization**:
    Use the provided visualization cells in the notebook to explore and analyze the scraped data.

## Example
Here is an example of how to run the scraper and store the data in a MySQL database:
```python
import warnings
warnings.filterwarnings('ignore')
from sqlalchemy import create_engine, Text, Date, Float, Integer
import pandas as pd
import urllib.parse

username = 'root'
password = urllib.parse.quote_plus('YourPassword')
host = 'localhost'
port = '3306'
database = 'ebayData'

dtype = {
    'name': Text(),
    'price_(USD)': Float,
    'stock': Integer,
    'Sold': Integer,
    'date_status': Date
}

engine = create_engine(f"mysql+mysqldb://{username}:{password}@{host}:{port}/{database}")

conn = engine.connect()

data = pd.read_csv("data.csv")

data['date_status'] = pd.to_datetime(data['date_status'], format='%Y-%m-%d').dt.strftime('%Y-%m-%d')

data.to_sql('electronic', engine, index=False, if_exists='append', dtype=dtype)
conn.close()
```

## License
This project is licensed under the MIT License. See the [LICENSE.md](LICENSE.md) file for details.

---

*Created by [TAMZIRT MOHAMED]*
