
## Models

```ts
class Doc {
    id: string | number;
    code: string;
    name: string;
    type: string;
    url: string;
    thumbnail: string;
    entity: Entity; 
    user: User;
}
```

```ts
class Folder {
    id: string | number;
    code: string;
    name: string;
    type: string;
    url: string;
    thumbnail: string;
    folders: Folder[];
    files: Doc[];
    entity: Entity; 
}
```

```ts
class Placeholder {
    name: string; // name of the file to use while uploading
    label: string;  // label to show on the file
    icon: string; // can be material icon or url of a file
}
```

## Base Components
```ts
class DriveFileListBaseComponent {
    @Input()
    entity: Entity;
    /* 
        limits files to one folder only
    */

    @Input()
    folder: Folder; 

    /*
        Set of files to show with + icon. These are just placeholder for files
    */
    @Input()
    placeholders: boolean | Placeholder[]; // true will shows set of files configured for that entity type

    /*
        can files be added and removed
        default: false
    */
    @Input()
    readonly: boolean;

    /*
        sort the docs by name, size, date
    */
    @Input()
    sort: string; 

    @Input()
    uploader: {
        types: string[], // ['pdf', 'word'] default null
        droppable: boolean, // default true
    };

    @Output()
    selected: EventEmitter<Doc>;

    @Output()
    created: EventEmitter<Doc>;

    @Output()
    deleted: EventEmitter<Doc>;

    /*
        child folders
    */
    folders: Folder[];

    /*
        all the files in the folder
    */
    items: Doc[];

    // ... paging components
```

```ts
class DriveFileUploaderBaseComponent {
    @Input()
    entity: Entity;

    @Input()
    placeholder: boolean | Placeholder; // true will shows set of files configured for that entity type

    @Input()
    options: {
        types: string[], // ['pdf', 'word'] default null
        droppable: boolean // default true
    };

    @Output()
    progress: EventEmitter<number>;

    @Output()
    created: EventEmitter<Doc>;

}
```

```ts
class DriveFileViewerBaseComponent {

    @Input()
    readonly: boolean // default true

    @Output()
    removed: EventEmitter<Doc>;

    properties: Doc;

}
```

## Components

### Shows files/folders as list

<img src="http://docs-api-dev.m-sas.com/files/image-bd65a480-6bf7-11e9-82f6-1169aa3bf751.png"/>

```html
<drive-files-list></drive-file-list>
```

### Shows files/folders in grid

```html
<drive-file-grid 
    [entity]="entity" 
    [options]="options">
</drive-file-grid>
```
### Shows files as gallery with lightbox
- hides folders
  
```html
<drive-file-gallery 
    [entity]="entity" 
    [options]="options"
    [lightbox]="true">
</drive-file-gallery>
```
### Shows files/folders as carousel

- hides folders
<img src="http://docs-api-dev.m-sas.com/files/image-814895b0-6bf8-11e9-82f6-1169aa3bf751.png"/>

```html
<drive-file-carousel 
    [entity]="entity" 
    [options]="options">
</drive-file-carousel>
```

## Uploading a file/files

```js
// required
const entity: Entity = {
    type: 'activity',
    id: 1232323
}

// optionals

// upload to specified folder
const folder: Folder = { } // default null 

const options = {
    template: string, // name of file to upload
    type: string[], // ['pdf', 'word'] default null
    multiple: boolean // default true
}
```
### A button to upload files
- click opens the file picker
- droppable zone
- upload progress
  
```html
<drive-file-uploader-button
    [entity]="entity" 
    [options]="options">
</drive-file-uploader-button>
```

### A zone where files can be dropped 
- click opens the file picker
- droppable zone
- upload progress

<img src="http://docs-api-dev.m-sas.com/files/image-105b4870-6bf8-11e9-82f6-1169aa3bf751.png">

<img src="http://docs-api-dev.m-sas.com/files/image-1a55f360-6bf9-11e9-82f6-1169aa3bf751.png">

```html
<drive-file-uploader-zone
    [entity]="entity" 
    [options]="options">
</drive-file-uploader-zone>
```

### Pdf file viewer
```html 
<drive-viewer-pdf [doc]="doc"></drive-viewer-pdf>
```

### JSON file viewer
```html 
<drive-viewer-json [doc]="doc"></drive-viewer-json>
```
### CSV file viewer
```html 
<drive-viewer-csv [doc]="doc"></drive-viewer-csv>
```

### DIACOM file viewer
```html 
<drive-viewer-diacom [doc]="doc"></drive-viewer-diacom>
```

### Image file viewer
```html 
<drive-viewer-image [doc]="doc"></drive-viewer-image>
```

### Video file viewer
```html 
<drive-viewer-video [doc]="doc"></drive-viewer-video>
```

