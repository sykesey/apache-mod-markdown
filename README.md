mod_markdown
============

mod_markdown is Markdown filter module for Apache HTTPD Server.

This is based on Hamano's original markdown module, with some new configuration directives

* MarkdownBodyClass [string]
  This directive adds an extra class to the BODY tag generated on output. Useful for using github-markdown CSS styles or PrismJS.

* MarkdownHeadHtml [string]
  This directive adds a custom string into the generated HEAD element. Useful for adding PrismJS.

## Dependencies

* discount

  http://www.pell.portland.or.us/~orc/Code/discount/

For Debian/Ubuntu:

~~~
# apt-get install build-essential libtool automake autoconf
# apt-get install libmarkdown2-dev apache2-dev
~~~

## Build

~~~
% autoreconf -f -i
% ./configure --with-apxs=<APXS_PATH> --with-discount=<DISCOUNT_DIR>
% make
% make install
~~~

Note: `<DISCOUNT_DIR>` is the directory that contains the include directory that contains mkdio.h
Probably you need to specify --with-discount=/usr or --with-discount=/usr/local

## Configuration
in httpd.conf:

~~~
LoadModule markdown_module modules/mod_markdown.so
~~~

You need to specify full path on debian or ubuntu.
~~~
LoadModule markdown_module /usr/lib/apache2/modules/mod_markdown.so
~~~

~~~
<Location />
    AddHandler markdown .md

    # If you want to use stylesheet.
    MarkdownCss /style/style.css
    MarkdownCss /css/prism.css
    MarkdownBodyClass github-markdown
    MarkdownHeadHtml "<script src='/js/prism.js'></script>"
    
</Location>
~~~

Or:

~~~
<Directory /var/www>
    AddHandler markdown .md
    DirectoryIndex index.md
</Directory>
~~~

Or in a .htaccess file:
~~~
MarkdownCss /style/style.css
MarkdownCss /css/prism.css
MarkdownBodyClass github-markdown
MarkdownHeadHtml "<script src='/js/prism.js'></script>"
~~~
