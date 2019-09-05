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

Thanks to <a href="https://www.unr.edu/tlt" target="blank">Don Massie</a> and <a href="https://wolfweb.unr.edu/~asarantsev/" target="blank">Andrey Sarantsev</a>
for investigating the <a href="https://wolfweb.unr.edu/~asarantsev/accessdetail.html" target="blank">primary issues and various solutions</a> for accessible math documents.

To summarize one of the main conclusions:
<blockquote>
We described a way to make LaTeX accessible for visually impaired students via conversion through Pandoc to HTML-MathJax. 
We discussed in detail that Pandoc does not convert everything automatically, and we need to do some work manually. 
This is especially true for research articles, not so much for lecture notes and assignments. 
In other words, it is easier to deal with materials for undergraduate teaching than it is with research papers.
</blockquote>

Due to various issues in making PDF documents accessible to screen readers, I want to make persistent copies of my materials that can be hosted online for documentation on
my course web pages.  However, when necessary, I want to be able to print nearly identical copies to hand out in my classes.

The main goal of this workflow is to produce Markdown/ HTML native documents in standard letter size, including mathematical equations rendered by
<a href="https://www.mathjax.org/" target="blank">MathJax</a>. This has the benefit of not needing to make multiple conversions, and relying on a
single style sheet for formatting. These documents should satisfy the following requirements:
  1. these must render as accessible, persistent HTML pages for hosting online; 
  2. these must print well directly from PDF exports of the HTML pages with standard web browsers;
  3. the process must be relatively simple, relying on few commands or specialized knowledge of Bash or HTML.

### Attribution

This project is a fork of the <a href="https://github.com/mszep/pandoc_resume" target="blank">Pandoc Resume</a> project, to which I owe inspiration for
the work flow, many aspects of the CSS and the Pandoc makefile.  Please see the <a href="LICENSE" target="blank">LICENCE</a>. 

## Instructions


### Installation

#### Requirements

* <a href="https://pandoc.org/installing.html" targeti="blank">pandoc 2.x</a>
    * 1.x is deprecated


#### How to download

```bash
git clone https://github.com/cgrudz/ADA_compliant_teaching_workflow
```

Or via the Github GUI.

#### How to use

```bash
cd ADA_compliant_teaching_workflow 
vim markdown/"some_template.md"   # choose a template to work with and fill values
make  # this will run pandoc with Mathjax settings, outputting to HTML
```
The make file will produce HTML documents (with MathJax equations from LaTeX) from all files found in the "markdown" directory.  The output HTML documents will be
saved to the "output" directory.  This should work on standard Linux and Unix distributions. Windows users can use the command 
line with <a href="https://docs.microsoft.com/en-us/windows/wsl/install-win10">Bash on Windows</a>

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

e.g.,
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

### How to use

Write new documents or edit existing templates in the ".md" file type wihtin the IN_DIR.

 * __Q:__ What is ".md" file type?

This is <a href="https://www.markdownguide.org/getting-started" target="blank">Markdown</a>, a popular Markup typsetting language. You
can think of this similarly to LaTeX, but based around web page commands and simplified HTML.

 * __Q:__ How do I write math equations in the documents?

This is done as with standard LaTeX, with minor differences.  To enter math-mode in line, use the usual ``$`` sign. To write equations
in a new line, use ``$$`` a double sign enclosure.  This will accept standard LaTeX environments such as

 * ``\begin{align}``
 * ``\begin{equation}``

but these must be enclosed within the double ``$$``.

 * __Q:__ What about including figures?

This should be done within native Markdown or with HTML in the text.  

 * __Q:__ How do I get a PDF output to print in class?

You can do this with a standard browser, such as Firefox or Chrome.  Use the print page option within the browser when you have loaded
the HTML page within the browser.  Remember, don't include any margins in the printing settings as these are set within the HTML
by default to notebook pages with 1 inch margins.

 * __Q:__ Why does printing cut off in weird places and how do I fix this?

The document doesn't automatically recognize where we want page breaks when we print to PDF or out to a hard copy.  Unfortunately,
the best option I'm aware of is to manually set these as follows:

```html
<div class="pagebreak"> </div>
```
 
Place a "pagebreak" div at the point you want the page to cut off.  This will automatically cut the page for printing or conversion
to PDF immediately before this element. __Note__ this will automatically enforce a 1 inch margin at the top of the new page,
but __you must manually set where you want a break at the bottom of the page__.  For my handouts, quizzes, etc, I feel OK just
approximating it.

 * __Q:__ How do I make space in between elements, such as blocks of text and math, to give problems with room to hand fill
answers in the printed sheet?

Include an "answers_div" as follows

```html
<div class="answer_div"></div>
```

Generally, you can set many different sizes of blank space either manually or with CSS.  The "answers_div" class is in the base.css
under the styles directory which is set to give 2 inches of blank space.  
You can edit this yourself if you need different spacing, or create different classes of divs for the same purpose.


