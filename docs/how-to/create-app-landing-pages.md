# Pages
#pages #navigation 

A `layout.json` file would be define

- the structure of the page
- where the landing page would render the widgets
- if there are any static HTML that needs to inject
- the look and feel of the page and its sections

This file would be available in the public folder `root|landing|:code`. Here is a sample document

```json
{
    "title": {
        "text": "A custom landing page",
        "style": {
            "font-size": "24px"
        }
    },
    "class": "",
    "style": {
        "background": ""
    },
    "divs": [{
        "id": "header",
        "class": "",
        "style": {
            "background": ""
        },
        "body": {
            "text": "This is <b>custom</b> landing page",
            "style": {
                "font-size": "12px"
            }
        }
    }, {
        "class": "",
        "style": {
            "background": ""
        },
        "title": {
            "text": "Custom Page",
            "style": {
                "font-size": "24px"
            }
        },

        "layout": {
            "class": "row-3-1",
            "divs": [{
                "code": "widgets-section-1"
            }, {
                "body": {
                    "text": "<img href='http://www.images.com/sample-image.png'/>"
                }
            }]
        }
    }, {
        "id": "footer"
    }]
}
```

Important Points:

1. The layout contains a collection of divs. Each div can have a further layout
2. The organization of div into columns and rows are determined by style and class in the layout object

The angular landing component would fetch the file and render it using the following logic

```html
<div [style]="layout.style" [class]="layout.class">
    <h1 *ngIf="layout.title" [style]="layout.title.style" [class]="layout.title.class">{{layout.title.text}}<h1>
    <div *ngIf="layout.body" [style]="layout.body.style" [class]="layout.body.class" [innerHtml]= "layout.body.text"></div>
    <ng-container *ngFor="let item of layout.divs" >
        <ng-container *ngTemplateOutlet="layoutTemplate; context: { div: item }"> </ng-container>
    </ng-container>
</div>

<ng-template #layoutTemplate let-div="div" let-fns="fns">
    <div [class]="item.class" [style]="item.style">
        <h1 *ngIf="div.title" [style]="div.title.style" [class]="div.title.class">{{div.title.text}}<h1>
        <div *ngIf="div.body" [style]="div.body.style" [class]="div.body.class" [innerHtml]= "div.body.text"></div>

        <ng-container *ngFor="let widget of widgets">
            <div *ngIf="div.code && widget.container && widget.container.code === div.code || (!div.code && !widget.container)" [class]="widget.container.class" [style]="{{widget.container.style}}">
                <ng-container [ngSwitch]="widget.type">
                <!-- TODO: render widget here -->
                </ng-container>
            </div>
        </ng-container>
        <div *ngIf="div.layout" [style]="div.layout.style" [class]="div.layout.class">
            <ng-container *ngFor="let item of div.layout.divs" >
                <ng-container *ngTemplateOutlet="layoutTemplate; context: { div: item }"> </ng-container>
            </ng-container>
        </ng-container>
    </div>
</ng-template>
```

Important Points:

1. the widgets (report type) are rendered as a set of stacked div
2. the widgets may decide to which container they would be rendered
3. the order of contents within a container is
   1. title
   2. body
   3. widgets
   4. sub-layouts
4. Each content can have its own styling
5. the style on the sub-layout div determines how its containing div would be rendered


 
 [[list-page]]
 [[page-divs]]

