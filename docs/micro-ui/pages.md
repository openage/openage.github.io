---
banner: "![[pages.png]]"
---

# Pages
#directory #system #console #pages #www
https://www.domain.com

## Features
-   Landing/Offering Pages
-   Dashboards
-   Page Sharing via alias 
-   Dynamic forms
-   Administration
-   Brand Management
-   Page/Form Designer
-   Alias Management/Tracking
-   SEO Management
-   Usage Tracking using GA

## Library 
    
-   Landing/Offering Pages, 
-   Survey Forms, 
-   Action Pages
-   Themes (Icons, CSS, Loading Icon)
-   Widgets (Prebuilt/Other Platforms)
    
## Reports
-   Usage based on Demographics
-   Usage based on Pages
    
## Concepts 

### Page

A page consist of collection of widgets pushed into a layout, and has a url to reach there

- Examples of url
	-  `{{base-url}}/landing` 
		- `/:level1` 
		- `/:level1/:level2` 
		- `/:level1/:level2/:level3` 
	-  `{{base-url}}/home` (with role guard)
		-  `dashboard`
		-  `/:level1` 
		- `/:level1/:level2` 
		- `/:level1/:level2/:level3` 


#### Editor

https://yofs.invisionapp.com/console/share/M434WVN9P6/814696366

- 3 column layout
	- Toolbar
	- Workspace
	- Properties
- Toolbar
	- Layout - 3 Column, 2 Column ( 1-2, 2-1)
	- Container - Card, Bordered, Flat
	- Widgets ()
		- HTML
		- Graph
		- Drive
		- Table
		- Insight
	- Injectables
		- Context
- Properties (selected field)
	- Theme Picker
	- Style Editor
	- Class Picker
	- Icon Picker
	- Property Editor
	- Permission Picker
- Workspace
	- JSON View
	- Preview
	- WYSIWYG View

## Epics

**pages micro ui**

- Meta driven pages
	- [ ] ability to select a theme for the portal
	- [ ] set the master page for whole app based on the theme
- SEO and Bot Friendly Page
	- [ ] ⏫ ability to set page SEO meta
- User Tracking
- Ability to change the layout and theme of the page
	- [ ] separate the customer portal as www.domain.com/customers (with customers as base url)
		- [ ] make the urls dynamic (level 1, level 2 ...)
		- [ ] set page as internal() and external (root level - www.domain.com/customers )

	- [ ] ability to modify the layout of the pages
		- [ ] make the pages meta driven 
		- [ ] move the existing components (search ) to widgets
		- [ ] ability to edit (JSON editor) the page meta
	- [ ] ability to add new pages
		- [ ] navigation editor 
		- [ ] select a template
		- [ ] set page code and title etc
	- [ ] ability to modify pages using wysiwyg editor
		- [ ] ability to set permissions for the page
- [ ] SRP revamp
	- [ ] look and feel
	- [ ] flow revamp 
		- [ ] json driven wizard 
		- [ ] validation handler
	- [ ] widgets revamp
		- [ ] SRP Search
		- [ ] SRP Result
		- [ ] action widgets
			- [ ] login widget in actions
			- [ ] signup widget in actions
			- [ ] phone verification action
- [ ] ability to search for pages 
	- [ ] from page meta
	- [ ] from url
	- [ ] from last viewed page (from local storage)
	- [ ] parse page from the code (regex)
