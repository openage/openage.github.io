# Structure of a List Page

The `NavService` will return the page object which was used as part of configuration

```TypeScript
this.page = this.navService.register('<registered-url>', this.route, (isCurrent, params) => {
  this.isCurrent = isCurrent;
  if (this.isCurrent) {
	// set any page specific setting here
  }
});
```

The `page` object usually contains `meta` that will be used in different parts of the page. It would typically have the following

- `divs`: to render the stats by `app-page-divs`
- `search`: defines the search params to be rendered by `oa-search`

A list page is usually part of a list-detail page. The details will be added in the `<router-outlet></router-outlet>`. The `main` section will hold the list.

```HTML
<div class="main" [class.hidden]="!isCurrent">
</div>

<router-outlet></router-outlet>
```

## Sections

### Header

```HTML
<div class="header">
<h5>{{page?.title}}</h5>
<span class="spacer"></span>
<!-- add list filters here -->
<oa-search class="spacer" (editing)="isSearching = $event" (changed)="onSearch($event)"
  [options]="page.meta.search"></oa-search>
<!-- add action items here -->
<button mat-raised-button class="primary" (click)="onNew()">New</button>
<mat-icon [matMenuTriggerFor]="moreMenu">more_vert</mat-icon>
<mat-menu #moreMenu="matMenu">
	<!-- additional action items here -->
</mat-menu>
</div>
```

### Stats

``` html
<app-page-divs [divs]="page?.meta?.divs" [areaCode]="'stat-area-code'" (selected)="onStatSelect($event)">
</app-page-divs>
```

It takes an array of `divs` and `areaCode`. Based on the areaCode it fetches all the stats definitions from the insight service and render them in the divs. If any of the stats is clickable, it it emitted via `selected` event

### List of Items
