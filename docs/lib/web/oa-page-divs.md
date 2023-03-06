# page DIVS

``` html
  <app-page-divs [divs]="page?.meta?.divs" [areaCode]="'stat-area-code'" (selected)="onStatSelect($event)">
  </app-page-divs>
```

```JSON
    "divs": [
      {
        "code": "enquiries-page",
        "style": {
          "widgets": {
            "class": "one"
          }
        },
        "widgets": []
      }
    ]
```

It takes an array of `divs` and `stat-area-code`. Based on the area code it fetches all the stats definitions from the insight service and render them in the divs. If any of the stats is clickable, it it emitted via `selected` event.
