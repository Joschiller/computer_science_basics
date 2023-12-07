# HTML (HyperText Markup Language)

- [Usage](#usage)
- [References](#references)
- [Overview](#overview)
- [HTML Document](#html-document)
- [Important Tags](#important-tags)
  - [Text](#text)
    - [Structuring](#structuring)
      - [With Semantics](#with-semantics)
      - [Without Semantics](#without-semantics)
    - [Formatting](#formatting)
      - [General](#general)
      - [Code](#code)
  - [Lists](#lists)
  - [Tables](#tables)
  - [Frames](#frames)
  - [Forms](#forms)
- [General Attributes](#general-attributes)
- [Special Characters](#special-characters)
- [HTML5](#html5)

## Usage

- web devenlopment
- UI
- Today: HTML = Structure, CSS = presentation, JS = Behavior, PHP = Backend, CMS = Content Management

## References

> https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML

## Overview

- element: `<name attr="value" ...>content</name>`
  - quotes around attributes can be omitted if the value does not contain spaces
  - quotes can be single or double quotes
- comments: `<!-- ... -->`

## HTML Document

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>Page Title</title>
    ...
  </head>
  <body>
    content
  </body>
</html>
```

Structuring in HTML5:

- `<header>`: header
- `<nav>`: navigation bar
- `<main>`: main content (subsections: article, section, div)
- `<aside>`: sidebar (often included in main)
- `<footer>`: footer

## Important Tags

| Tag                | Meaning                                                                                                        | Attributes                                                                       |
| :----------------- | :------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------- |
| `<img/>`           | image                                                                                                          | src="path"<br/>height, width, alt, border                                        |
| `<a>Link Text</a>` | anchor => hyperlink<br/>should provide attributes and clear signal words e.g. for file links (file format ...) | href="url"<br/>title="description"<br/>target="\_blank" for opening in a new tab |

### Text

#### Structuring

##### With Semantics

| Tag               | Meaning   | Attributes |
| :---------------- | :-------- | :--------- |
| `<p>`             | paragraph |            |
| `<h1><h2><h3>...` | heading   |            |

##### Without Semantics

```html
<span style="css">content</span>
```

CSS Content:

- font-size
- margin
- display
- ...

#### Formatting

##### General

| Tag            | Meaning                    | Attributes                  |
| :------------- | :------------------------- | :-------------------------- |
| `<i> <em>`     | italic                     |                             |
| `<b> <strong>` | bold                       |                             |
| `<u>`          | underline                  |                             |
| `<del>`        | crossed                    |                             |
| `<blockquote>` | highlight quote            |                             |
| `<abbr>`       | highlight abbreviation     |                             |
| `<address>`    | format contact information |                             |
| `<sup> <sub>`  | Exponent; Index            |                             |
| `<time>`       | format date/time           | datetime="date/time string" |
| `<br>`         | linebreak                  |                             |
| `<hr>`         | horizontal line            |                             |

##### Code

| Tag      | Meaning            | Attributes |
| :------- | :----------------- | :--------- |
| `<code>` | format code        |            |
| `<pre>`  | keep whitespace    |            |
| `<var>`  | highlight variable |            |
| `<kdb>`  | highlight keyword  |            |
| `<samp>` | format output      |            |

### Lists

| Tag    | Meaning                                                  | Attributes |
| :----- | :------------------------------------------------------- | :--------- |
| `<ul>` | unordered list => bullet points                          |            |
| `<ol>` | ordered list => numbers                                  |            |
| `<li>` | list item of an `<ul>` or `<ol>`                         |            |
| `<dl>` | description list, consists of `<dt>` and `<dd>` elements |            |
| `<dt>` | description term                                         |            |
| `<dd>` | description definition                                   |            |

### Tables

- table > table row > table column (table data)
- Attributes: table: border; td: colspan

```html
<table>
  <tr>
    <td>...</td>
    ...
  </tr>
  ...
</table>
```

### Frames

- part of a page
- Attributes frameset: cols, rows, noresize
- Attributes frame: src

### Forms

```html
<form>
  <input />
  ...
</form>
```

Form Attributes:

- action="url" => opens webpage after finishing form
- method="..." => HTTP method

Input Attributes:

- type (e.g. radio, submit, ...)
- name
- value

## General Attributes

- boolean attributes => can simply be set by writing down their name (or leaving them out):
  disabled
- id => reference point for a hyperlink (#...)
- align (center, ...), bgcolor
- class => class of HTML elements that can be styled together in a CSS-file using .classname

## Special Characters

- `<` = `&lt;`
- `>` = `&gt;`
- `"` = `&quot;`
- `'` = `&apos;`
- `&` = `&amp;`

## HTML5

| Tag          | Meaning                              | Attributes                                      |
| :----------- | :----------------------------------- | :---------------------------------------------- |
| `<video>`    | shows video<br/>=> child: `<source>` | controls<br/>autoplay<br/>loop                  |
| `<source>`   |                                      | src="path"<br/>type=...<br/>e.g. video/mp4, ... |
| `<progress>` |                                      | min, max, value                                 |

- Web Storage: sessionStorage(), localStorage() => setItem(key, value), getItem(key)
- Geolocation API: navigator.geolocation.getCurrentPosition()
- Drag & Drop API: attribute draggable="true" => function drag(ev) { ev.dataTransfer.setData(key, value); }
- editing svg images, animations, paths
- stronger forms
