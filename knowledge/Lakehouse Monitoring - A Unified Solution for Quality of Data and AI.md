Før du læser, så hav styr på: 
- [[Data Lake]]
- [[Data Warehouse]]
- [[Data Lakehouse]]

## Introduction
Basal forklaring af _Lakehouse Monitoring_, er, at det er et tool til at holde øje med alle ens pipelines uden ekstra redskaber eller kompleksitet. 

En _serverless_ løsning.

## Why Lakehouse Monitoring?
Årsagen til at Lakehouse Monitoring kom til verdenen, var fordi der typisk er et problem i, at man har en data pipeline der virker til at køre gnidningsfrit, men hvor man på et tidspunkt opdager at data-en der bliver produceret bliver værre og værre.

Derfor kan _Lakehouse Monitoring_ hjælpe til med at opdage kvalitetsproblemer før det påvirker den data der bliver produceret, så man ikke skal debugge og tilbagerulle ændringer man har lavet tidligere.

## How it works
Jeg vil lade databricks selv forklare hvordan det fungere:
>With Lakehouse Monitoring, you can monitor the statistical properties and quality of all your tables in just one-click. We automatically generate a dashboard that visualizes data quality for any Delta table in Unity Catalog. Our product computes a rich set of metrics out of the box. For instance, if you’re monitoring an inference table, we provide model performance metrics, for instance, R-squared, accuracy, etc.. Alternatively, for those monitoring data engineering tables, we provide distributional metrics including mean, min/max, etc.. In addition to the built-in metrics, you can also configure custom (business-specific) metrics that you want us to calculate. Lakehouse Monitoring refreshes metrics and keeps the dashboard up-to-date according to your specified schedule. All metrics are stored in Delta tables to enable ad-hoc analyses, custom visualizations, and alerts.