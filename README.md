# Clean Blog by Start Bootstrap - Jekyll Version

The official Jekyll version of the Clean Blog theme by [Start Bootstrap](http://startbootstrap.com/).

[View Live Demo &rarr;](http://blackrockdigital.github.io/startbootstrap-clean-blog-jekyll/)

## Before You Begin

In the _config.yml file, the base URL is set to /startbootstrap-clean-blog-jekyll which is this themes gh-pages preview. It's recommended that you remove the base URL before working with this theme locally!

It should look like this:
`baseurl: ""`

## What's Included

A full Jekyll environment is included with this theme. If you have Jekyll installed, simply run `jekyll serve` in your command line and preview the build in your browser. You can use `jekyll serve --watch` to watch for changes in the source files as well.

A Grunt environment is also included. There are a number of tasks it performs like minification of the JavaScript, compiling of the LESS files, adding banners to keep the Apache 2.0 license intact, and watching for changes. Run the grunt default task by entering `grunt` into your command line which will build the files. You can use `grunt watch` if you are working on the JavaScript or the LESS.

You can run `jekyll serve --watch` and `grunt watch` at the same time to watch for changes and then build them all at once.

## Support

Visit Clean Blog's template overview page on Start Bootstrap at http://startbootstrap.com/template-overviews/clean-blog/ and leave a comment, email feedback@startbootstrap.com, or open an issue here on GitHub for support.

## Unique to Richard Burd's Homepage

Several custom features are build outside of the Jekyll framework.

### Software Documentation Page
This page is under construction and utilizes an [HTML5-UP](https://html5up.net/) template  in order to reach the page's precise URI so as to get the *documentation* resource (i.e. https://richard-burd.github.io/documentation) a file called `.htaccess` needed to get added to the main directory.&nbsp; This is because the `documentation.html` file bypasses all of Jekyll's compiling and is transported directly to the `_site` folder as is, without being altered.&nbsp;  This means the usual abstractions related to navigation and styling are not applied to the *documentation* resource.&nbsp;  Additionally, when the documentation resource is being **modified and reviewed *locally***, you must navigate to http://localhost:4000/documentation.html (**that is, include the *.html***) in order to see the documentation resource as it properly references the styling and font resources in the `.documentation` directory.&nbsp; .
