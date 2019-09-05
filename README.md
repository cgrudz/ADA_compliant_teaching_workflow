# ADA Compliant Teaching Work Flow


## Background


This repository is to document and share my teaching workflow.  This workflow has been designed to meet as best as possible 
<a href="https://www.ada.gov/pcatoolkit/chap5toolkit.htm" target="blank">ADA web accessibility requirements</a>.  Implementing the rules surrounding
ADA accessibility for mathematics and statistics coursework is a complex task, and

<blockquote style="fontweight:bold"> 
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, 
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, 
DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH 
THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE. SEE THE <a href="LICENSE" target="blank">LICENCE</a> FOR FUTHER DETAILS.
</blockquote>

The main goal of this workflow is to produce Markdown/ HTML based documents in standard letter size, including mathematical equations rendered by
<a href="https://www.mathjax.org/" target="blank">MathJax</a>.  These documents should satisfy two requirements:
  1. these must render as accessible, persistent HTML pages for hosting online; and
  2. these must print well directly from PDF exports of the HTML pages with standard web browsers.
Due to various issues in making PDF documents accessible to screen readers, the persistent copies are meant to be hosted online for documentation on
my course web pages.  However, when necessary, I want to be able to print nearly identical copies to hand out in my classes.  These templates are an
attempt at meeting the two above goals.

### Attribution

This project is a fork of the <a href="https://github.com/mszep/pandoc_resume" target="blank">Pandoc Resume</a> project, to which I owe inspiration for
the work flow, many aspects of the CSS and the Pandoc makefile.  Please see the <a href="LICENSE" target="blank">LICENCE</a>. 

## Instructions
```bash
git clone https://github.com/cgrudz/ADA_compliant_teaching_workflow
cd ADA_compliant_teaching_workflow 
vim markdown/"some_template.md"   # choose a template to work with and fill values
make  # this will run pandoc with Mathjax settings, outputting to HTML
```
The make file will produce HTML documents (with MathJax equations from LaTeX) from all files found in the "markdown" directory.  The output HTML documents will be
saved to the "output" directory.

The preset values can be edited in the Makefile as

```bash
UT_DIR=output
IN_DIR=markdown
STYLES_DIR=styles
STYLE=base
```
where the output and input directories can be edited in the UT_DIR and IN_DIR above.  STYLES_DIR is the directory which contains all CSS for rendering 
the documents with note page formatting.  STYLE variable will be the chosen css in the STYLES_DIR.

### Requirements

* <a href="https://pandoc.org/installing.html" targeti="blank">pandoc 2.x</a>
    * 1.x is deprecated




Last tested on the above versions and that's not to say the later versions won't work. Please try to use the latest versions when possible.

Check if the dependencies are up to date.

```
pandoc --version
```

#### Cannot process lua
Currently pandoc 1.x may be within your distro's repos and the latest version should be used. See the
[pandoc releases](https://github.com/jgm/pandoc/releases) for your distro.

e.g. for Debian / Ubuntu
```
wget https://github.com/jgm/pandoc/releases/download/2.2.1/pandoc-2.2.1-1-amd64.deb
sudo dpkg -i pandoc-2.2.1-1-amd64.deb
```
