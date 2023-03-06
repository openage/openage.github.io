# OA Table

It generates a table of data from the list of items. It uses table `definitions` to customize the look and feel of the table.

## Overview

### Showing data in a table

```HTML
<oa-table 
    [definition]="options.table" 
    [items]="data">
</oa-table>
```
For following data 
```JSON
[{
    "code": "tech",
    "name": "Tech",
    "description": "Solution Delivery Services",
    "children": [{
        "code": "dev",
        "name": "Development",
        "status": "Active"
    }]
}, {
    /// ...
}]
```
The definition would like this

```JSON
{
    "fields": [{
        "label": "Sr.No",
        "key": "index"
    }, {
        "label": "Code",
        "key": "code"
    }, {
        "label": "Name",
        "key": "name"
    }, {
        "label": "Status",
        "key": "status",
    }]
}
```

Checkout [field details](/how-to/field-attribtutes.md) for more details.


The definition achives follwoing purposes
1. Ordering of columns
2. Standardizing the table
3. Making the table mobile responsive

### Selectable rows

You can make the index column to render the checkbox.

```JSON
{
   "fields": [{
        "label": "Sr.No",
        "key": "index",
        "control": "checkbox",
        "config": {
            "toggle": "selected"
        }
    }, {
        // Other fields
    }]
}
```

When the user clicks on the checkbox, the `item.isSelected` value is toggled and all the selected items are emitted in `selected` event.

### Styling the columns

```JSON
{
    "style": {
        "container": {
            "class": "",
            "style": {}
        },
        "header": {
            "class": "",
            "style": {}
        },
        "fields": {
            "class": "",
            "style": {}
        }
    }
}
```


![[fix-me.jpg]]
TODO: insert image -different styling mechanism

## Actionable Rows

### Adding Action Buttons
Add the action fileds
```JSON
{
    "fields": [{
        // Other Fields
    }, {
        "label": "Action",
        "key": "action",
        "config": {
            "actions": [ {
                "code": "add-child",
                "icon": "add_circle_outline",
                "title": "Add Child",
                "style": "accent"
            }, {
                "code": "edit",
                "title": "Edit",
                "style": "primary"
            }, {
                "code": "remove",
                "title": "Remove",
                "style": "default"
            }]
        }
    }]
}
```
NOTE: there are several system defined icons mapped to the code. Checkout the [pre-defined icons](/lib/web/pre-defined-icons.md).

Add the action handler in the component

```typescript
this.actionHandler = {
    'addChild': (i) => this.showDialog(i),
    // define other actions
}
```

Pass the action handler to the oa-table
```HTML
<oa-table 
    [definition]="options.table" 
    [items]="data" 
    [actions]="actionHandler">
</oa-table>
```

### Overriding Action Rendering

You can skip the `oa-table` action rendering, and instead add custom action rendering.

Create an action rendering template.

```HTML
<ng-template #actionCell let-item="item" let-index="index">
  <button (click)="addChild(item)">
    <mat-icon >add_circle_outline </mat-icon>
  </button>
  <button (click)="onEdit(item)">
    <mat-icon style="color:var(--primary);">edit</mat-icon>
  </button>
  <button (click)="onRemove(item)">
    <mat-icon>delete_outline</mat-icon>
  </button>
</ng-template>
```
and pass it to `<oa-table>`

```HTML
<oa-table 
    [definition]="options.table" 
    [items]="data" 
    [actionTemplate]="actionCell">
</oa-table>
```

NOTE: you still need to define the `action` field

## Customizing the value rendering

There are several different ways to change the value rendering.

### Implementing a cell template

Create a cell template.
```HTML
<ng-template #valueCell let-item="item" let-field="field" let-index="index">
  <ng-container [ngSwitch]="field.template">
    <div *ngSwitchCase="'children-count'" class="badge accent">{{item?.children?.length || 0}}</div>
    <div *ngSwitchCase="'status'" class="pill-box" [class]="item.status === 'Active' ? 'primary' :'disabled'">{{item.status}}</div>
  </ng-container>
</ng-template>
```

```JSON
{
"fields": [{
    // Other Fields
    }, {
        "label": "Chlidren",
        "key": "children",
        "template": "children-count"
    },
    {
        "label": "Status",
        "key": "status",
        "template": "status"
    }, {
        // Other Fields
    }]
}
```
NOTE: we have specified `template` based on which you will filter out the column to render.

Pass the cell template to the `oa-template`

```HTML
<oa-table 
    [definition]="options.table" 
    [items]="data" 
    [cellTemplate]="valueCell">
</oa-table>
```

### Formatting a value

```JSON

{
"fields": [{
    // Other Fields
    }, {
        "label": "Created On",
        "key": "createdTime",
        "type": "date",
        "format": "date-time"
    }, {
        // Other Fields
    }]
}
```

In order to format a value, you need to specify `format` as part of field definition. To use the format, `oa-table` additionaly needs `type` to use the formatter.

Checkout the [pre-defined value formatters](/lib/web/pre-defined-value-formatters.md.md).

## Extensions

###  Details Rendering 

Define the detail template

```HTML
<ng-template #itemDetails let-item="item" let-index="index">
  <table *ngIf="item?.children?.length">
    <tbody>
      <tr *ngFor="let child of item.children">
        <td>{{child.name}}</td>
        <td><div class="pill-box"> {{child.status}}</div></td>
        <td><button><mat-icon (click)="onEditChild(child)">edit</mat-icon></button></td>
      </tr>
  </table>
  <oa-no-data-found *ngIf="!item?.children?.length"></oa-no-data-found>
</ng-template>
```

Pass it to the `oa-table`

```HTML
<oa-table 
    [definition]="options.table" 
    [items]="data" 
    [detailsTemplate]="itemDetails">
</oa-table>
```

Specify the trigger for rendering the details. 

```JSON
{
    "fields": [{
        // Other Fields
    }, {
        "label": "Name",
        "key": "name",
        "config": {
            "click": {
                "toggle": "details"
            }
        }
    }, {
        // Other Fields
    }]
}
```
Above example makes the `Name` field clickable.

### Item editor

This is very similar to showing the details.

As shown in the previous example, create an editor template, set it as `editorTemplate` on the `oa-table`. Then in the field definition set the value `click.toggle` to `editor`.

To have inline editor, set the `options.editor.view` property to `inline` and define the `edit` action without specifying the action handler.

```JSON
{
    "options":{
        "editor": {
            "view": "inline"
        }
    },
    "fields": [{
        // Other Fields
    }, {
        "label": "Action",
        "key": "action",
        "config": {
            "actions": [ {
                "code": "edit",
                "title": "Edit",
                "style": "primary"
            }, {
                // Other Actions
            }]
        }
    }]
}
```

The `oa-table` will implement the default action handler for edit, buy setting the `item.isEditing` to `true`. If the `options.editor.view` is set to `inline` it will render the field controls. Otherwise, it will render the `editorTemplate`. The `edit` action, while in editing mode, will be replaced with `save` and `cancel` buttons

### New item

In table definition add the create option.

```JSON
{
    "options":{
        "create": {
            "view": "inline",
            "position": "top"
        }
    },

    "fields": [
        // Fields
    ]
}
```

This will try to render as **first row**, editor for each field, where the control is specified. Alternatively, you can specify the `createTemplate` to render your custom create item row.

To render the create item row as footer, simply set the `options.create.position` to `"bottom"`.


## Overriding Mechanisms

### Templated Header

Create a custom header and set it on `oa-table`

Table header template

```HTML
<ng-template #headerRow>
    <div class="header">
        <div class="code">Code</div>
        <div class="name">Name</div>
        <div class="children">Childern</div>
        <div class="status">Status</div>
    </div>
</ng-template>
```

```HTML
<oa-table 
    [definition]="options.table" 
    [items]="data" 
    [headerTemplate]="headerRow">
</oa-table>
```

### Templated Row

Create a custom data row and set it on `oa-table`

Data row template

```HTML
<ng-template #dataRow let-item="item" let-index="index">
    <div class="card">
        <div class="header">{{item.name}}</div>
        <div class="body">
            <div class="field">
                <label>Code</label>
                <div>{{item.code}}</div>
            </div>
            <div class="field">
                <label>Name</label>
                <div>{{item.name}}</div>
            </div>
            <div class="field">
                <label>Description</label>
                <div>{{item.description}}</div>
            </div>
        </div>
        <div class="footer">
            <button (click)="onStatusClicked(item)">{{item.status}}</button>
            <button (click)="onEditClicked(item)">Edit</button>
        </div>
    </div>
</ng-template>
```

Specify the `rowTemplate`

```HTML
<oa-table 
    [definition]="options.table" 
    [items]="data" 
    [rowTemplate]="dataRow">
</oa-table>
```
