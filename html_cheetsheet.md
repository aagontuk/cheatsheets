# INDEX #
1. [\<html\>](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#html)
2. [\<head\>](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#head)
3. [\<meta\>](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#meta)
4. [\<body\>](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#body)
5. [\<h1\> - \<h6\> for heading](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#h1-to-h6)
6. [\<hr\ for horizontal line>](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#hr)
7. [\<p\> for paragraph](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#p)
8. [\<pre\> to preserve line breaks](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#pre)
9. [Formatting Tags](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#formatting-tags)
10. [Quotations](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#quotations)
    1. [Quoting using quotation mark](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#quoting-with-quotation-mark)
    2. [Quoting using \<blockquote\>](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#quoting-using-blockquote)
    3. [\<abbr\> for Abbreviation](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#abbr-for-abbreviation)
    4. [\<address\> for Contact Information](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#address-for-contact-information)
    5. [Citation](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#cite)
11. [HTML color](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#html-color)
12. [HTML & CSS](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#css-and-html)
    1. [Inline CSS](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#inline-css)
    2. [Internal CSS](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#internal-css)
        1. [Internal CSS using id](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#html-id-example)
        2. [Internal CSS using class](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#html-class-example)
    3. [External CSS](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#extarnal-css)
13. [\<a\> For links](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#a-for-links)
14. [\<img\> For images](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#img-for-images)
15. [\<table\> For tables](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#table-for-tables)
16. [HTML Lists](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#html-lists)
17. [HTML Forms](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#html-form)
    1. [\<input\> for various input area](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#input-for-various-types-of-input-area)
    2. [Example of an HTML form with all the tags and attributes](https://github.com/aagontuk/cheatsheets/blob/master/html_cheetsheet.md#example-of-an-html-form-with-all-the-tags-and-attributes)

### `<html>` ###
---

**Attributes:**
* `lang="language"` - Specifies language used in the document. Example lang="en-US".

### `<head>` ###
---

Contains title, style, script, meta informations of a page.

### `<meta>` ###
---

This tag can only go inside `<head>` tag. It contains meta data of an HTML page.
`<meta>` tag has no ending tag.

**Attributes:**
* `charset="charset"` - Describe the character encoding used in the document. Eg. UTF-8.
* `name="type"` - Describe different information about the document. types for name can be
    * `application-name`
	* `author`
	* `description`
	* `keyword` - Keywords about the page. Useful for search engines.
	* `viewport` - Describe how the page will be shown in different devices. Very useful for portability.
* `http-equiv="type"` - Provieds an HTTP header for the information of the content attribute. type can be:
    * `refresh` - To set refresh time of a page.
* `content="value"` - Hold values for different types specified in `name` / `http-equiv` attribute.

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

### `<body>` ###
---

**Attributes:**
* `alink="color"` - color of a link when it is clicked.
* `link="color"` - color of unvisited link.
* `vlink="color"` - color of visited link.
* `background="image.png"` - background image of a page if bgcolor not set.
* `bgcolor="color"` - background color of a page if background image not set.
* `text="color"` - color of the texts in the page.

### `<h1> to <h6>` ###
---

Creates headlines in html document.

### `<hr>` ###
---

Creates a horizontal line. Used for styling the document.

**Attributes:**
* `align` - Specifies alignment.
* `size="pixel"` - Specifies height in pixel. Eg. size="10"
* `width="x%"` - Specifies width in %. Eg. width="50%"
* noshed - Line will be of a solid color.

### `<p>` ###
---

Creates a paragraph. Omit any line breaks(extra space, tab etc).

### `<pre>` ###
---

Use fixed width font. Preserve line breaks.

### Formatting Tags ###
---

* `<b>` - Bold Text.
* `<i>` - Italic Text.
* `<u>` - Underline.
* `<strong>` - Strong Text.
* `<em>` - Emphasized Text.
* `<small>` - Samll Text.
* `<sup>` - Superscript.
* `<sub>` - Subscript.
* `<mark>` - Marked Text. Text with some background color.
* `<del>` - Deleted Text. Striked.
* `<ins>` - Inserted Text. Underlined.

### Quotations ###
---

#### Quoting with quotation mark ####

Texts under `<q>` tag are placed under quotation mark.

#### Quoting using `<blockquote>` ####

`<blockquote>` is used to quote text from another source.
Text under `<blockquote>` are indented.
```html
<p>Here is some information about Themis:</p>
<blockquote cite="https://en.wikipedia.org/wiki/Themis">
Themis is an ancient Greek Titaness. She is described as
"[the Lady] of good counsel", and is the personification of
divine order, fairness, law, natural law and custom.
Her symbols are the Scales of Justice, tools used to remain balanced and pragmatic.
</blockquote>
```

#### `<abbr>` for Abbreviation ####

`<abbr>` is used for abbreviation. Show full form under cursor.
```html
<p>
	Richard M. Stallman is the creator of the <abbr title="GNU is not Unix">GNU</abbr> system.
</p>
```

#### `<address>` for Contact Information ####

```html
<address>
Luke Skywalker</br>
Naboo System</br>
</address>
```

#### `<cite>` ####

`<cite>` is used for mentioning the title of someone's work.
```html
<p><cite>Star Wars</cite> directed by George Lucas</p>
```

### HTML Color ###
---

Color can be specified in three way.

1. Using color name. [List of standard color names](https://www.w3schools.com/colors/colors_names.asp)
```html
<p style="color: red">This is a red text</p>
```
2. Using RGB value.
```html
<p style="color: rgb(0, 255, 0)">This is a green text</p>
```
3. Using hexadecimal value.
```html
<p style="color: #808080">This text is Ass</p>
```

### CSS And HTML ###
---

CSS is used for decoration. Three ways to use CSS in HTML.

#### Inline CSS ####

Inline CSS is used to decorate each tag individualy using the `style` attribute.
```html
<p style="font-family: garamond; color: red;">We want freedom in the web</p>
```

#### Internal CSS ####

Internal CSS is used to decorate the whole HTML document. `<style>` tag in used
inside `<head>` to decribe CSS properties.
```html
<!DOCTYPE html>

<html>
	<head>
		<title>HTML Document</title>

		<style>
			h3 {
				font-size: 50px;
				text-align: center;
			}

			p {
				font-family: garamond;
				color: blue;	
			}
		</style>
	</head>

	<body>
		<h3> Internal CSS Example </h3>
		<p> Internal CSS is decribed using <q>style<q> tag </p>
	</body>
</html>
```

To identify each tag separately **id** and **class** can be used.

##### HTML id Example #####
```html
<!DOCTYPE html>

<html>
	<head>
    	<title>Internal CSS</title>
        
        <style>
        	h3 {
            	font-size: 30px;
                font-family: garamond;
            }
            
            #p01 {
            	color: red;
                font-size: 14px;
            }
            
            #p02 {
            	color: green;
                font-size: 20px;
            }
        </style>
    </head>
    
    <body>
    	<h3> Internal CSS Example using id </h3>
    	<p id="p01"> This is first paragraph </p>
        <p id="p02"> This is second paragraph </p>
    </body>
</html>
```

##### HTML class Example #####
```html
<!DOCTYPE html>

<html>
	<head>
    	<title>Internal CSS</title>
        
        <style>
        	h3 {
            	font-size: 30px;
                font-family: garamond;
            }
            
            p.redText {
            	color: red;
                font-size: 14px;
            }
            
            p.greenText {
            	color: green;
                font-size: 20px;
            }
        </style>
    </head>
    
    <body>
    	<h3> Internal CSS Example using class </h3>
    	<p class="redText"> This text should be red </p>
        <p class="greenText"> This text should be green </p>
    </body>
</html>
```

#### Extarnal CSS ####

Separate CSS file is used. `<link>` tag is used to use the file in the document.
```html
<head>
	<link rel="stylesheet" href="style.css">
</head>
```

### `<a>` for Links ###

See W3Schools.

### `<img>` for Images ###

See W3Schools. Some interesting features:
* **Floating property**
* `<map>` tag.

### `<table>` for Tables ###

See W3Schools. Example:
```html
<table style="width:100%">
	<tr>
    	<th>Title 1</th>
		<th>Title 2</th>
	</tr>
	<tr>
		<td> Cell 1</td>
		<td> Cell 2</td>
</table>
```

### HTML Lists ###

See W3Schools. Interesting:

* Description List.
* Creating a Menu using list and CSS.

### HTML Form ###

For creating HTML forms for getting data from user.
Froms are created using `<form></form>` tag. Forms normaly contains:

* `<input>` - Creating various types of inputs. Text, button, radio button, checbox etc.
* `<select>` - For creating a drop down list.
* `<textarea>` - For creating a large text field.
* `<label>` - For creating label for various inputes.
* `<fieldset>` - For specifying different input group. `<legend>` tag is used for labeling `<fieldset>`.

**Important Attributes:**

* `action="process_file_address"` - Specifies the sever side sript which will process the submitted data.
* `method="get/post"` - `get` for plain text submit. `post` for encrypted submit.
* `name="form_name"` - Specifies the name of the form.
* `id=""` - ID of the form.
* `autocomplete="on/off"` - Turn on/off browser autocomplete feature.
* `enctype=""` - Specifies how the data will be encrypted when send to the server.
* `accept="file_type"` - Specifies comma separated file types that will be allowed for upload.
* `target=""` - Specifies where submit response will be shown(New tab, own page etc).

#### `<input>` for various types of input area ####

In `type` attribute input types are specified.
It can be:

* `type="text"` - For simple text area.
* `type="password"` - For taking passwords.
* `type="radio"` - For radio buttons.
* `type="checkbox"` - For checkbox.
* `type="file"` - For uploading file.
* `type="button"` - Creating a button. When the button is clicked it works based on `onclick="scrpit_to_execute"` attribute.
* `type="submit"` - Creates a submit button for the form. When the submit button is clicked action is taken based on the `action` attribute of the form.
* `type="reset"` - Creates a button for resetting the form.
* `type="image"` - Defines an image as a submit button.
* `type="range"` - Creates a range slider.
* `type="number"` - Creates a number picker.
* `type="color"` - Creates a color picker.
* `type="date"` - Creates a date picker.
* `type="tel"` - Telephone number form.

**Important Attributes:**

* `name=""` - Specifies the name of an `<input/>` element.
* `value=""` - Specifies the value of an `<input>` element. This can be used for setting default value.
* `placeholder=""` - This text is shown faded in the text fields.
* `size=""` - Maximum character input size for an input field.
* `max=""` - Maximum accepted value for number, range, date type.
* `min=""` - Minimum accepted value for number, range, date type.
* `step=""` - Step size for slider or number picker.
* `pattern=""` - Specifies a regular expression against which input is validated.
* `title=""` - Text that is show when input dont pass regex validation.
* `autocomplete="on/off"` - on/off browser autocomplete feature.
* `autofocus="on/off"` - Will autofocus to this input field when the page loads.
* `checked` - Make a checkbox / radio button as checked.
* `disabled` - To disable an input field.
* `multiple` - User can enter multiple values in an input element.
* `readonly` - Specifies a input field as readonly. It can't be changed.
* `required` - Specifies a field as required.
* `accept="file_type1, file_type2"` - Accepted file types. Comma separated for multiple file type acceptence.
* `formaction=""` - Specifies the script that will process this input field when the form submitted.
* `formmethod="get/post"` - Which method to follow for form submission.
* `formenctype=""` - Submitted data encryption type.
* `formtarget=""` - Specifies where the response will be placed for this input(New tab, own page etc).

#### Example of an HTML form with all the tags and attributes ####

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
	<body>
		<h2 class="header"> Create an Account in Hell NOW! </h2>

		<form action="process.php" method="post" autocomplete="on">
			<fieldset>
				<legend>Basic Information</legend>
				Your Name:&nbsp;
				<input type="text" name="name" value="name" placeholder="Name" size="40" autofocus="on"/><br/>
				Your Gender:<br/>
				<input type="radio" name="gender" value="male"/>Male<br/>
				<input type="radio" name="gender" value="female"/>Female<br/>
				<input type="radio" name="gender" value="other" checked="checked"/>Other<br/>
				Married?<br/>
				<input type="checkbox" name="married" value="no" checked="checked"/>No<br/>
				<input type="checkbox" name="married" value="yes"/>Yes</br>
			</fieldset>

			<fieldset>
				<legend>Insanity Check</legend>
				Pick <span class="color">Red</span> color:&nbsp;
				<input type="color" name="color" value="blue"><br/>
				What is the value of &Pi;:&nbsp;
				<input type="number" name="pi" value="3" min="1" max="9" step="2"/><br/>
				Can you slide for no reason?&nbsp;
				<input type="range" name="slide" value="50" min="0" max="100" step="2"/>
			</fieldset>

			<fieldset>
				<legend>Create Username</legend>
				Username:&nbsp;
				<input type="text" name="uname" placeholder="username" pattern="[A-Za-z]{6}" label="Only letters and upto six characters" required/><br/>
				Password:&nbsp;
				<input type="password" name="pass" pattern="[A-Za-z0-9]{6}" label="Only letters and numbers upto 6 characters" required/><br/>
				Upload Image:<br/>
				<input type="file" name="image"/>
			</fieldset>

			Want to meet god?<br/>
			<label name="meetYes">Yes</label>
			<input type="radio" name="god" value="yes" id="meetYes" disabled="disabled"/><br/>
			<label name="meetNo">No</label>
			<input type="radio" name="god" value="no" id="meetNo" disabled="disabled"/><br/>
			<input type="submit" value="Register!"/>
			<input type="reset"/>
		</form>
	</body>
</html>
```
