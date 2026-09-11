Classical archaeologist working in analytics engineering. I build data models with dbt and BigQuery, and most of what I point them at is archaeological.

The two are the same kind of work. A finds assemblage and a production table are both partial records of something that happened, and neither means much until you know how it was assembled — what got recorded, what got dropped, at what resolution. Archaeology calls that provenance and context. Data modelling calls it lineage and grain.

## Projects

**[greenweez-analytics-pipeline](https://github.com/melisaceliklabs/greenweez-analytics-pipeline)** — dbt, BigQuery

A daily finance metrics table, built in bronze/silver/gold layers. 7 models, 5 tests, 3 documented sources, lineage generated from the project itself.

Most of the effort went into the source data rather than the models: type mismatches that produced wrong aggregates without failing anything, duplicate columns, and a table whose primary key turned out to be composite.

**[circle-parcel-dbt-pipeline](https://github.com/melisaceliklabs/circle-parcel-dbt-pipeline)** — dbt, BigQuery

Parcel and shipment data. The staging layer fixes inconsistent column casing and parses dates that arrive as strings like `January 5, 2024`. The analytics layer derives delivery status, transit times and a delay flag, and partitions the parcel-product table on purchase date.

This is where I learned about grain the hard way. Joining parcels straight to products multiplies each parcel row by its product count and inflates every total. No error, just wrong numbers. Aggregate first, then join.

**[norfolk-roman-coins](https://github.com/melisaceliklabs/norfolk-roman-coins)** — Python, pandas, GeoPandas

25,394 Roman coin records from Norfolk, recorded by the Portable Antiquities Scheme. District-level mapping, a Reece period profile, denomination and ruler breakdowns.

Worth knowing what this dataset is before reading the maps. 99.87% of the records were found by metal detector; seven came from an archaeological context. Findspots are withheld below county level so sites aren't targeted by illicit detecting. That isn't a flaw in the data, it's what the data is, and it sets a limit on what can be claimed from it.

## How I work
 
I pay attention to what a dataset leaves out. Gaps, restricted fields, records that were never made — these usually say something about how the data was collected, and I keep them visible in the results instead of quietly dropping them for a cleaner output.
 
I check before I trust. Plausible-looking numbers are the dangerous ones, so I'd rather build in something that breaks loudly when an assumption stops holding than find out months later that a total has been wrong the whole time.
 
And I write down the decisions. What I chose, why, and what I deliberately didn't do. Partly so someone else can follow the work, partly because I've forgotten my own reasoning often enough to stop trusting my memory for it.

## Tools

SQL, dbt, BigQuery, Python (pandas, GeoPandas, matplotlib), Git. Some QGIS and PostGIS.

