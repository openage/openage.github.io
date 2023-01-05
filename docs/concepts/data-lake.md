# Data Warehouse
#data #warehouse

To be able to run reports, you need to keep data in de-normalize form.  

---
## Collecting the data

There are 2 ways in which data can be collected.
1. Run scheduled jobs to fetch the data from the OTLP data sources
2. Use data update trigger to fetch the data and add it to the lake

The first approach works fine when the data size is small, but when the need is for near realtime stats, you should use event triggered data collection mechanism.

---
### Using Composer 

![[fix-me.jpg]]

---
### Using DB triggers 
![[fix-me.jpg]]

---

Next: Create Aggregated data
