---
title: Concepts 
layout: page 
pager: true
author: Jan Decaluwe
---

Introduction
============

Welcome to Urubu! My name is Jan Decaluwe and I am Urubu's author.

Urubu is a micro CMS for static websites.  The qualification "micro* means that
it has a small feature set, defined by what I need for my purposes.  To know
whether it is the right tool for you, check out [/start]. 

*[CMS]: Content Management System

Urubu's design philosophy is radical reuse of great software and ideas from
others. In the following sections, I will describe its concepts and how
they are implemented.

Authoring
=========

In Urubu, content is entered in [markdown] format. This is a lightweight format
that feels like a natural way to write content in plain text.

Markdown support in Urubu is implemented by the [python_markdown] package, that
converts the format to html. Urubu also supports the industry standard
[markdown_extra] extensions, with useful features such as tables and definition
lists.

Urubu supports nicely rendered code blocks, an essential feature for software
projects documentation. [fenced_code] are provided by the Markdown Extra
extensions.  This lets you enter language-specific code blocks without the need
for indentation. The [code_hilite] extension of Python-Markdown enables
language-specific syntax highlighting via the [pygments] library.

Configuration
=============

The configuration options in Urubu are kept minimal, in the spirit of "There
should be one obvious way to do it".  Where used, the configuration format is
YAML, implemented by the [pyyaml] library.

Configuration is mostly distributed, in the sense that every content file
should have a *front matter*, that specifies the title, layout, date and so on.
This idea is found in many tools, but Urubu reuses the technique from [jekyll].
YAML front matter is specified between two sets of triple dashes.

Urubu extends this configuration technique by treating index files specially.
Each folder in the site should have an index file (called `index.md`) that
specifies the ordered folder content. This can be done explicitly by listing
the files, or implicitly by specifying how the files should be ordered. 

Templating
==========

With templates you specify the html layout for a particular type of a page.
In a template you can mix plain html with control structures and variable
interpolation. The actual html page is generated by evaluating the template
with the appropriate evaluation context provided by Urubu.

Urubu uses the [jinja2] templating language library.


Theming
=======

A theme refers to the general look and feel of a web site. Partially this is
defined by the templates as discussed above. The other part is defined in style
sheets, with a technique known as Cascading Style Sheets (CSS). Basically
this is a sophisticated technique to define how the various html elements
should be rendered by the web browser.

With Urubu, you are free to design and use your own style sheets. However, it
has been developed with [bootstrap] in mind.  Bootstrap is a
professionally-designed framework with lots of useful predefined styles
components. Urubu generates html that is Bootstrap-friendly, and infers the
appropriate template variables for certain Bootstrap components. 

A great feature of Bootstrap is that it is "mobile first". This means that your
website will automatically adapt to any platform - smartphone, tablet or
widescreen.

A notable project is [bootswatch]. This is a set of themes designed as drop-in
replacement for the stock bootstrap styles. This gives you an effortless
option to change the look and feel of your website.

Navigation
==========

I am a big fan of Steve Krug's book [Don't make me think][dmmt],
and I feel that the lessons from this book are still often ignored.
Actually, the lack of focus of other tools on these ideas are the
main reason why I wrote Urubu.

[dmmt]: http://www.amazon.com/Dont-Make-Me-Think-Usability/dp/0321344758

A main concept is good navigation. Urubu supports various techniques
by inferring navigation-oriented variables and making them available to
the template engine. Moreover, they work well with some well-defined
and nicely style [bootstrap] navigation components. In this way,
you can easily implement the following:

* a navbar for navigation between major sections
* table of contents of a page in a sidebar
* breadcrumbs
* previous and next pager buttons
* active page or section highlighting 

Other techniques, independent from Urubu, can also help. Note for example that
the sidebar on this page is "affixed": it moves as you scroll through the page,
but never leaves the viewport. (Note: this description assumes that the
viewport is wide enough to accomodate the sidebar.) At any time, the full
structure of the page remains visible and available for navigation. This was
implemented by borrowing code from the [bootstrap] theme.

Project-wide reference links 
============================

A reference link is a way to refer to a link object via a reference id. Urubu
supports the concept of project-wide reference links.  Global reference links
are defined in the site configuration file.  Moreover, all content pages and
folders are available as reference links.

When you use a reference id in configuration info or in Markdown content
(between square brackets) Urubu will automatically resolve it. For Markdown,
this feature is implemented as a Markdown extension. Note that it doesn't
require any syntax change. It enables page linking similar to what is commonly
found on wiki's. 

Project-wide reference links are a distinguishing Urubu feature.

One of the messages of Steve Krug's book is that the text that you click should
be the title of the page where you land. Therefore, when you use reference
links, Urubu will insert the title of the link in the generated html (unless
you specify an alternative text explicitly).

Development and deployment
==========================

You can develop a Urubu project is like a software project, from a git or
mercurial repository.  This gives you best-in-class revision control.
Moreover, all the workflows that these systems provide are available. For
example, you can develop your website collaboratively on [github] or
[bitbucket].  Finally, it is easy to automate deployment, triggered by a push
of the generated site to an upstream repository. 