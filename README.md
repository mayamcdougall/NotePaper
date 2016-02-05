---
Title: NotePaper Theme
Author: Simon McDougall
Date: 2015/12/03
toc:
  features: Features
  download: Download
  installation: Installation
  changelog: Changelog
  license: License
---
## NotePaper Theme

Thank you for using my [NotePaper](http://development.sjmcdougall.com/pico-themes/NotePaper) theme for [Pico](http://picocms.org/).  This theme was originally inspired by the [Anarcho Notepad](https://wordpress.org/themes/anarcho-notepad/) theme for WordPress.  This is my first Pico theme, so the coding might be rough in spots, but overall I'm pleased with how it's turned out.  If you have any suggestions on how I can improve this theme, or if you discover any bugs, please create a [New Issue](https://github.com/smcdougall/NotePaper/issues) on GitHub.

If you're viewing this on GitHub, please check out the [NotePaper Site](http://development.sjmcdougall.com/pico-themes/NotePaper) for a live example of the theme.

## Features {#features}

### Widgets

The biggest feature I've brought to this theme is Widget Support.  By defining a custom Meta Header in your markdown files, you can generate themed widgets that run down the right side of the page.  There are two types of widgets, named Stickies and Doodles, as well as a third, "disabled" option for those you'd like to hide temporarily.  Sticky Widgets are themed as sticky notes, while Doodle widgets are depicted as if they were drawn onto the page.  To make a widget, add "Widget: Sticky", "Widget: Doodle", or "Widget: Disabled" to the header of any markdown file in your content folder.

Widgets are organized by Pico's built-in page ordering.  If, for example, you sort your content by ascending date, then I would recommend organizing your widgets using date values (Date: 1001, Date: 1002, Date: 1003) to organize your widgets.  If you're using alphabetical page ordering, you could order them by changing the meta names of the widgets to start with letters (A,B,C).  If your pages are in descending order, then just reverse the numbering or lettering you use (C,B,A / Z,Y,X / 1003, 1002, 1001 / etc).

The "Doodle" area is 200px wide, and works great for images, just be sure to size them accordingly.  If your image is less than 200px wide, you may want to pad the image to 200px or use html + css to center it.

Image locations (or any other paths) within widgets must be defined with an absolute path from your base_url (eg "&#37;base_url&#37;/assets/doodle.png").  Because of how Pico imports content, relative paths are not recommend and are known to cause issues.  See Pico's [Documentation](http://picocms.org/docs.html) for additional information about file paths.

Like regular pages, widgets can be written in markdown, html, or a combination of the two.  Just make sure they end in ".md" (or the file extension you chose in your config) so Pico can find them.

Be careful not to make widgets longer than your page content.  If you do, they'll break out of the frame and continue on their own.  I haven't yet been able to code them in a way that restricts them to the length of the main content (without making them look worse in the process).

### Front Page

I've also included a rudimentary blog-style front page feature.  If enabled in your Pico config, the theme will ignore your main index.md.  Instead, it will import the first few content files it finds into one long page.  Depending on what you've set Pico's "pages_order" setting to be, the front page will be your most recent pages, your very first pages, your first pages alphabetically, or your last pages alphabetically.  By default, it will import five pages, though you can change this with a config setting.

There's also a "blog mode" Meta Header.  If this header is defined in your markdown (eg "Blog: Yes" or "Blog: anything"), your page will be hidden from the main navigation and only accessible through the front page or first/prev/next/last buttons.

At the moment this feature is a bit limited though.  There is currently no way to "load more" pages after the initially defined limit.  In the future, I'll expand more on this feature or replace it with Pico's Pagination Plugin.  Unfortunately, NotePaper's widget system makes it incompatible with this plugin in it's current state.

### Sub-Navigation
This feature takes a Markdown table of contents and generates a sub-navigation for the current page.  This table of contents is defined as a Meta Header named "toc" in your markdown file.  This is an experimental feature at the moment.  Use it with caution, as it **will break your site if you format the toc incorrectly**.  (A future version will hopefully address this issue and/or supply an error message instead of breaking entirely).  The formatting is simple: Using spaces, indent each item of the toc by the same amount.  Tabs will *not* work, and will cause your site to break.  The header of each item must match the name of its corresponding html anchor, but its value can be anything you want.  This value will become the text displayed for your link.  You may also have a second level of items, indented further, within another item.  Just label the first entry of the second level "&#95;title".  Here is an example of the proper formatting, as used in this readme.  Note that I added a second level under "installation" for the sake of the example.

```
toc:
  features: Features
  download: Download
  installation:
    _title: Installation
    step-1: Step 1
    step-2: Step 2
    step-3: Step 3
  changelog: Changelog
  license: License
```

### Bottom Navigation Links
There are optional navigation links you can enable for the bottom of your page.  These are enabled using a custom config option, and are incredibly customizable.  There are five links total, First, Prev, Back to Top, Next, and Last.  You can set the text or an image for each one, or disable them individually.  You can also define a text character or image to use as a separator between them.

### Disqus comments

I've integrated Disqus comments into the theme.  They can be enabled them in your Pico config.  There's also an option of whether or not to display them on your front page.

### Custom Styles

You can override the default CSS styles of the theme by specifying an overriding stylesheet in your Pico config.  Your stylesheet will be linked after the theme's original stylesheet, so you only need to style the elements you'd like to change.

## Download {#download}
You can download the NotePaper theme [on GitHub](https://github.com/smcdougall/NotePaper/releases).


## Installation {#installation}

Selectively extract the contents of the download into your Pico folder.  Everything in the "themes" folder is required for the theme to function.  The "content" folder holds the sample widgets you see here.  You can install these as well and use them as a template for your own widgets, or you can leave them out and write yours from scratch.

Finally, don't forget to update your config.php to use the NotePaper theme.  It should read:

`$config['theme'] = 'NotePaper';`

While you're at it, you'll likely want to add in the custom variables discussed below.  They aren't required for the theme, but I do recommend checking them out as they add quite a few levels of extra customization.

### Custom Config Variables

Here is a list of all the custom Pico config options you can utilize in this theme.  The config options are arranged in a series of nested arrays for readability and ease of use.  I'd recommended adding this entire block to the end of your Pico "config.php" file, then modifying it to fit your preferences.  You can comment out any options you don't wish to use by adding a `//` to the beginning of the line or by wrapping a section in `/* */`.  If you comment out one of the nested arrays, be sure to comment out that *entire array* and not just the header.  Also, please note that date_format is now ignored in this theme.  The date format is instead hard-coded to work around the lack of ordinal suffixes in strftime (used by Pico 0.9 and later).

<pre style="overflow-x: scroll;"><code>
$config['NotePaper'] = array(
	#Basic Config
	'site_logo'      => 'assets/site_logo.png',	// Site logo, reletive to base_url.
	'og_image'       => 'assets/site_logo_og.png',	// Facebook "Open Graph" Image.  Specify an image to be used when sharing a link on Facebook.  Provides a nice workaround for light logos not displaying on Facebook.
	'toc'            => 'Table of Contents',	// Text for the "Table of Contents" header.
	'copyright'      => 'Copyright © 20XX - Your Name',	// Copyright or other text for page footer.
	'css_override    => 'assets/override.css',	// Override theme styles with custom stylesheet, relative to base_url.

	#Front Page Mode
	'front_page'     => array(
		'enabled'    => '',	// If defined, your index.md will be ignored for a blog-style front page.
		'limit'      => 5	// Limit the number of items in Front Page Mode. Defaults to 5 if undefined.
		),
	#Disqus
	'disqus'         => array(
		'enabled'    => 'yes',	// Enable Disqus. Use "front" if you want Disqus on your front page as well.  Blank is disabled.  Any other value will enabled.
		'shortname'  => 'your-shortname-here'	// The unique identifier given to you by Disqus.
		),
	#Bottom Links
	'bottom_links'   => array(
		'enabled'    => 'yes',	// Adds links to page bottoms: First, Prev, Back to Top, Next, Last.  Use "Blog" to only display on pages with meta.blog set.  Blank is disabled. Any other value will enabled.
		'first'      => array(
			'text'   => '&amp;lt;&amp;lt; First',	//Text for "First" button at the bottom of the page.  Blank to disable any given button.
			'image'  => 'default'	//Image for "First" button, relative to base_url.  If defined, the "text" variables will instead be used as Alt and Title attributes.  Use "default" for internal button images.
		),
		'prev'       => array(
			'text'   => '&amp;lt; Prev',	//Text for "Prev" button.
			'image'  => 'default',	//Image for "Prev" button.
		),
		'next'       => array(
			'text'   => 'Next &amp;gt;',	//Text for "Next" button.
			'image'  => 'default',	//Image for "Next" button.
		),
		'last'       => array(
			'text'   => 'Last &amp;gt;&amp;gt;',	//Text for "Last" button.
			'image'  => 'default', //Image for "Last" button.
		),
		'top'        => array(
			'text'   => 'Back to Top',	//Text for the "Back to Top" button.
			'image'  => 'default',	//Image for the "Back to Top" button.
		),
		'separator'  => array(
			'text'   => '|',	//Character to use as a separator between buttons.
			'image'  => 'default'	//Image to use as a separator between buttons.
		)
	)
);
</code></pre>

#### site_logo
If this variable is defined, your site's title will be replaced with this image file.  It must be defined as an absolute path from your base_url (eg "assets/site_logo.png").

#### og_image
"Open Graph" Image.  You can specify an image to be used when sharing a link on Facebook and other sites that support it.  Since this theme has a dark background by default, this provides a nice workaround for light logos not displaying against Facebook's white background.  You can use Facebook's [Debugging Tool](https://developers.facebook.com/tools/debug/) to help diagnose any issues using these features.

#### toc
Table of Contents.  This is the text that will display above your navigation (the sticky note in the top right).

#### copyright
This text string will be displayed in the footer of your website.

#### css_override
You can override the default styles of this theme by entering in the path to a custom CSS stylesheet.  This must be also defined as an absolute path from your base_url (eg "assets/override.css").

For example, you could try changing the page background using CSS.  By doing this in the override file, you don't have to overwrite the original background image.  I'd recommend trying any of the wood textures [here](http://webtreats.mysitemyway.com/8-tileable-dark-wood-texture-patterns/) or [here](http://webtreats.mysitemyway.com/tileable-light-wood-textures/) for and quick and seamless change.  One of them is already being used as the default background.  You may also want to resave them with a higher level of jpg compression, as they're quite large.

#### front_page

* **enabled**

	If this variable is defined, your site's main index.md will be ignored in favor of a blog-style front page.

* **limit**

	This is the number of articles that will be displayed on your front page, should you use the optional front page feature.

#### disqus

* **enabled**

	If this variable is defined, Disqus support will be enabled.  If this variable is set to "front", Disqus will also be enabled on your front page.  This works regardless of whether you are using a normal front page or the front page mode feature.  Leaving this variable blank will disable Disqus integration.

* **shortname**

	This is a unique identifier given to you by Disqus.  Enter it here to link your site to your Discus account.  You don't need to copy any other code that Disqus provides you with, it is already included in the theme.

#### bottom_links

* **enabled**

	Enables additional navigation links (First, Prev, Back to Top, Next, Last) at the bottom of pages.  At the moment, due to the lack of proper pagination, these are not enabled on the Front Page when using Front Page Mode. Use "Blog" to only display on pages with meta.blog set.  Blank is disabled. Any other value will enabled.

* **first, prev, next, last, top, separator**

	* **text**

		Here you can customize the text for each button.  If you leave this blank, it will disable that button.  When using images, this text becomes the hover text for each button.  If you do not wish to have any hover text, use a space " " instead of leaving blank so that the button stays enabled.  Don't forget to escape any html entities you might be using, such as &lt; or &gt;.

	* **image**

		You can optionally provide an image for each button, relative to base_url.  If defined, the "text" variables will instead be used as Alt and Title attributes of your image.  If you use the value of "default", NotePaper will use it's own internal button images.

## Changelog {#changelog}

### 1.4.0 - 12/03/15
* Updated for Pico 1.0.  Older versions unsupported, stick to 1.3.2.
* Major Rewrite.  Cleaned up a large amount of code.
* Removed "#" code from 1.3.2 because this url hack has been fixed in Pico 1.0.
* Sub-Navigation support now supplements the removed "#" code.
* Renamed "ToC" in config to "toc" for consistency.
* Open Graph image option for Facebook Shares.
* Widgets are now tagged with the "Widget" Meta Header.  Folder location is now irrelevant.
* "Blog" Meta Header hides pages from Navigation.
* First, Prev, Next, Last link options for the bottom of your pages.
* Added styles to inline images (a max-width and rounded corners).
* Added styles to the &lt;pre&gt; tag.
* Added margins to site title/logo
* Optimized Config using arrays.

### 1.3.2 - 10/31/15
* Last version to support Pico 0.9.
* Added a check for a "#" when constructing the front page.  I've been using blank documents, with names containing "#" and that only contain the Pico header, for linking to anchors on other pages.  Now the front page will ignore them instead of printing a header and nothing else.
* Added the version number and url to the top of index.html and style.css.

### 1.3.1 - 06/19/15
* Added code that hides the main index.md in the Table of contents if front page mode is enabled.
* Added code that ignores index.md's title attribute when setting the title of the front page if front page mode is enabled.
* My original intention was to just remove the index.md file altogether, but that caused the page title to reference 404.md.
* In my efforts to make it ignore everything about index.md however, I've indirectly made it work either way (with or without an index.md).  How about that.

### 1.3.0 - 06/19/15
* Changed front_page_mode to a config option to prevent empty list item created in Table of Contents when using the old method (having an empty index.md).

### 1.2.0 - 06/12/15
* Added support for custom CSS stylesheets
* Fixed errors in Readme about subfolders and needing to use absolute paths.

### 1.1.0 - 06/06/15
* Updated for Pico 0.9

### 1.0.0 - 06/05/15
* Initial Release

## License {#license}

This theme is free software under the terms of the GNU General Public License v3.  Please see the included LICENSE file for details.

Please use and/or modify it as you see fit.

You may also comment out the author credit text in the footer of the page if you feel it interferes with your website.
