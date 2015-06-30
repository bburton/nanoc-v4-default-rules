# Better default nanoc v4 Rules

## Overview

Better default Rules for nanoc static site compiler version 4 that for 
the simple cases, require little to no configuration. 

This implementation is based on the observaton that there are really two
types of text files in nanoc---page files and non-page files. Page files
are any type of text file that are compiled into HTML resulting in a page
viewable in a browser. Non-page file are any other files such as CSS,
JavaScript or other types of files not compiled into an HTML page.

With this understanding, it's then possible to generalize a lot of logic 
in the Rules file and made it trivial to support both clean URI's and 
extension URI's with a simple configuration change.

Files that are considered to be pages (based on a list of extensions
defined in nanoc.yaml), are appropriately filtered, have a layout applied 
and routed for some common file types such as HTML, Haml, Markdown and 
Textile. All other text files and binary files are copied verbatim from 
input to output preserving their extension unless their extension is mapped 
to a different one, e.g. .sass => .css, .scss => .css and .coffee => .js.

This implementation is being made available to help adopting nanoc v4 
and as a prototype for some enhancements that could be made to nanoc. 
There's not doubt ways to simplify and improve this implementation so I 
look forward to any feedback.

## Objectives

* No changes to nanoc itself are required. However, if certain changes 
  could be made, it would simplify the Rules file.

* Handle both "clean URI's" as supported by nanoc v3 as well as extension
  URI's with a simple configuration change in nanoc.yaml.

* Use new nanoc v4 default settings for glob matches and full identifiers.

* Avoid custom paths such as for a stylesheets or javascript folder as
  this is just one more thing to configure and people tend to have 
  preferences on what the folder names should be.

* Rules file is written to be a template of sorts rather than trying to
  support all possible filters supported by nanoc.  The Ruby code is 
  written to be simple so those that don't know Ruby well will have less 
  of an issue understanding and changing it.

## Compass and Sass support

Compass/Sass support is preconfigured and just needs to be uncommented if 
it's going to be used. A Compass config.rb with extensive documentation is 
also included. By default, Compass will generate css in development mode 
which is verbose with line numbers as nanoc does not currently provide a 
way to specify the environment such as development or production when 
compiling a site. 

To output css in production mode which is much more terse and compact, 
either edit config.rb or run the following command after a nanoc compile: 

`compass compile -e production -s compact --force`

When developing a site and you want to debug the Sass from a browser,
compile enabling Source Map support after a nanoc compile:

`compass compile -e development -s nested --force --sourcemap`

## Usage

1. Replace existing Rules, nanoc.yaml and optionally config.rb if using
   Compass/Sass. 

2. Review settings in nanoc.yaml, especially: clean_uri_routing,
   page_extensions and extensions_map.

3. Review blogging route in the Rules file and customize prefix and output 
   format if blogging will be implemented. 

4. If using Compass/Sass, edit config.rb and adjust paths and settings as
   necessary. Also edit the Rules file and uncomment the call to initialize
   Compass.

## Change Log

0.1 (29-Jun-2015)

* Initial version based on an older version written for nanoc v3.

