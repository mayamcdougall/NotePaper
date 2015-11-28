## ★ NotePaper for Pico 1.0 is almost ready! ★
If you desperately need it, please download from the testing branch.  It may contain some comments or other junk, but should otherwise be fully functional.  The documentation is the main item left to finish, so expect some inconsistancies and hold-overs from 1.3.2.  A proper release will be coming out shortly.

Also, the new version will be properly documented here on GitHub.  The content below is copied directly from my site and has not been modified for GitHub, so just keep that in mind while reading it.  To see it in it's original form, please visit:

###http://development.sjmcdougall.com/pico-themes/NotePaper

##NotePaper Theme

Thank you for using my [NotePaper](http://development.sjmcdougall.com/pico-themes/NotePaper) theme for [Pico](http://picocms.org/).  This theme is loosly based on the [Anarcho Notepad](https://wordpress.org/themes/anarcho-notepad/) theme for Wordpress.  This is my first Pico theme, so the coding might be rough in spots, but overall I'm pleased with how it's turned out.  If you have any suggestions on how I can improve this theme, feel free to [contact me](malto:simon@sjmcdougall.com).

<a name="features"></a>
##Features

###Widgets

The biggest thing I've tried to bring to this theme is Widget Support.  By placing markdown files into "content/widgets", you can generate themed widgets that run down the right side of the page.  There are three subfolders for widgets, named "stickies", "doodles", and "disabled".  Widgets in the "stickies" folder are themed as sticky notes, while widgets in the "doodles" folder are depicted as if they were drawn onto the page.

Widgets are organized by Pico's built-in page ordering.  I would recommend ordering content by ascending date, then using single digit date values (1,2,3) to organize your widgets.  Alternatively, you could change the internal names of the widgets to start with letters (A,B,C) and order them on a site using Alphabetical page ordering.

The "doodles" area is 200px wide, and works great for images, just be sure to size them accordingly.  If your image is less than 200px wide, you may want to pad the image to 200px or use html + css to center it.

Image locations (or any other paths) within widgets must be defined with an absolute path (starts with a / ) from your document root (eg "/content/widgets/doodles/doodle.png").  Because of how Pico imports content, relative paths will get determined based on your current url, not in relation to the file's original location.  If you don't use an absolute path, subfolder pages will not be able to load your image properly.

Also, like regular pages, widgets can be written in markdown, html, or a combination of the two.  Just make sure they end in ".md" or Pico won't find them.

Be careful not to make widgets longer than your page content.  If you do, they'll break out of the frame and continue on their own.  I haven't yet been able to code them in a way that restricts them to the length of the main content.

###Front Page

I've also included a rudimentary blog-style front page feature.  If enabled in your Pico config, the theme will ignore your main index.md.  Instead, it will import the first few content files it finds into one long page.  Depending on what you've set Pico's "pages_order" setting to be, the front page will be your most recent pages, your very first pages, your first pages alphabetically, or your last pages alphabetically.  By default, it will import five pages, though you can change this with a config setting.

I'll admit that the code for this feature is a bit sloppy, and was a little difficult to get working.  In the future, I may try to integrate support for Pico's Pagination plugin as a better option.

###Disqus comments

I've integrated Disqus comments into the theme.  They can be enabled them in your Pico config.  There's also an option of whether or not to display them on your front page.

###Custom Styles

You can override the default CSS styles of the theme by specifying an overriding stylesheet in your Pico config.  Your stylesheet will be linked after the theme's original stylesheet, so you only need to style the elements you'd like to change.

<a name="download"></a>
##Download
You can download the NotePaper theme here: [Download](content/NotePaper.zip)

<a name="installation"></a>
##Installation

Extract the contents of the download into your Pico folder.  Everything in the "themes" folder is required for the theme to function.  The "content" folder holds the sample widgets you see here.  You can install these as well and use them as a template for your own widgets, or you can leave them out and write yours from scratch.

Finally, don't forget to update your config.php to use the NotePaper theme.  It should read:

> $config['theme'] = 'NotePaper';

While you're at it, you may want to add in the custom variables discussed below.  They aren't required for the theme, but I do recommend checking them out.

This Readme is also included in the theme's directory in case you need to refresh your memory in the future.

###Custom Config Variables

Here is a list of all the custom Pico config options you can utilize in this theme.  I'd recommended adding this entire block to the end of your Pico "config.php" file, then modifying it to fit your preferences.  Also, please note that date_format is now ignored in this theme.  The date format is instead hard-coded to work around the lack of ordinal suffixes in strftime (used by Pico 0.9).


> $config['site_logo'] = '/content/site_logo.png';	// Site logo.  Absolute path from document root (start with / ).
> $config['front_page_mode'] = ''; // If defined, index.md will be ignored for a blog-style front page.
> $config['front_page_limit'] = 5;	// Limit Items on Front Page  
> $config['ToC'] = 'Table of Contents';	// Text for the "Table of Contents" header.  
> $config['copyright'] = 'Copyright © 20XX - Your Name';	// Copyright or other text for page footer  
> $config['disqus'] = 'yes';	// Enable Disqus. Use "front" if you want Disqus on your front page as well. Blank is disabled. Any other value will enabled.  
> $config['disqus_shortname'] = 'your-shortname-here' // The unique identifier given to you by Disqus  
> $config['css_override'] = '/content/css-override.css'; // Override theme styles with custom stylesheet using "path/to/override.css".  Absolute path from document root (start with / ).

####site_logo

If this variable is defined, your site's title will be replaced with this image file.  It must be defined as an absolute path from your document root (start your path with a / ).  If you don't use an absolute path, subfolder pages will not be able to properly find your logo.


####date_format

This date format is what I'd recommend for the theme.  It's a personal preference, and entirely up to you.  Keep in mind however, that this format is used for the date printed on the red ribbon.  Using another format may break the appearance of the ribbon.  The recommended format includes a line-break `<br>` tag which separates the month from the date.


####front_page_mode

If this variable is defined, your site's main index.md will be ignored in favor of a blog-style front page.  More details are available above, under features.


####front_page_limit

This is the number of articles that will be displayed on your front page, should you use the optional front page feature.


####ToC

Table of Contents.  This is the text that will display above your navigation (the sticky note in the top right).


####copyright

This text string will be displayed in the footer of your website.


####disqus

If this variable is defined, Disqus support will be enabled.  If this variable is set to "front", Disqus will also be enabled on your front page.  This works regardless of whether you are using a normal front page or the theme's front page feature.  Leaving this variable blank will disable Disqus integration.


####disqus_shortname

This is a unique identifier given to you by Disqus.  Enter it here to link your site to your Discus account.  You don't need to copy any other code that Disqus provides you with, it is already included in the theme.


####css_override

You can override the default styles of this theme by entering in the path to a custom CSS stylesheet.  This must be also defined as an absolute path from your document root (start your path with a / ).  If you don't use an absolute path, subfolder pages will not be able to properly find your stylesheet.

For example, you could try changing the page background using CSS.  By doing this in the override file, you don't have to overwrite the original background image.  I'd recommend trying any of the wood textures [here](http://webtreats.mysitemyway.com/8-tileable-dark-wood-texture-patterns/) or [here](http://webtreats.mysitemyway.com/tileable-light-wood-textures/) for and quick and seamless change.  One of them is already being used as the default background.  You may also want to resave them with a higher level of jpg compression, as they're quite large.


<a name="changelog"></a>
##Changelog

###1.3.2 - 10/31/15
* Added a check for a "#" when constructing the front page.  I've been using blank documents, with names containing "#" and that only contain the Pico header, for linking to anchors on other pages.  Now the front page will ignore them instead of printing a header and nothing else.
* Added the version number and url to the top of index.html and style.css.

###1.3.1 - 06/19/15
* Added code that hides the main index.md in the Table of contents if front page mode is enabled.
* Added code that ignores index.md's title attribute when setting the title of the front page if front page mode is enabled.
* My original intention was to just remove the index.md file altogether, but that caused the page title to reference 404.md.
* In my efforts to make it ignore everything about index.md however, I've indirectly made it work either way (with or without an index.md).  How about that.

###1.3 - 06/19/15
* Changed front_page_mode to a config option to prevent empty list item created in Table of Contents when using the old method (having an empty index.md).

###1.2 - 06/12/15
* Added support for custom CSS stylesheets
* Fixed errors in Readme about subfolders and needing to use absolute paths.

###1.1 - 06/06/15
* Updated for Pico 0.9

###1.0 - 06/05/15
* Initial Release

<a name="license"></a>
##License

This theme is free software under the terms of the GNU General Public License v3.  Please see the included LICENSE file for details.

Please use and/or modify it as you see fit.

You may also comment out the author credit text in the footer of the page if you feel it interferes with your website.
