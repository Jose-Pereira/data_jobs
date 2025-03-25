# LinkedIn Job Scraper

This project scrapes job listings from LinkedIn based on defined keywords and stores them in a SQLite database and CSV files. It's designed to run automatically via GitHub Actions.

## Features

- Scrapes LinkedIn job listings based on keywords and location
- Automatically detects initial run to gather all active jobs regardless of posting date
- On subsequent runs, focuses only on recently posted jobs
- Filters jobs based on title, description, and language
- Stores results in a SQLite database
- Saves daily job listings as CSV files with timestamps
- Runs automatically via GitHub Actions

## Setup

1. Clone this repository
2. Install dependencies:
   ```
   pip install -r requirements.txt
   ```
3. Copy `config.json.template` to `config.json` and customize your search parameters

## Configuration

Edit `config.json` to customize your job search:

```json
{
  "proxies": {},
  "headers": {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
  },
  "search_queries": [
    {
      "keywords": "data OR analytics OR 'business intelligence'",
      "location": "Costa Rica", 
      "f_WT": ""
    }
  ],
  "title_include": ["data", "analytics", "business intelligence"],
  "title_exclude": [],
  "company_exclude": [],
  "desc_words": [],
  "languages": ["en", "es"],
  "timespan": "r86400",
  "jobs_tablename": "jobs",
  "filtered_jobs_tablename": "filtered_jobs",
  "db_path": "./data/jobs.db",
  "pages_to_scrape": 3,
  "rounds": 1,
  "days_to_scrape": 7
}
```

### Configuration Options

- `proxies`: Proxy settings if needed
- `headers`: HTTP headers for requests
- `search_queries`: List of search queries with keywords and location
  - `f_WT`: Filter for remote work (empty for all, "2" for remote only)
- `title_include`: Keywords to include in job titles
- `title_exclude`: Keywords to exclude from job titles
- `company_exclude`: Companies to exclude from results
- `desc_words`: Words to exclude based on job description
- `languages`: Languages to include (e.g., "en", "es")
- `timespan`: Time period for job listings (r86400 = last 24 hours, r604800 = past week, r2592000 = past month). Used only for non-initial runs.
- `jobs_tablename`: Name of the database table for matched jobs
- `filtered_jobs_tablename`: Name of the database table for filtered jobs
- `db_path`: Path to the SQLite database
- `pages_to_scrape`: Number of pages to scrape per search query
- `rounds`: Number of rounds to run the scraper
- `days_to_scrape`: Maximum age of jobs to include (in days)

## Running Locally

To run the scraper locally:

```
python main.py
```

You can also specify a custom config file:

```
python main.py custom_config.json
```

### Initial Run vs. Subsequent Runs

- **Initial Run**: When first executed (no existing database), the scraper will gather all active job listings regardless of posting date.
- **Subsequent Runs**: After the initial run, the scraper will only collect jobs posted within the timeframe specified by the `timespan` parameter in your config.

## GitHub Actions Automation

This project includes a GitHub Actions workflow that runs the scraper daily and commits the results to the repository. The workflow is defined in `.github/workflows/linkedin_scraper.yml`.

The workflow:
1. Runs daily at 4:00 AM UTC
2. Sets up Python
3. Installs dependencies
4. Creates a config file
5. Runs the scraper
6. Commits and pushes any new data files

You can also trigger the workflow manually from the Actions tab in your GitHub repository.

## Output

The scraper produces:
1. A SQLite database in `data/jobs.db` with tables for matched and filtered jobs
2. Daily CSV files in the `data/` directory with timestamps (e.g., `linkedin_jobs_20250323.csv`)
