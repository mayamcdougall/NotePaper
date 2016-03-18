---
Title: NotePaper Theme
Author: Simon McDougall
Date: 2016/03/10
toc:
  features: Features
  download: Download
  installation: Installation
  upgrade: Upgrading
  configuration: Configuration
  changelog: Changelog
  license: License
Tags: Documentation
---
## NotePaper Theme

Thank you for using my [NotePaper](http://development.sjmcdougall.com/pico-themes/NotePaper) theme for [Pico](http://picocms.org/).  This theme was originally inspired by the [Anarcho Notepad](https://wordpress.org/themes/anarcho-notepad/) theme for WordPress.  This is my first Pico theme, so the coding might be rough in spots, but overall I'm pleased with how it's turned out.  If you have any suggestions on how I can improve this theme, or if you discover any bugs, please create a [New Issue](https://github.com/smcdougall/NotePaper/issues) on GitHub.

If you're viewing this on GitHub, please check out the [NotePaper Site](http://development.sjmcdougall.com/pico-themes/NotePaper) for a live example of the theme.

## Features {#features}

### Widgets

The biggest feature I've brought to this theme is Widget Support.  By defining a custom meta variable in your markdown files, you can generate themed widgets that run down the right side of the page.  There are two types of widgets, named Stickies and Doodles, as well as a third, "disabled" option for those you'd like to hide temporarily.  Sticky Widgets are themed as sticky notes, while Doodle widgets are depicted as if they were drawn onto the page.  To make a widget, add "Widget: Sticky", "Widget: Doodle", or "Widget: Disabled" to the header of any markdown file in your content folder.

Widgets are organized by Pico's built-in page ordering.  If, for example, you sort your content by ascending date, then I would recommend organizing your widgets using date values (Date: 1001, Date: 1002, Date: 1003) to organize your widgets.  If you're using alphabetical page ordering, you could order them by changing the metadata names of the widgets to start with letters (A,B,C).  If your pages are in descending order, then just reverse the numbering or lettering you use (C,B,A / Z,Y,X / 1003, 1002, 1001 / etc).

The "Doodle" area is 200px wide, and works great for images, just be sure to size them accordingly.  If your image is less than 200px wide, you may want to pad the image to 200px or use html + css to center it.

Image locations (or any other paths) within widgets must be defined with an absolute path from your base_url (e.g. "&#37;base_url&#37;/assets/doodle.png").  Because of how Pico imports content, relative paths are not recommend and are known to cause issues.  See Pico's [Documentation](http://picocms.org/docs.html) for additional information about file paths.

Like regular pages, widgets can be written in markdown, html, or a combination of the two.  Just make sure they end in ".md" (or the file extension you chose in your config) so Pico can find them.

* **Note:** The SideBar theme's widgets can sometimes continue outside of the main content area on short pages.  This behavior has been fixed in the default NotePaper theme, but requires a small rewrite of SideBar.  It will be fixed in the next release.

### Front Page

I've also included a simple blog-style front page feature.  If enabled in your Pico config, the theme will ignore your main index.md.  Instead, it will import the first few content files it finds into one long page.  Depending on what you've set Pico's "pages_order" setting to be, the front page will be your most recent pages, your very first pages, your first pages alphabetically, or your last pages alphabetically.  By default, it will import five pages, though you can change this with a config option.

The Front Page Mode can also have pagination support, allowing you to navigate through multiple pages of results after the initial limit.  At present, this feature requires an [optional plugin](#plugin), though this will hopefully change in the future.

There's also a "blog mode" meta variable.  If you add "Blog: True" to your meta header, your page will be hidden from the main navigation and only accessible through the front page or first/prev/next/last buttons.

### Sub-Navigation
This feature takes a YAML table of contents and generates a sub-navigation for the current page.  This table of contents is defined as a meta variable named "toc" in your markdown file.  The formatting is simple: Using spaces, indent each item of the toc by the same amount.  Tabs will *not* work, and will cause your page to throw an exception.  The key of each item must match the name of its corresponding html anchor, but its value can be anything you want.  This value will become the text displayed for your link.  You may also have a second level of items, indented further, within another item.  The first item of a new level is used to title its parent.  In the example below, its key is "&#95;title", but it doesn't matter what you use.  Here is an example of the proper formatting, as used in this readme.  Note that I added a second level under "installation" for the sake of the example.

```
toc:
  features: Features
  download: Download
  installation:
    _title: Installation
    step-1: Step 1
    step-2: Step 2
    step-3: Step 3
  upgrade: Upgrading
  configuration: Configuration
  changelog: Changelog
  license: License
```

### Bottom Navigation Links
There are optional navigation links you can enable for the bottom of your page.  These are enabled using a custom config option, and are incredibly customizable.  There are five links total, First, Prev, Back to Top, Next, and Last.  You can set the text or an image for each one, or disable them individually.  You can also define a text character or image to use as a separator between them.  A set of default images for these buttons is included in NotePaper.

### Comments

I've integrated Disqus and Facebook comments into the theme.  They can be enabled in your Pico config.  There's also an option of whether or not to display them on your front page, and various settings to customize their appearance.

Please note that both Disqus and Facebook pull in a a large number of extra scripts and resources.  These extra scripts are part of how these comment systems work, but can have an impact on the performance of your website.

These comment systems also have privacy implications for your users as both (Facebook especially) are known to track users across the web (sometimes even if they are not logged in!).  These comment engines are provided as a convenience, however if you feel they might infringe on your users' privacy, simply disable them.

All comments code is contained within an "if" statement in NotePaper's Twig template.  Twig is processed on the server through PHP, so if you have comments disabled, **no scripts or other resources will be pulled in or sent to your users!**  This also helps keep NotePaper modular and stops it from being slowed down by disabled features.

### Custom Themes

NotePaper has support for full custom CSS themes.  These themes reside in "assets/NotePaper_Themes/".  NotePaper themes can be defined globally using config options, but can also be assigned on a page-by-page basis using the "Theme" meta variable.  The theme defined in your metadata will always overrule the theme defined in your config.  You can also set a page to use NotePaper's default theme instead of the one defined in your config.  To do this, simply set your metadata theme value to "Default" (e.g. "Theme: Default").

Two sample themes are included with NotePaper:
	* WritingDesk is a simple palette swap of NotePaper, providing a lighter color scheme.
	* SideBar is a more full-featured theme, which trades Sticky Notes and Doodles for a sidebar.

These themes will be updated with NotePaper in the future, and more may be added as well.  Feel free to create your own themes as well.  You can even use the one of the sample themes as a base for your own!

The structure of these themes is simple:  The theme "name" is just the name of the folder, and your CSS file should be named "theme.css" and placed inside it.  You should place any other assets in the folder as well and access them in your CSS as needed.

### Override Styles

You can override the default CSS styles of the theme by specifying an overriding stylesheet in your Pico config.  Your stylesheet will be linked after both NotePaper's default stylesheet and any Theme's stylesheet, so you only need to style the elements you'd like to change.

Override Styles are best used if you have one or two elements that you want to change about NotePaper (or one of its themes).  If you'd like to do a major overhaul of its appearance, try creating a custom "NotePaper Theme" instead.  This will give you more flexibility when choosing the appearance of your site, and will save the Override stylesheet for when you might need to override a few elements of your own theme.

### Search

NotePaper includes a very basic search function that can search page titles, descriptions, and content for a single search term.  At the moment, the search is treated as a solid string, so if you search for multiple words, it will only find them *exactly* as you typed them.

There is a sample search widget included with NotePaper.  You may use it as is, modify it, or create your own version.

The search feature requires the [optional plugin](#plugin) in order to function.

### Tag Widgets

NotePaper includes two optional, tag-based widgets.  These widgets operate by reading a "Tags" meta variable from every page.  Tags should be a list of items, separated by commas.  Spaces in tag names are not yet supported, but will be added in the future.  A properly formatted tag list would look like this: "Tags: One,Two,Red,Blue".  Note that even if the tag widgets are enabled, they will not display if no tags are found in your content.

The Tag List widget will display all tags in a list.  The Tag Cloud widget will display a block of tags, with more common tags appearing larger than less common tags.  Text sizes start at 2em and are reduced from there.  You can specify how many size increments to use in your config file.

Both widgets have the option to display the number of occurrences in parentheses next to the tag name.  They can be sorted either alphabetically or numerically (by number of occurrences).  If you don't specify a sorting method, they'll be displayed in rather chaotically, in the order Pico discovers them (dependent on your Pico config and the order you've written them in).  They can also be ordered in reverse order.  The heading text of either widget can be specified in the config as well.

Clicking on a tag in either widget will do a search for all pages labeled with that tag.

* **Note:** While the Tag Widgets do not themselves require it, the [optional plugin](#plugin) *is* required in order to make the tags searchable.  This will hopefully change in the future.

### Folder Navigation (Experimental)

Folder Navigation will break up your Table of Contents into separate widgets based on your folder structure.  Pages in the root of your content folder will appear as normal in the Table of Contents.  Pages inside folders will be organized into separate widgets based on this first level of folder.  Any deeper folders will be rendered as pop-up menus when you hover on their name.

Folder names will be automatically converted into Title Case (allowing you to use lowercase folder names) and any underscores "&#95;" will be converted to spaces.  This name converting scheme is hard-coded at the moment, but I will likely add customization in the future.

* This feature is labeled as **Experimental** due to one major bug: The menus it generates often get rendered underneath other widgets on default theme.  Themes that do not use Transformations on widgets (such as SideBar), do not suffer from this issue.  This is really the only issue I've found with it, and the only thing keeping me from labeling it "Stable".  If this issue doesn't effect your use-case, feel free to try it out.  Also, the issue only really becomes apparent on the menus because they float over the other widgets.  If you only have one level of folders inside your content folder, this feature should work just fine for you.
	* The issue is caused due to how browsers render Transformations (of the Sticky Notes), pulling them out of the regular z-index context.
	* There is a partial workaround coded, but at the moment it's only working in Firefox.

## Download {#download}
You can download the NotePaper theme [on GitHub](https://github.com/smcdougall/NotePaper/releases).


## Installation {#installation}

Selectively extract the contents of the download into your Pico folder.
* Everything in the "themes" folder is required for the theme to function.
* The "content" folder holds the sample widgets you see here.  You can install these as well and use them as a template for your own widgets, or you can leave them out and write yours from scratch.
* The "assets/NotePaper_Themes" folder contains the additional sample themes.
* The "config" folder contains a sample NotePaper config.  The easiest way to configure NotePaper is to place the sample config, `NotePaper-Config.php.sample` in your config folder, and rename it `NotePaper-Config.php`.  Then add "`include 'NotePaper-Config.php';`" to the bottom of your Pico config.  Alternatively, you can copy the NotePaper array from the sample file and paste it into your pico config (just be sure not to copy the first "`<?php`" line).

Finally, don't forget to update your config.php to use the NotePaper Theme.  It should read:

`$config['theme'] = 'NotePaper';`

While you're at it, you'll likely want to modify the config options [discussed below](#configuration).  They add quite a few levels of extra customization.

### Plugin {#plugin}

Several of the features of this theme require the use of a small plugin.  The purpose of this plugin is to pass the Query String variables along to Twig, something that Pico does not do by default.  This will hopefully change in the future.

* **Disclaimer:** Despite writing this plugin, I am *not* a plugin developer.  This plugin is incredibly basic, and should work perfectly fine.  I am not a PHP developer however, so I am unable to provide support for this plugin in any way.  I'm providing it because, in my testing and development, it worked just fine.

The plugin does two things, and *only* two things.  First, it passes on Query String data to Twig in a variable named "TwigGetUrl".  Next, it defines a new variable "TwigGetUrlEnabled" as True.  This second variable is used to determine whether the plugin is active or not.

There is a small possibility that the use of this plugin could create a security risk.  In my tests, I have been unable to break anything with it.  I am not a security expert however and do not know all the ins and outs of Pico, PHP, and Twig.  As far as I can tell, there should be *no* added risk to running this plugin, but I unfortunately cannot guarantee this.

In the future, I will be searching for a better way to accomplish these features, hopefully without needing a plugin.

## Configuration {#configuration}

Here is a list of all the custom configuration options you can utilize in this theme.  The config options are arranged in a series of nested arrays for readability and ease of use.  You can comment out any options you don't wish to use by adding a `//` to the beginning of the line or by wrapping a section in `/* */`.  If you comment out one of the nested arrays, be sure to comment out that *entire array* and not just the header.  Also, please note that date_format is now ignored in this theme.  The date format is instead hard-coded to work around the lack of ordinal suffixes in strftime (used by Pico 0.9 and later).

#### site_logo
If this variable is defined, your site's title will be replaced with this image file.  It must be defined as an absolute path from your base_url (e.g. "assets/site_logo.png").

#### og_image
"Open Graph" Image.  You can specify an image to be used when sharing a link on Facebook and other sites that support it.  Since this theme has a dark background by default, this provides a nice workaround for light logos not displaying against Facebook's white background.  You can use Facebook's [Debugging Tool](https://developers.facebook.com/tools/debug/) to help diagnose any issues using this feature.

#### copyright
This text string will be displayed in the footer of your website.

#### description_length

The Search and Tag views use meta.description for listing search results.  Here, you can define the character length of automatic descriptions for files that are lacking a meta.description.  The automatic descriptions will be rounded down to the previous space so as to not truncate any words.  An ellipsis is also added to the end of the description.

#### css

* **theme**

	Here you can specify a custom CSS Theme for NotePaper to use.  The theme name is simply the name of the folder.  Two extra themes are included by default, WritingDesk and SideBar.

* **override**

	You can override the default styles of this theme by entering in the path to a custom CSS stylesheet.  This must be defined as an absolute path from your base_url (e.g. "assets/override.css").  The CSS Override file is applied last, after both the default NotePaper styles and the CSS Theme.  This means that it can override any styles in either of those files.

	For example, you could try changing the page background using CSS.  By doing this in the override file, you don't have to overwrite the original background image.  I'd recommend trying any of the wood textures [here](http://webtreats.mysitemyway.com/8-tileable-dark-wood-texture-patterns/) or [here](http://webtreats.mysitemyway.com/tileable-light-wood-textures/) for and quick and seamless change.  One of them is already being used as the default background.  You may also want to re-save them with a higher level of jpg compression, as they're quite large.

* **fonts**

	You can add custom fonts to NotePaper by adding them here.  Inside the array parentheses, enter the urls to your font's stylesheet, in quotes and separated by commas.

	An easy way to include custom fonts is to use Google Fonts, but you can also link to your own stylesheets.

	As an example, your config should look like this:
	```
	'fonts'  => array('https://fonts.googleapis.com/css?family=Roboto','https://fonts.googleapis.com/css?family=Ubuntu'),
	```

* **mirrorwidgets**

	By default, NotePaper's widgets are placed on the right side of the page.  This option flips widgets to the left side of the page instead.

#### toc

* **text**

Table of Contents.  This is the text that will display above your navigation (the sticky note in the top right).

* **folder**

Experimental Folder Navigation.  If enabled, your Table of Contents will be broken up into categories based on your folder structure.

#### tags

* **sort**

	* **method**

	Sorts tags by name or occurrence. Use 'alphabetical' to sort by name, 'numerical' to sort by occurrence, or leave blank.  Blank doesn't sort, causing tags to be in the order they first appear as Pico reads your files (which is rather chaotic).

	* **reverse**

	This will reverse the sorting order.  Alphabetical will start at Z and Numerical will start with the least used tag.

* **list,cloud**

	* **enabled**

		Enables the individual widget.

	* **title**

		Text to use for the header of the individual widget.

	* **total**

		If enabled, tags will display the total number of occurrences in parentheses.

	* **levels**

		Only for Tag Cloud.  Number of text sizes to use when sorting tags.  The more levels however, the less variation there will be between one size and the next.  Text size starts at 2em and goes down by increments based on the number of levels.  If there are fewer tag occurrences than you've specified for levels, the number of levels is automatically reduced to match the largest number of tag occurrences.

#### front_page

* **enabled**

	If enabled, your site's main index.md will be ignored in favor of a blog-style front page.

* **limit**

	This is the number of articles that will be displayed on your front page, should you use the front page feature.

#### comments

* **type**

	Set this to either 'disqus' for disqus comments or 'facebook' for facebook comments.  Leave it blank to disable comments altogether.

* **front**

	If enabled, comments will also be displayed on your front page.  This works regardless of whether you are using a normal front page or the front page mode feature.

* **Discus Options**

	* **shortname**

	This is a unique identifier given to you by Disqus.  Enter it here to link your site to your Discus account.  You don't need to copy any other code that Disqus provides you with, it is already included in the theme.

* **Facebook Options**

	* **limit**

	This is the number of comments to display by default, without having to click "Load More Comments"

	* **admin_type**

	Type of comments administration.  You can use either multiple Facebook User ID's or a single Facebook App ID to moderate your comments.  Set this to "user" if using User ID's or "app" if using an App ID.

	* **admin_id**

	Here you can specify the moderators for your comments.  This option uses an array, so make sure to place your input inside the parentheses.  If you're using User ID's, wrap each ID in quotes and separate them with commas.  If you're using an App ID, just place it in quotes inside the parentheses.

	* **dark**

	The default color scheme for Facebook comments is "light".  Enabling this will set them to use their "dark" theme, if you find it's a better match for your website.

	* **order**

	This is the order to display comments in.  Your options are "social", "time", and "reverse_time".  Social displays comments by popularity, in a "top comment" fashion. "time" displays them in chronological order, with the oldest at the top.  "reverse_time" displays the newest comments first.  Will default to "social" if left undefined.

#### bottom_links

* **enabled**

	Enables additional navigation links (First, Prev, Back to Top, Next, Last) at the bottom of pages.  Use 'blog' to only display on pages with meta.blog set.   Bottom Links are always enabled on Front Page Mode unless explicitly disabled below, and always enabled for Search results and Tag search results.

* **first, prev, next, last, top, separator**

	* **text**

		Here you can customize the text for each button.  If you leave this blank, it will disable that button.  When using images, this text becomes the hover text for each button.  If you do not wish to have any hover text, use a space " " instead of leaving blank so that the button stays enabled.  Don't forget to escape any html entities you might be using, such as &lt; or &gt;.

	* **image**

		You can optionally provide an image for each button, relative to base_url.  If defined, the "text" variables will instead be used as Alt and Title attributes of your image.  If you use the value of "default", NotePaper will use it's own internal button images.

#### disable

* **header, date, toc, front_page_buttons**

	Here, you can disable each of these individual page elements.  Disabling the Header will remove the Title, Author, and Date from showing at the top of the page.  Disabling the Date will hide just the Date Ribbon.  ToC hides the table of contents.  Front Page Buttons will hide the navigation buttons from the bottom of the front page, which normally show in Front Page Mode even if Bottom_Links are disabled.

## Upgrading {#upgrade}

If you're upgrading from a previous version of NotePaper, the best way to upgrade is to replace your old `NotePaper-Config.php` file (or array) with the new version and then migrate your old config values into the new fields.

This is because NotePaper is constantly improving and the structure of NotePaper's config array is continuously changing to make room for new options and to refine old ones.  Replacing the old file (or array) with the new one ensures that any changes made since the last version will not cause problems for your website.

All other NotePaper files can just be removed/replaced as usual.  You may want to remove your old NotePaper files first, just in case some of them have moved around since the last version.

## Changelog {#changelog}

### 1.5.1 - 03/10/16
Fixed two minor papercuts:
* Made automatically generated `og:description` use the value of `description_length`.
* Removed `overflow: hidden;` from SideBar's `.site_title h1`, as it was cutting off the descenders of letters like j, g, y, etc.

### 1.5.0 - 02/29/16
* Many Config Changes, see new Sample Config file.
* Many new Config options, including:
	* Ability to disable various page components.
	* Ability to embed custom fonts.
* Option to flip Widgets to left side of the page.
* Support for full CSS themes, in addition to regular overrides.
* Ability to select a different CSS theme for every file using a meta variable.
* Two sample themes:
	* WritingDesk, a recolor of NotePaper's default theme.
	* SideBar, a redesigned layout with a sidebar instead of stickies and doodles.
* Option to use Facebook comments instead of Disqus.
* Better Open Graph support.
* Many rewrites and under-the-hood changes.
* More "Responsive Design" on small screens.
* YAML Error Message Handling
* Recursive ToC's for pages.  Sub-Navigation will go as many levels deep as you write.
	* "&#95;title" is no longer needed. Child menus are detected automatically.
* Many other code refinements.
* Experimental Folder Navigation.
* New Features, Requiring Plugin (For now; Subject to Change in Pico 1.1):
	* Tag List and Tag Cloud
	* Front Page Mode Pagination
	* Search function and widget.

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
