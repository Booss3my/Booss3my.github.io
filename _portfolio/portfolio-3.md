---
title: "Indeed data scraper"
excerpt: "Scraping job offers from indeed and scheduling tasks using Airflow <br/><img src='/images/SOH_estimator/inference.png'>"
collection: portfolio
---


# Overview
Developed a robust web scraper for Indeed job listings, employing a paid web proxy API and orchestrating the process with Airflow. Leveraged Docker Compose for seamless deployment, extracting and storing job information in a PostgreSQL database. The project aimed at providing comprehensive insights into the job market, enabling personalized searches, and automating job applications.

# Technical Highlights
## Web Scraping Logic

The core of the project lies in the web scraping logic. Utilized Python and BeautifulSoup to extract relevant job information from Indeed's dynamic web pages and pandas for data cleaning and processing, the main function is the scrape function (called in the airflow DAG).

```python
def scrape(max_date=2, subjects=["data science"], pages=3):
    """
    Main function to extract, transform, sort, and save job offers.

    Args:
        max_date (int): Age of offers in days.
        subjects (list): List of subjects for job offers.
        pages (int): Number of pages to scrape per subject.
    """
    offerlist = []
    for subject in subjects:
        for i in range(0, pages * 10, 10):
            soup = extract(max_date, i, subject)
            df = transform(soup)
            df["Date"] = freshness_to_date(df["Freshness"])
            offerlist.append(df)

    df = pd.concat(offerlist)
    df.reset_index(drop=True)
    df.to_csv(os.path.join(RPATH,"staging/offers.csv"))
```

## Airflow Orchestration
Employed Apache Airflow to orchestrate and schedule the scraping tasks. Configured an Airflow DAG (Directed Acyclic Graphs) to define the workflow, and the execution schedule (daily). This approach allows for easy monitoring and maintenance of the scraping and loading processes.

DAG :
```python
ingestion_dag = DAG(
    'Indscraping_dag',
    default_args=default_args,
    description='Job offer records scraping',
    schedule_interval=timedelta(days=1),
    catchup=False
)
```
Scraping task :
```python
task_1 = PythonOperator(
    task_id='ScrapeData_and_transform',
    python_callable=scrape,
    dag=ingestion_dag,
)
```

Loading task :
```python
task_2 = PythonOperator(
    task_id='load_to_DB',
    python_callable=load_data,
    dag=ingestion_dag,
)
```

## PostgreSQL Database Integration
Implemented PostgreSQL as the backend database for storing scraped job data. Utilized SQLAlchemy for seamless integration with Python, ensuring efficient data storage and retrieval.
