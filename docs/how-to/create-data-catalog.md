# Data Catalog
#data #report #catalog

Data Catalog is a set of data labled and ready for consumption.

---
I constitutes of
1. Discovery - labeling and categorization for discovery of the catalog
2. Prefined Query - to fetch the data
3. Columns - with key, label
4. Params - filters which are available for visualization

---
Here are the steps for creating data catalog
1. Create data warehouse. See [[data-lake]]
2. Create aggregation pipeline. See [[data-transformation]]
3. Creating Report Master

---
## Creating Report Master

![[report-data-catalog.png]]


1. Select source of data. See [[predefined-connections]]
2. Set the Query/Stored procedure.

---
### Do's and Dont's
- Never fetch data from the OTLP
- Always read data from read replica
