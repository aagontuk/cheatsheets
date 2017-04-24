#### HTML Heading ####

**h1 to h6**: 

### AT A GLANCE ###

#### `<head>` ####

Contains title, style, script, meta informations of a page.

#### `<meta>` ####

This tag can go inside `<head>` tag. It contains meta data of an HTML page.

**Attributes:**
* charset="charset" - Describe the character encoding used in the document. Eg. UTF-8.
* name="type" - Describe different information about the document. types for name can be
    * application-name
	* author
	* description
	* keywords - Keywords about the page. Useful for search engines.
	* viewport - Describe how the page will be shown in different devices. Very useful for portability.
* http-equiv="type" - Provieds an HTTP header for the information of the content attribute. type can be:
    * refresh - To set refresh time of a page.
* content="value" - Hold values for different types specified in `name` / `http-equiv` attribute.

**Examples:**
```html
<!-- Define keywords for search engines -->
<meta name="keyword" content="HTML, Cheetsheet, Tags, Attributes">

<!-- Define description of a web page -->
<meta name="description" content="This page is about html cheatsheet">

<!--To state author of the page>
<meta name="author" content="Aagontuk">

<!-- To set character encoding -->
<meta charset="UTF-8">

<!-- To refresh page in every 15 sec -->
<meta http-equiv="refresh" content="15">

<!-- To make the page look good in every device -->
<meta name="viewport" content="width=device-width, initial-scale="1.0"">
```

#### `<body>` ####

**Attributes:**
* alink="color" - color of a link when it is clicked.
* link="color" - color of unvisited link.
* vlink="color" - color of visited link.
* background="image.png" - background image of a page if bgcolor not set.
* bgcolor="color" - background color of a page if background image not set.
* text="color" - color of the texts in the page.
