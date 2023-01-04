
You will find data about Activities in this api  

# Insight Api > Journal list
It is an Activity Service has one Required Model Entity

If you send an entity object then it will filter using the object otherwise it will give you result according to organization and tenant.

For example:

If you need to get vendor's activities then send entity object with entity.type="vendor".


## Models

```ts
export class Entity {
  id?: String;
  code?: String;
  type?: String;
  name?: String;
}

```

```ts
export class Journal extends ModelBase {

  message: string;
  entity: Entity;
  user: User;
  meta: {} = {};
  type: string;
  changes: [{
    field: string,
    value: string,
    oldValue: string
  }];

  constructor(obj?: any) {
    super();

    if (!obj) { return; }
    this.id = obj.id;
    this.timeStamp = obj.timeStamp;

    this.message = obj.message;
    this.meta = obj.meta;
    this.type = obj.type;

    this.changes = obj.changes;

    if (obj.entity) {
      this.entity = new Entity(obj.entity);
    }
  }
}
```

## Base Components

### Journal List
```ts
export class JournalListBaseComponent implements OnInit, OnChanges {

  @Input()
  entity: Entity;
  //You can either send an entity object or not

  @Input()
  refreshSeconds = 0;
  //You can either send refreshSeconds or not

  @Input()
  options: PageOptions;
  //You can either send an options object or not

  @Input()
  params: any = {};
  //You can either send a params object or not

  items: Journal[] = [];

  isProcessing = false;

}
```

## Components

### Journal List

```html
<insight-journal-list></insight-journal-list>
```

OR

```html
<insight-journal-list [entity]="entity"></insight-journal-list>
```
