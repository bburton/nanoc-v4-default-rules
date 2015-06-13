## Overview

Better default Rules for nanoc static site compiler (http://nanoc.ws version 3.x)
that for the simple cases require little to no configuration. 

Files that are considered to be pages (based on a list of extensions), are 
appropriately filtered and routed for some common file types such as Haml, 
Markdown and Textile. All other text files and binary files are copied 
verbatim from input to output. 

## Compass and Sass support

Compass/SASS support is preconfigured and just needs to be uncommented if 
it's going to be used. A compass config.rb with extensive documentation is 
also included. By default, compass will generate css in development mode 
which is verbose with line numbers. As nanoc does not currently provide a 
way to specify the environment such as development or production when 
compiling a site. 

So to output css in production mode which is much more terse, run the 
following command after a nanoc compile: 

`compass compile -e production --force`

## Usage

To use these files, replace existing Rules, nanoc.yaml and optionally 
config.rb with these files. Most common custom compile and route rules for 
stylesheets and many other files like robots.txt are simply unnecessary 
with the included Rules file.

