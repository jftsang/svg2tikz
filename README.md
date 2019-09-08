svg2tikz
========

Convert SVG figures generated by *inkscape* to TiKZ

Usage
-----

```
python3 svg2tikz.py

A program to generate TiKZ code from inkscape-generated SVGs
Future plans include generalising to SVG without depending on Inkscape

positional arguments:
  INFILE                Input file

optional arguments:
  -h, --help            show this help message and exit
  --version             show program's version number and exit
  -d, --debug           Enable debugging messages (repeat for more messages)
  -a, --auto            Create output name from source
  -o OUTPUT, --output OUTPUT
                        Write to file(default is stdout)
  -b BORDER, --border BORDER
                        Set standalone border (default:1mm)
  -r DPI, --dpi DPI     Resolution (assume 72dpi)
  -R, --round           Round numbers to the nearest integer (default is 1
                        decimal)
  -M, --multi           Make a multi-slide LaTEX file
  -s, --standalone      Make a standalone LaTEX file
  -X XFORM, --xform XFORM
                        transformation applied to the SVG code (default:
                        yscale=-1)
  --code CODE           Output file coding
```

This script converts SVG to TiKZ drawings. In standalone mode, the result can then be converted to PDF using pdflatex (see Makefile). Otherwise, the result is a TeX file that is included into LaTEX documents (using the ```\input{}``` command)

_MAIN SCOPE_: The main scope of this script is files generated with *Inkscape*. I will make my best to parse other SVGs

Multi slide HOWTO
-----------------

In order to create an animation from an Inkscape file

1. Create an inkscape figure. 
2. Group objects you want to appear on each slide incrementally 
3. Using the XML Editor in Inkscape, order the groups by order of appearance
4. Group all pages in one object. The structure should look like 

```<svg>
 +-<defs>
 +-<g>
    +-<g>
    +-<g>
     ...
```
    
4. Add ```--multi``` when calling svg2tikz
5. In your Beamer presentation, ```\input{generated_tikz}```

*Example*: ```make multi``` will convert `mount-ns.svg` and compile `test-multi.tex` to create a multi-slide presentation

**Limitations**: Multi-slide standalone TiKZ files are not supported.

TODO
----
*  arcs:
  * Better support for rotation

Dependencies:

* Python 3
* LXML to parse the SVG files
