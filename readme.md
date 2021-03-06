Overview
=============

Bootstrap3-wysihtml5 is a javascript plugin that makes it easy to create simple, beautiful wysiwyg editors with the help of [wysihtml5](https://github.com/xing/wysihtml5) and [Twitter Bootstrap 3](http://getbootstrap.com/).
It based on the Project [http://jhollingworth.github.io/bootstrap-wysihtml5/](http://jhollingworth.github.io/bootstrap-wysihtml5/)

[![Circle CI](https://circleci.com/gh/Rise-Vision/bootstrap3-wysihtml5/tree/master.svg?style=svg)](https://circleci.com/gh/Rise-Vision/bootstrap3-wysihtml5/tree/master)

Examples
=============

[http://schnawel007.github.com/bootstrap3-wysihtml5](http://schnawel007.github.com/bootstrap3-wysihtml5/)

Quick Start
=============

[Download the latest version of bootstrap-wysihtml5](https://github.com/schnawel007/bootstrap3-wysihtml5/).

Files to reference
=============

```html
<link rel="stylesheet" type="text/css" href="lib/css/bootstrap.min.css" /> <!-- Please use the newest Version of Bootstrap 3.0.X -->
<link rel="stylesheet" type="text/css" href="src/bootstrap-wysihtml5.css" />
<script src="lib/js/wysihtml5-0.3.0.js" type="text/javascript"></script>
<script src="lib/js/jquery-1.7.2.min.js" type="text/javascript"></script>
<script src="lib/js/bootstrap.min.js" type="text/javascript"></script>
<script src="src/bootstrap3-wysihtml5.js" type="text/javascript"></script>
```

Usage
=============

```html
<textarea id="some-textarea" placeholder="Enter text ..."></textarea>
<script type="text/javascript">
	$('#some-textarea').wysihtml5();
</script>
```

You can get the html generated by getting the value of the text area, e.g.

```javascript
$('#some-textarea').val();
```

Advanced
=============

Options
-------------

An options object can be passed in to .wysihtml5() to configure the editor:

```javascript
$('#some-textarea').wysihtml5({someOption: 23, ...})
```

### Buttons

To override which buttons to show, set the appropriate flags:

```javascript
$('#some-textarea').wysihtml5({
	"font-styles": true, //Font styling, e.g. h1, h2, etc. Default true
	"emphasis": true, //Italics, bold, etc. Default true
	"lists": true, //(Un)ordered lists, e.g. Bullets, Numbers. Default true
	"html": false, //Button which allows you to edit the generated HTML. Default false
	"link": true, //Button to insert a link. Default true
	"image": true, //Button to insert an image. Default true,
	"color": false, //Button to change color of font
	"size": 'sm' //Button size like sm, xs etc.
});
```

### Custom Templates for Toolbar Buttons

To define custom templates for buttons, you can submit a customTemplates hash with the new definitions.  Each entry should be a function which expects 'locale' and optional 'options' to manage the translations.

For example, the default template used for the editHtml mode button looks like this (with size fetched from the optional 'options')

```html
<li>
  <div class='btn-group'>
    <button class='btn btn-" + size + "' data-wysihtml5-action='change_view' title='" + locale.html.edit + "'><i class='icon-pencil'></i></a>"
  </div>
</li>
```

You can change it to not use the pencil icon (for example) by defining the custom template like this:

```javascript
var myCustomTemplates = {
  html : function(locale) {
    return "<li>" +
           "<div class='btn-group'>" +
           "<a class='btn btn-default' data-wysihtml5-action='change_view' title='" + locale.html.edit + "'>HTML</a>" +
           "</div>" +
           "</li>";
  }
}

// pass in your custom templates on init
$('#some-textarea').wysihtml5({
   customTemplates: myCustomTemplates
});
```


This will override only the toolbar template for html, and all others will use the default.


### Stylesheets

It is possible to supply a number of stylesheets for inclusion in the editor `<iframe>`:

```javascript
$('#some-textarea').wysihtml5({
	"stylesheets": ["/path/to/editor.css"]
});
```

### Events

Wysihtml5 exposes a "number of events":https://github.com/xing/wysihtml5/wiki/Events. You can hook into these events when initialising the editor:

```javascript
$('#some-textarea').wysihtml5({
	"events": {
		"load": function() {
			console.log("Loaded!");
		},
		"blur": function() {
			console.log("Blured");
		}
	}
});
```

###  Shallow copy by default, deep on request

Options you pass in will be added to the defaults via a shallow copy.  (see "jQuery.extend()":http://api.jquery.com/jQuery.extend/ for details). You can use a deep copy instead (which is probably what you want if you're adding tags or classes to parserRules) via 'deepExtend', as in the parserRules example below.

###  Parser Rules

If you find the editor is stripping out tags or attributes you need, then you'll want to extend (or replace) parserRules.  This example extends the defaults to allow the ```<strong>``` and ```<em>``` tags, and the class "middle":

```javascript
$('#some-textarea').wysihtml5('deepExtend', {
  parserRules: {
    classes: {
      "middle": 1
    },
    tags: {
      strong: {},
      em: {}
    }
  }
});
```

There's quite a bit that can be done with parserRules; see "wysihtml5's advanced parser ruleset":https://github.com/xing/wysihtml5/blob/master/parser_rules/advanced.js for details.  bootstrap-wysihtml5's default parserRules can be found "in the source":https://github.com/jhollingworth/bootstrap-wysihtml5/blob/master/src/bootstrap-wysihtml5.js (just search for 'parserRules' in the file).

###  Defaults

You can change bootstrap-wysihtml5's defaults by altering:

```javascript
$.fn.wysihtml5.defaultOptions
```

This object has the same structure as the options object you pass in to .wysihtml5().  You can revert to the original defaults by calling:

```javascript
$(this).wysihtml5('resetDefaults')
```

Operations on the defaults are not thread-safe; if you're going to change the defaults, you probably want to do it only once, after you load the bootstrap-wysihtml plugin and before you start instantiating your editors.

##  The underlying wysihtml5 object

You can access the "wysihtml5 editor object":https://github.com/xing/wysihtml5 like this:

```javascript
var wysihtml5Editor = $('#some-textarea').data("wysihtml5").editor;
wysihtml5Editor.composer.commands.exec("bold");
```


##  I18n

You can use Bootstrap-wysihtml5 in other languages. There are some translations available in the src/locales directory. You can include your desired one after the plugin and pass its key to the editor. Example:

```html
<script src="src/locales/bootstrap-wysihtml5.pt-BR.js"></script>
<script type="text/javascript">
  $('#some-textarea').wysihtml5({locale: "pt-BR"});
</script>
```

It is possible to use custom translations as well. Just add a new key to $.fn.wysihtml5.locale before calling the editor constructor.

**Facilitator**

[Donna Peplinskie](https://github.com/donnapep "Donna Peplinskie")
