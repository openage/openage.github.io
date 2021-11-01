# Static Content

## Getting the content

Drive would serve as the source of static assets. This content would mainly be HTML. The owner of this content would be **system admin** (`owner-code=system`) and can be grouped into folders (like `folder-code=root|faq`). You can get them as collection using `files?folders-code={code}` or individually using the `files/{code}`

Here are some of the user cases

### Collection of files

- List of Introductory content

GET `{{api-root-url}}/drive/api/files?folder-code=root|intro&owner-code=system&tenant-code=splitz`

- List of Slides

GET `{{api-root-url}}/drive/api/files?folder-code=root|slides&owner-code=system&tenant-code=splitz`

- Get FAQ

GET `{{api-root-url}}/drive/api/files?folder-code=root|faq&owner-code=system&tenant-code=splitz`

### Individual files

- Get a welcoming video

GET `{{api-root-url}}/drive/api/files/welcome?folder-code=root|info&owner-code=system&tenant-code=splitz`

- Get TnC

GET `{{api-root-url}}/drive/api/files/tnc?folder-code=root|info&owner-code=system&tenant-code=splitz`

- Get Privacy Policy

GET `{{api-root-url}}/drive/api/files/privacy-policy?folder-code=root|info&owner-code=system&tenant-code=splitz`

- Get About Us

GET `{{api-root-url}}/drive/api/files/about-us?folder-code=root|info&owner-code=system&tenant-code=splitz`

## Creating and Editing the Content

Static content can be added to folders by posting content to the following URL

POST `{{api-root-url}}/drive/api/files`

- Add Into Content

```json
{
    "code": "slide-1",
    "name": "Slide 1 title",
    "description": "This is Slide 1 Summary",
    "content": {
        "body": "This is Slide 1 details",
    },
    "folder": {
        "code": "root|intro"
    },
    "owner": {
        "code": "system"
    },
    "tags": ["into"],
    "viewer": "html",
    "isPublic": true
}
```

- Create FAQ

```json
{
    "code": "faq-1",
    "name": "FAQ 1 Question",
    "description": "This is FAQ 1 Summary",
    "content": {
        "body": "This is FAQ 1 details",
    },
    "folder": {
        "code": "root|faq"
    },
    "owner": {
        "code": "system"
    },
    "tags": ["faq", "doubts"],
    "viewer": "html",
    "isPublic": true
}
```

- Create About Us

```json
{
    "code": "about-us",
    "name": "About Us",
    "description": "This is AU Summary",
    "content": {
        "body": "This is AU details",
    },
    "folder": {
        "code": "root|info"
    },
    "owner": {
        "code": "system"
    },
    "tags": ["tnc", "policies", "about"],
    "viewer": "html",
    "isPublic": true
}
```

- Create Privacy Policy

```json
{
    "code": "privacy-policy",
    "name": "Privacy Policy",
    "description": "This is PP Summary",
    "content": {
        "body": "This is PP details",
    },
    "folder": {
        "code": "root|info"
    },
    "owner": {
        "code": "system"
    },
    "tags": ["tnc", "policies", "privacy"],
    "viewer": "html",
    "isPublic": true
}
```

- Create TnC

```json
{
    "code": "tnc",
    "name": "Terms and Conditions",
    "description": "This is TnC Summary",
    "content": {
        "body": "This is TnC details",
    },
    "folder": {
        "code": "root|info"
    },
    "owner": {
        "code": "system"
    },
    "tags": ["tnc", "policies", "info"],
    "viewer": "html",
    "isPublic": true
}
```

- Upload Welcome Video

upload video file to
POST `{{api-root-url}}/drive/api/files?code=welcome&folder-code=root|info&owner-code=system&isPublic=true`
