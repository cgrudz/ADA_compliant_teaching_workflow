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

I can recommend two ways to approach this:

<ol>
  <li>If you prefer to work within a graphical environment, use <a href="https://www.rstudio.com/" target="blank">R Studio</a> 
  and approach this within an <a href="https://bookdown.org/yihui/rmarkdown/">RMarkdown framework</a>.  This has the following pros and cons:</li>
  <ul>
   <li> Pro: R Studio has integration with Pandoc, which means that you can output your markdown files into any format you want.</li>
   <li> Pro: R Studio is also highly user-friendly, and includes document previews and automatic compiling of documents through the graphical interface.</li>
   <li> Pro: There are pre-made templates within the R Studio environment for different types of documents.</li> 
   <li> Pro: R Studio has installers for all operating systems and should be compatible with most configurations without any extra work.</li>
   <li> Con: R Studio yaml frontmatter doesn't seem to fully respect custom CSS stylesheets.  In response, I have found several "hacky" workarounds to force-overide some of these
        settings which are inclued in my R Markdown templates, but this can be inelegant.  Some issues aren't fully resolved and are discussed in the <a href="https://github.com/cgrudz/ADA_compliant_teaching_workflow#known-issues" target="blank">Known Issues Section</a>.</li> 
   <li> Con: Output PDFs through the Pandoc integration don't match the styling of the HTML documents by default, meaning you will have different formatting
        for printed and hosted documents.  For this reason, it is still recommended that you only output your markdown documents to HTML anyway.</li>
  </ul> 
  <li>If you are even slightly familiar with command line, you can use my templates and "Makefile" for Pandoc with any editor you like. This has the following
      pros and cons:</li>
  <ul>
   <li> Pro: you can use any editor you like and any custom stylesheets for formatting.</li>
   <li> Con: I haven't figured out yet how to integrate R Markdown features such as Knitr code wrapping into documents from command line.  This will be investigated further as
        time is available.  If you have a solution, fork this repository and contact me.</li>
   <li> Con: for Windows users, you will need to use a <a href="https://docs.microsoft.com/en-us/windows/wsl/install-win10" target="blank">Linux subsystem on Windows</a> in order to
        use the Makefile in the Bash shell.</li>
  </ul>
  
</ol>

### Installation 

#### Requirements

* <a href="https://pandoc.org/installing.html" targeti="blank">pandoc 2.x</a>
    * 1.x is deprecated

* <b>Optional:</b> <a href="https://www.rstudio.com/" target="blank">R Studio</a>

#### How to download the repository

```bash
git clone https://github.com/cgrudz/ADA_compliant_teaching_workflow
```

Or via the Github GUI.

#### How to get started

##### In R Studio

Open any of the templates in the .rmd file type in the R_markdown directory.  Use the 
<a href="https://support.rstudio.com/hc/en-us/articles/200552056-Using-Sweave-and-knitr" target="blank">knit</a> option in the R Studio editor
to produce an HMTL document in the same directory.  You can print from this HTML page by setting the margins within the browswer printing options; 
unfortunately it seems that the frontmatter doesn't respect the page formatting in the "base.css" in the provided stylesheets, but it will respect
some of the options.

You can also use any of the standard .rmd templates provided by R Studio, but it is recommended that you compile all documents to HTML as your
persistent, shareable format.

##### In command line

1. Enter the repository directory:
```bash
cd ADA_compliant_teaching_workflow 
```

2. Edit "some_template" with your favorite editor:

```bash
vim markdown/"some_template.md"   
```

3. Run pandoc with Mathjax settings enabled, outputting to HTML files
```bash
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

* <a href="https://pandoc.org/installing.html" target="blank">pandoc 2.x</a>
    * 1.x is deprecated

Last tested on the above versions and that's not to say the later versions won't work. Please try to use the latest versions when possible.
Check if the dependencies are up to date.

e.g.,
```
pandoc --version
```
#### Installation

e.g. for Debian / Ubuntu
```
wget https://github.com/jgm/pandoc/releases/download/2.2.1/pandoc-2.2.1-1-amd64.deb
sudo dpkg -i pandoc-2.2.1-1-amd64.deb
```
* For the R Studio option, follow all the installation requirements provided by R Studio.

### FAQ

#### Q: How do I create my own materials with this workflow?

Write new documents or edit existing templates in the ".md" file type within the IN_DIR.  Use the make command as above to export these
into the HTML pages.

#### Q: What is ".md" file type?

This is <a href="https://www.markdownguide.org/getting-started" target="blank">Markdown</a>, a popular Markup typsetting language. You
can think of this similarly to LaTeX, but based around web page commands and simplified HTML.


#### Q: How do I write math equations in the documents?

This is done as with standard LaTeX, with minor differences.  To enter math-mode in line, use the usual ``$`` sign. To write equations
in a new line, use ``$$`` a double sign enclosure.  This will accept standard LaTeX environments such as

 * ``\begin{align}``
 * ``\begin{equation}``

but these must be enclosed within the double ``$$``.

#### Q: What about including figures?

This should be done within native Markdown or with HTML in the text.  

#### Q: How do I get a PDF output to print in class?

You can do this with a standard browser, such as Firefox or Chrome.  Use the print page option within the browser when you have loaded
the HTML page within the browser.  Remember, don't include any margins in the printing settings as these are set within the HTML
by default to notebook pages with 1 inch margins.

#### Q: Why does printing cut off in weird places and how do I fix this?

The document doesn't automatically recognize where we want page breaks when we print to PDF or out to a hard copy.  Unfortunately,
the best option I'm aware of is to manually set these as follows:

```html
<div class="pagebreak"> </div>
```
 
Place a "pagebreak" div at the point you want the page to cut off.  This will automatically cut the page for printing or conversion
to PDF immediately before this element. __Note__ this will automatically enforce a 1 inch margin at the top of the new page,
but __you must manually set where you want a break at the bottom of the page__.  For my handouts, quizzes, etc, I feel OK just
approximating it.

#### Q: How do I make space in between elements to give, e.g., problems with room to hand fill answers in the printed sheet?

Include an "answers_div" as follows

```html
<div class="answer_div"></div>
```

Generally, you can set many different sizes of blank space either manually or with CSS.  The "answers_div" class is in the base.css
under the styles directory which is set to give 2 inches of blank space.  
You can edit this yourself if you need different spacing, or create different classes of divs for the same purpose.

#### Q: How do I highlight portions of text in solution keys, e.g., to show the solution after the problem?

This can be done with the "solutions" class of div,

```html
<div class="solutions">
"Some text"
</div>
```
Within this element, "Some text" will be colored blue, as will anything else which lies in this container.  The color can be changed within the base.css,
and other similar classes can be created like this.


#### Q:  How do I get help?

You can contact me directly at cgrudzien AT unr DOT edu and I will try to assist or point you to a relevant resource.

### Known Issues

#### R Markdown issues


##### Notebook size documents in R Markdown
R Markdown yaml frontmatter will import custom stylesheets, however, it will not respect page size settings.  For this reason, I have incuded additional frontmatter with 
```yaml
includes:
      in_header: ../styles/notebook.html
```
in my R Markdown templates.  This has the effect of enforcing notebook size margins within these documents, by including CSS for the body element which is usually neglected by the yaml.



#### R Presentation Issues

There are several different presentation mediums within R Markdown, including ioslides, slidy presentations, and .rpres documents which integrate reveal.j.
My experience so far is with usings .rpres documents because I like the features of reveal.js, however, there are various issues especially as it seems like
the yaml for rpres is more limited by default than with other R Markdown documents.  I will outline the issues encountered so far and what solutions, if any,
I have been able to find.

#### Non-local Mathjax in Rpres html docs
By default, when you export an HMTL document from a ```template.rpres``` document, it will include a folder called ```template_files```.  This includes an entire installation of Mathjax
in the local directory (V. 2.6.1) so you can host and load the presentation without internet connection.  However, for folks like myself who want to host their presentations on their website,
this comes with the unnecessary burdent of hosting a local copy of Mathjax for every presentation.  Moreover, rpres yaml options do not respect setting a Mathjax link externally.
One option is to go through each HTML output file and manually and resetting the Mathjax source, but this is a frustrating option for many folks.  The workaround I have found is to
include __before the yaml frontmatter__ the following lines,

```html
<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
````
