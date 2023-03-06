
# Insight 
The purpose of the insight is to provide reports and dashboard widgets to the application. 

The definition of an insight resides in `Report Type`. It has the data `provider` on which it runs it's queries and then renders the data. The rendering can take many forms - tabular, chart etc. You can even download the data is _excel_ or _pdf_ formats.

Here are the attributes of a Report Type

```ts
export class ReportType {
  code: string;
  name: string;
  icon?: string;
  description?: string;

  area: ReportArea;
  provider: ReportProvider;

  config: any;

  download?: ReportDownload;
  widget?: ReportWidget;

  header: ReportColumn[] = [];
  table?: ReportTable;
  footer: ReportColumn[] = [];

  params: ReportParam[] = [];
  columns: ReportColumn[] = [];

  status: string;
  permissions?: string[];
}
```

A Sample Data
```javascript
{
    "code" : "present-today",
    "name" : "Presents",
    "area" : {
      "code": "attendance"
    },
    "provider" : {
      "code": "ams-db",
      "db": { /* connection information goes here*/}
    },
    "config" : {
        "sql" : {} 
    },
    "download": {
        "format" : "pdf",
         "page": { 
           "size": "A4",
           "orientation": "landscape",
           "margins": [5,10, 5,10]
         },
    },
    "widget": {
        "type": "table",
        "style": {/* */},
    },
    "header": [{
      "label": "Report:"
      "column": 1
      "key": "type.name", // context.organization.name, params, params[0].date etc
      "format": '', // used to format dates
      "style": { 
        /* */
      }
    }],
    "table": { 
      "layout": "zebra"
      /* */
    },
    "footer": [{ 
      "key": "pageNo", // context.organization.name, params, params[0].date etc
      "format": 'pageNo of totalPages', //
      "style":  { /* */},
    }],
    "columns" : [{
        "label" : "Department",
        "key" : "department",
        "type" : "string",
        "dbKey" : "-- the select part of query --",
        "format": '', // used to format dates
        "style" : {}
    }, {
       /* -- more columns -- */ 
    }],
    "params" : [{
        "label" : "Date",
        "key" : "date",
        "dbKey" : "v.Date",
        "dbCondition" : "gt",
        "type" : "date",
        "required" : true,
        "message" : "Please select date"
    }, {
       /* -- more filter params -- */ 
    }],
    "permissions" : [ 
        "organization.admin"
    ],
    "status" : "active",
}
```

```ts
export class ReportParam {
  label?: string;
  key: string;
  required?: boolean;
  value?: any;
  valueKey?: string;
  valueLabel?: string;
  message?: string;
  group?: string;
}
```

```ts
export class ReportColumn {
  key: string; // type.name, context.organization.name, params, params[0].date etc
  label?: string;
  icon?: string;

  dbKey : string;
  type: string; // date, string, number, pager
  format: string, // date format when type is date, pageNo of totalPages

  style?: ReportStyle;
  ascending?: boolean;
}
```

```ts
export class ReportStyle {
  font?: {
    size: number,
    bold: boolean
  },
  align: 'left'|'right'|'center',
  border?: {
    left: 'thin'|'thick',
    right: 'thin'|'thick',
    top: 'thin'|'thick',
    bottom: 'thin'|'thick',
    color: string
  },
  background: string
}
```

```ts
export class ReportDownload {
  format: string; // default "excel", "pdf,
  page: ReportPage;
}
```

```ts
export class ReportPage {
  size: string; // default "A4",
  orientation: string; // "landscape",
  margins: [5, 10, 5, 10] // left, top, right, bottom
}
```


It has some main Entities :-
- Area Code
- Report Type Code
- Report

Each Area has some Report Types based on Tenant and Organization

For example:

An Tenant Heritage Has Organization ASI and It has a Area called Online which contain Deatils of All Online Tickets of Monuments.
In online Area it has a report type called daily tickets which gives us total online tickets details of current date.


## Models

```ts
export class ReportArea {
  code: string;
  name: string;
  icon?: string;
  permissions?: string[];
}
```


```ts
export class Report {
  id: string;
  type: ReportType;
  params: ReportParam[] = [];

  requestedAt: string;
  startedAt: string;
  completedAt: string;

  filePath: string;
  url: string;
  config: any;

  error: string;
  status: string;
}
```


## Base Components

### Report Type List
```ts
export class ReportTypeListBaseComponent {

  @Input()
  area: string | ReportArea;
  //Area Code

  @Input()
  view: 'table' | 'list' | 'grid' = 'table';

}
```

### Report List
```ts
export class ReportListBaseComponent {

  @Input()
  reportType: ReportType;
  //Reprt Type Object

  }
```

### Report Data
```ts
export class ReportDataBaseComponent {

  @Input()
  report: Report;
  //Report To Show

  @Input()
  reportType: ReportType;

  @Input()
  query: any;
  //Query Items For Report Data Filtering

  @Input()
  refreshSeconds = 0;

  @Input()
  view: 'table' | 'grid' | 'bars' | 'pie' = 'table';

  // @Output()
  // onClose: EventEmitter<any> = new EventEmitter<any>();

  // page: PagerModel<any>;

  headArray = [] ;
  //Columns Array For Table Heads

  }
```

### Widgets Component

We can send Either Report Type Object or Report Type Code

items is an Array containing item's Each item is in Format :- 

```ts
key: value,
key: value,.....
```
You Can Fetch Each value using ReportType.ReportColumn.key

```ts
export class WidgetBaseComponent {

  @Input()
  reportType: ReportType;

  @Input()
  code: string;

  @Input()
  refreshSeconds = 0;

  @Input()
  options: PageOptions;

  @Input()
  params: any = {};

  items: any[] = [];

  isProcessing = false;

  //Functions For Child Components
  afterInitialization: () => void;
  afterProcessing: () => void;

  }
```

## Components

### Report Type List

```html
<insight-report-type-list [area]="areaCode" (selected)="onSelect($event)" [view]="onlyList? 'table': 'list'">
</insight-report-type-list>
```

### Report List
```html
<insight-report-list [reportType]="reportType" (selected)="selectReport($event)">
</insight-report-list>
```

### Report Data
```html
<insight-report-data [report]="report" [reportType]="reportType">
</insight-report-data>
```

### Single Item Graph

type :- 
- bar
- line
- pie

```html
<insight-graph-widget [reportType]="reportType" type='type'>
</insight-graph-widget>
```

### Multiple Items Graph

type :- 
- bar
- line
- pie

```html
<insight-dual-graph-widget [reportType]="reportType" type='type'>
</insight-dual-graph-widget>
```

### Grid
```html
<insight-grid-widget [reportType]="reportType">
</insight-grid-widget>
```

### Table
```html
<insight-table-widget [reportType]="reportType">
</insight-table-widget>
```
