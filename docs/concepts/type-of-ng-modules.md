# Modules

The application is divided into the following modules

1. Domain modules
1. Framework modules
1. Page modules
1. Shared Modules

## Shared Modules

### Shared Module

- defines common components, directives, pipes and dialogues
- is used by other application modules but uses none of them
- Does not depend on any modules

### Core Module

- is used to construct the application structure
- can depend on any module
- should be limited to bare minimum dependencies as it is loaded during the booting itself

## Framework Modules

- have no dependencies on any other module expect the `shared.module`

They are grouped under `core`, `logical` and `angular` groups

### Core module

Defines structural components that other components can extend and use

### Logical modules

Defines

- models,
- services and
- abstract components

### Components modules

- one per each microservice, they implement the UX

## Domain Modules

These modules define the domain controls that the page module uses. The components can be classified as a list or detail component

### List component

- naming convention `domain-entity-list`
- extends `PagerBaseComponent`
- emits events
  - `fetched` - once the list is fetched
  - `selected`
- implements
  - `refresh` method to re-fetch the data from the server

### Details component

- naming convention `domain-entity-details`
- extends `DetailBaseComponent`
- emits
  - `changed` event
- implements
  - `refresh` method to re-fetch the data from the server
  - `validate` method to check if all the required components are in place
  - `save` to save the model to the backend

**Best Practices**

- should
  - depend on only one microservice
  - implement `<processing-indicator *ngIf="isProcessing"></processing-indicator>` when interacting with backend
- can
  - consume framework modules
- should not
  - depend on other domain modules (let page-level module have this kind of functionality)
  - navigate the user to other pages (let the consuming page decide what to do on click)
  - interact with other components via service (let the consuming page manage the flow)

## Page Modules

- each page would lie inside its module's page folder `module/pages`
- if page components that span more than one framework module more than one

```html
<div class="main" [class.hidden]="!isCurrent">
    <div class="header">
      <h5>{{page?.title}}</h5>
      <span class="spacer"></span>
    </div>
    <app-page-divs [divs]="page?.meta?.divs"></app-page-divs>
    <domain-entity-list (selected)="onSelect($event)"></domain-entity-list>
</div>
<router-outlet></router-outlet>
```

```typescript
export class TypicalPageComponent implements OnInit, OnDestroy {

  isCurrent = true;
  page: Link;
  params: any = {};

  constructor(
    private navService: NavService,
    public uxService: UxService,
    private route: ActivatedRoute
  ) {
    this.page = this.navService.register(`path`, this.route, (isCurrent) => {
      this.isCurrent = isCurrent;
      if (this.isCurrent) {
        this.setContext();
      }
    });
  }

  ngOnInit() {
  }

  setContext() {
    this.uxService.setContextMenu([ { code: 'close'}]);
  }

  ngOnDestroy() {
    this.uxService.resetContextMenu();
  }
}
```

**What goes where?**

Based on their usage the pages and be categorized into the following:

### Landing module

- pages for the guest user

### Home module

- dashboard
- pages specific to the current users

### Transactional modules

Pages to interact with the data that has a fixed life

### Master module

- pages for non-transactional data

### Settings module

- pages to manage user-level or account level settings
- determine how a user behaves within the application

### System module

- pages that help monitor and control the application

### Reports module

- a set of reports that are grouped under different areas
