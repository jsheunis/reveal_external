# External.js

This is a plugin for Reveal.js. It allows you to specify external files to be loaded into a presentation. This extension also allows external files in already external files (Subfiles). It allows a course, which may be hundreds of slides, to be broken into modules and managed individually.

This version of the plugin has been modified to be compatible with the latest Reveal.js (5, at the time of writing).
 
## Installation

Download external/external.js and save it to your project structure. E.g.:

```
MyProject
.
├── myslides.html
└── reveal.js
    └── plugin
        └── external
            └── external.js
```


## Example

Example usage available at: https://hub.datalad.org/edu/slides


## Using external.js

Using the plugin is easy. Include it in your reveal slides like this:

```html
<script src="../reveal.js/dist/reveal.js"></script>
<script src="../reveal.js/plugin/external/external.js"></script>
<script>
Reveal.initialize({
	...
	plugins: [ RevealExternal ]
})
</script>
```

Then simply add an element into your presentation with a `data-external` or `data-external-replace` attribute.

### `data-external`

Will put the loaded content into the node with the `data-external` attribute.

```html
<section data-external="module_01/index.html"> </section>
```

### `data-external-replace`

Will replace the node with the loaded content. 

```html
<section data-external-replace="module_02/index.html"> </section>
```

### Load Fragments

You can specify a CSS selector to add only a part of the loaded content.

For example, use `#.slides > section` to ensure only the actual slide nodes are pulled in from another Reveal slide deck:

```html
<section data-external-replace="short.html#.slides > section"></section>
```

Additional examples:
- To load a single element by id, use `##<element-id>`.
- To load all elements with a class, use `#.<class-name>`.

### Options 

```javascript
external: {
    mapAttributes: ['src']
}
```

By default the plugin will convert relative paths (dot as first character) in `src` attributes. This
allows you to specify the path relative to the file you're in, rather then the one it is included in.

Set `mapAttributes` to `false` to disable, or provide an array of attribute names.

### Recursion

If you want to load external files, you have to choose relative paths in the `data-external*`-attribute. In the following there is a simple example of how to include many files in one reveal presentation: 

Folder structure:

```
- __includes__
	- __chapter1__
		- 	__chapter1_1__
			- index1_1.html 
		-  __chapter1_2__
			- index1_2.html 
		-  index_1.html
	- __chapter_2__
		- index_2.html
	- __chapter_3__
		- index_3.html
- index.html
```

Code of index.html: 

```html
<div class="reveal">
    <!-- Any section element inside of this container is displayed as a slide -->

    <div class="slides">
         <section data-external="includes/chapter1/index_1.html"> </section>
         <section data-external="includes/chapter2/index_2.html"> </section>
         <section data-external="includes/chapter3/index_3.html"> </section>
    </div> <!-- slides -->

</div> <!-- Reveal -->
```

Now you may wish to include the subchapters 1.1 and 1.2 to the content of chapter 1. This would be the code of index_1.html:

```html
	<section data-external="chapter1_1/index1_1.html"> </section>
	<section data-external="chapter1_2/index1_2.html"> </section>
```

Remember that all the paths entered in "data-external" were relative!

It is also possible to include files outside of _section_-tags, as this would result in seperate slides. If you don't want the included content to be a new slide, you can include the content to another element, too (e.g. a _div_).

```html
	<div data-external="chapter1_1/index1_1.html"> </div>
```

## Credits

Previous version by [Jan Schoepke](https://github.com/janschoepke) ("Thanks to [Thomas Weinert](https://github.com/ThomasWeinert) for massive improvements in version 1.3!"), originally by [Cal Evans](https://github.com/calevans),

License: MIT
