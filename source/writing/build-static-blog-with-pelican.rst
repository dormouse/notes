Build Static Blog With Pelican
==============================

:date: 2015-03-10 13:55:57
:modified: 2017-02-08 13:55:57
:slug: build-static-blog-with-pelican
:tags: pelican, blog
:category: software
:author: Dormouse Young
:summary: Build static blog with pelican.

Quick start
------------

Setup environment and install software::

    $ mkdir pelican_blog
    $ cd pelican_blog
    $ mkvirtualenv pelican_blog
    $ pip install pelican markdown beautifulsoup4

Pelican quickstart::

    $ pelican-quickstart

You will see blow::

    Welcome to pelican-quickstart v3.5.0.

    This script will help you create a new Pelican-based website.

    Please answer the following questions so this script can generate the files
    needed by Pelican.


    > Where do you want to create your new web site? [.]
    > What will be the title of this web site? Dormouse Hole
    > Who will be the author of this web site? Dormouse.Young
    > What will be the default language of this web site? [en] zh
    > Do you want to specify a URL prefix? e.g., http://example.com   (Y/n)
    > What is your URL prefix? (see above example; no trailing slash) http://http://dormouse.github.io
    > Do you want to enable article pagination? (Y/n)
    > How many articles per page do you want? [10]
    > Do you want to generate a Fabfile/Makefile to automate generation and publishing? (Y/n)
    > Do you want an auto-reload & simpleHTTP script to assist with theme and site development? (Y/n)
    > Do you want to upload your website using FTP? (y/N)
    > Do you want to upload your website using SSH? (y/N)
    > Do you want to upload your website using Dropbox? (y/N)
    > Do you want to upload your website using S3? (y/N)
    > Do you want to upload your website using Rackspace Cloud Files? (y/N)
    > Do you want to upload your website using GitHub Pages? (y/N) y
    > Is this your personal page (username.github.io)? (y/N) y
    Done. Your new project is available at /home/dormouse/project/pelican_blog

Now we have following files in folder::

    content            fabfile.py  output          publishconf.py
    develop_server.sh  Makefile    pelicanconf.py

Get plugins::

    $ git clone git://github.com/getpelican/pelican-plugins.git

Get theme:

    $ mkdir pelican-themes
    $ cd pelican-themes/
    $ git clone https://github.com/robulouski/voidy-bootstrap.git

Or you can test all themes, notice use "recursive"::

    $ git clone --recursive git://github.com/getpelican/pelican-themes ./pelican-themes

Edit pelicanconf.py as following::

    #!/usr/bin/env python
    # -*- coding: utf-8 -*- #
    from __future__ import unicode_literals

    AUTHOR = u'Dormouse.Young'
    AUTHOR_EMAIL = u'dormouse.young@gmail.com'
    SITENAME = u'Dormouse Hole'
    SITEURL = 'https://dormouse.github.io'
    TAGLINE = 'Simple is better.'
    PATH = 'content'
    TIMEZONE = 'Asia/Shanghai'
    DEFAULT_LANG = u'zh'
    DEFAULT_DATE_FORMAT = ('%Y-%m-%d')

    # Feed generation is usually not desired when developing
    FEED_ALL_ATOM = None
    CATEGORY_FEED_ATOM = None
    TRANSLATION_FEED_ATOM = None
    AUTHOR_FEED_ATOM = None
    AUTHOR_FEED_RSS = None
    DEFAULT_PAGINATION = 10

    # Blogroll
    LINKS = (('Pelican', 'http://getpelican.com/'),
             ('Python.org', 'http://python.org/'),
             ('Jinja2', 'http://jinja.pocoo.org/'),
            )

    # Social widget
    SOCIAL = (('Github', 'https://github.com/dormouse'),
            )

    # Uncomment following line if you want document-relative URLs when developing
    RELATIVE_URLS = True

    # Theme
    THEME = 'pelican-themes/elegant-1.3'
    SITESUBTITLE ='Simple is better.'
    STYLESHEET_FILES = ("pygment.css", "voidybootstrap.css",)
    CUSTOM_ARTICLE_FOOTERS = ("taglist.html", "sharing.html", )
    CUSTOM_SCRIPTS_ARTICLE = "sharing_scripts.html"
    SIDEBAR = "sidebar.html"

    DISQUS_SITENAME = "dormouseyoung"

Themes which I like is:

* elegant
* `pelican-bootstrap3
  <https://github.com/getpelican/pelican-themes/tree/master/pelican-bootstrap3>`_
* pelican-sundow
* voidy-bootstrap

Edit publishconf.py as following:

.. code-block:: python

    #!/usr/bin/env python
    # -*- coding: utf-8 -*- #
    from __future__ import unicode_literals

    # This file is only used if you use `make publish` or
    # explicitly specify it as your config file.

    import os
    import sys
    sys.path.append(os.curdir)
    from pelicanconf import *

    SITEURL = 'https://dormouse.github.io'
    RELATIVE_URLS = False

    FEED_ALL_ATOM = 'feeds/all.atom.xml'
    CATEGORY_FEED_ATOM = 'feeds/%s.atom.xml'

    DELETE_OUTPUT_DIRECTORY = True

    # Following items are often useful when publishing

    DISQUS_SITENAME = "dormouseyoung"
    #GOOGLE_ANALYTICS = ""

Make some floders::

    $ cd content
    $ mkdir articles files images pages

Write first blog::

    $ vim articles/hello.rst

Blog content like this::

    ==============================
    Build Static Blog With Pelican
    ==============================

    :date: 2015-03-10 13:55:57
    :modified: 2017-02-08 13:55:57
    :slug: build-static-blog-with-pelican
    :tags: pelican, blog
    :category: write
    :author: Dormouse Young
    :summary: Build static blog with pelican

    Setup environment and install software::

        mkdir pelican_blog
        cd pelican_blog
        mkvirtualenv pelican_blog
        pip install pelican markdown beautifulsoup4

preview local html::

    make devserver


Add Favicon
-----------

http://iconifier.net is helpful. Upload your pic and get a zip file which
include all size files within.


Auto Github Push
------------------

Modify Makefile. Add::

    GITHUB_DIR=~/project/dormouse.github.io/

Chang "github" part as following::

    github: publish
    rm -rf $(GITHUB_DIR)/*
    cp -r  $(OUTPUTDIR)/* $(GITHUB_DIR)
    cd $(GITHUB_DIR) && git add --all && git commit -m 'update' && git push origin $(GITHUB_PAGES_BRANCH)


Add License
------------

I choose Attribution-NonCommercial-ShareAlike 4.0 International
(CC BY-NC-SA 4.0) and copy code from http://creativecommons.org/choose/ .


Reference
--------------

* `Configuring Pelican Static Blog <http://pbpython.com/pelican-config.html>`_
* `使用 Pelican + Markdown + GitHub Pages 来撰写 Blog
  <http://www.tuicool.com/articles/INjiui>`_


TODO
-----

- add TOC(use pelican-toc plugin)
- update conf
