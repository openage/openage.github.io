---
banner: "![[reports.jpg]]"
---
# Reports
#insight #console #directory 

Operator should be able to respond to the dynamic business needs by understanding, tweaking and sharing the data/reports with various type of users

The tool would enable the user to
-   View what data is available in the system
-   Create visual representation of the data
-   Generate and distribute reports
-   Limit the access to data based on his role

https://reports.prebuilt.tech


## Roles
- User
- Operator
- Data Engineer
- System Engineer

## Features

### Pages
#### Dashboard 
#### Reports

### Designers
#### Data Catalogue Builder 
##### Data Fetching Wizard
1. Select and configure the provider

#### Document Designer
#### Dashboard Designer
#### Report Widget
- Stats
- Chart
- Table

## Technology Stack

### Data Pipeline
- Data Collection
	- Open Age Composer to collate data into a data warehouse
	- Open Age Connect to pull and push data from external sources
	- Data Manager UI to configure data sources and collation keys
- Data Analytics
	- Apache Flink to create data aggregation pipeline
	- TensorFlow to build prediction models
	- Aggregation Builder UI to manage pipelines

### Data Discovery

Data Catalogue
-   Open Age Insight to manage data catalogue
-   Open Age Directory to manage who can access what data
-   Data Catalogue UI to view the data catalogue
Data Widgets
-   Widget Designer to view/create Grafana/ChartJS data widgets
Report Builder to manage columns, filters, access, styling and download formats**

## Roadmap
- [ ] ability to collect and collate data from multiple sources 
	- [ ] ability to add data source
		- [ ] discover data provider
		- [ ] select and configure data provider
	- [ ] ability to add data target (data warehouse)
		- [ ] discover data provider
		- [ ] select and configure provider
	- [ ] ability to write and run query
		- [ ] context: save
		- [ ] toolbar: 
			- [ ] data providers
			- [ ] tables
			- [ ] join
			- [ ] select
		- [ ] workspace: 
			- [ ] Provider
			- [ ] Columns
			- [ ] Query Builder (provider specific)
				- [ ] Generic (raw)
				- [ ] Provider Specific 
					- [ ] MSSQL
					- [ ] MySQL
					- [ ] MongoDb - collection,lookups, project, sorts, limit, 
			- [ ] result (show results)
		- [ ] properties: column, params, report-master
		- [ ] Run and see result
- [ ] ability to aggregate the data 
	- [ ] data pipeline provider (flink)
	- [ ] pipeline viewer/editor
- ability to discover data available in the system so that reports can be created from it
	- [ ] ability to build data catalogue (https://yofs.invisionapp.com/console/share/M434WVN9P6/813969464)
		- [ ] select a set of data from warehouse and give it a unique name & code and following attributes
			- [ ] category  - Order, User, Job etc
			- [ ] tags - 
			- [ ] name and description of each column/field
	- [ ] ability to view data catalogue
		- [ ] show the catalogue grouped by category
		- [ ] create report button from the catalogue
- ability to build/view report
	- [ ] business user's ability to build report from the data catalogue
		- [ ] Toolbar 
			- [ ] data catalogue, 
			- [ ] data table: catalogue columns (selected catalogue),
			- [ ] data table: filters
			- [ ] summary: widgets
			- [ ] root: layout
		- [ ] Workspace 
			- [ ] catalogue,
			- [ ] summary, 
			- [ ] filters, 
			- [ ] data table, 
			- [ ] export, 
			- [ ] job (to schedule/send report etc)
		- [ ] Properties - for 
			- [ ] report (title, icon, code, area/collection, security), 
			- [ ] column (title, formatting, click handler, formula& format etc), 
			- [ ] filter (title, default value, visible/hidden etc) export format
	- [ ] ability to view the reports
		- [ ] report's dashboard - collection of widgets, including reports grouped by areas
		- [ ] report pages grouped by area
	- [ ] data engineer's ability to create data widgets - to be used on report/dashboard pages
		- [ ] Toolbar - data catalogue
		- [ ] Workspace - widget, filters, data table, export, job (to schedule/send report etc)
- [ ] ability to build and edit dashboard with data widgets
- [ ] ability to create a dynamic document from the data
- [ ] ability to share reports manually or when an event occurs in the system

