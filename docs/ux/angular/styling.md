# Styling

## Columns

**evenly spread**

```html
<div class="controls-row">
  <div>column 1</div>
  <div>column 2</div>
  <div>column 3</div>
</div>
```

**left-aligned**

```html
<div class="controls-row">
  <div>column 1</div>
  <div>column 2</div>
  <div class="spacer"></div>
</div>
```

**right-aligned**

```html
<div class="controls-row">
  <div class="spacer"></div>
  <div>column 1</div>
  <div>column 2</div>
</div>
```

**justified aligned**

```html
<div class="controls-row">
  <div class="spacer"></div>
  <div>column 1</div>
  <div class="spacer"></div>
  <div>column 2</div>
</div>
```

**pre-defined ratio**

3 columns

* `flex-1-1-2`
* `flex-1-2-1`
* `flex-2-1-2`
* `flex-1-3-1`
* `flex-1-7-2`

2 columns (and vice versa)

* `flex-1-1`
* `flex-1-2`
* `flex-1-3`
* `flex-1-4`
* `flex-1-6`
* `flex-1-9`

## Icons

all icons need to be square

```html
<i class="home"></i>
<mat-icon class="oa"></mat-icon>
```

supported sizes are

* `x-sm` 5px
* `sm` 10px
* `md` 20px
* `x-md` 30px
* `xx-md` 40px
* `lg` 100px
* `x-lg` 150px
* `xx-lg` 200px

## Tabs

**horizontal tab**

```html
  <div class="tabs horizontal">
    <div [class.active]="section === 'a'}" (click)="section = 'a'">Tab A</div>
    <div [class.active]="section === 'b'}" (click)="section = 'b'">Tab B</div>
    <div [class.active]="section === 'c'}" (click)="section = 'c'">Tab C</div>
  </div>
  <ng-container [ngSwitch]="section">
    <ng-container *ngSwitchCase="'a'"> Section A Content</ng-container>
    <ng-container *ngSwitchCase="'b'"> Section B Content</ng-container>
    <ng-container *ngSwitchCase="'c'"> Section C Content</ng-container>
  </ng-container>
```

**horizontal tab with actions**

```html
  <div class="tabs horizontal with-actions">
    <div [class.active]="section === 'a'}" (click)="section = 'a'">Tab A</div>
    <div [class.active]="section === 'b'}" (click)="section = 'b'">Tab B</div>
    <div class="spacer controls-row">
      <div class="spacer"></div>
      <button (click)="onAction1()">Action 1</button>
    </div>
  </div>
  <ng-container [ngSwitch]="section">
    <ng-container *ngSwitchCase="'a'"> Section A Content</ng-container>
    <ng-container *ngSwitchCase="'b'"> Section B Content</ng-container>
  </ng-container>
```

## Table

```html
<div class="table">
  <div class="header">
    <div class="col-1">Header 1</div>
    <div class="col-2">Header 2</div>
    <div class="col-3">Header 3</div>
    <div class="col-4">Header 4</div>
  </div>
  <div class="data-row">
    <div class="col-1">Cell 1-1</div>
    <div class="col-2">Cell 1-2</div>
    <div class="col-3">Cell 1-3</div>
    <div class="col-4">Cell 1-4</div>
  </div>
  <div class="footer">
    <div class="spacer">Total</div>
    <div class="col-4">200 INR</div>
  </div>
</div>
```
