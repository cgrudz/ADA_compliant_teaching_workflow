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

Due to various issues in making PDF documents accessible to screen readers, I want to make persistent HTML copies of my materials that can be hosted online for documentation on
my course web pages. This includes my lecture slides and lecture notes, which I want to host only online.  This also includes my homework, quizzes and handouts that,
when necessary, should print nearly identically to online hosted documents as hard copies to distribute in class.

There are two goals of this workflow:

  1. to efficiently generate presentation slides including both mathematical and code content in HTML as an alternative to PDF based formats;
  2. to efficiently generate HTML documents in standard letter size, including mathematical and code content which can be printed directly from a standard
     browser for a hard copy to hand out.

This workflow should satisfy the following requirements:
  
  1. documents must render as accessible, persistent HTML pages for hosting online; 
  2. the process must be relatively simple, relying on few commands or specialized knowledge of Bash or HTML.

My solution has been to largely adopt Markdown and R Markdown as my basis for typesetting.  Mathematical equations are rendered by
<a href="https://www.mathjax.org/" target="blank">MathJax</a> in HTML which is screen reader accessible. 
Writing all my teaching documents in a Markdown/ HTML native environment  has the benefit of not needing to make multiple conversions, 
and relying on a single style sheet for formatting.  Although it is possible with Pandoc to create PDF outputs and HTML outputs simultaneously from the same Markdown document,
this also requires editting and maintaining multiple stylesheets for the different output formats.

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
   <li> Con: Not all of the R Studio templates produce accessible HTML documents by default, and/ or satisfy the above goals. In response, 
        I have found several workarounds to force-overide some of these issues. I have filed formal bug reports with R Studio for issues I have noticed,
        but I am not contributing to the project directly, only providing temporary workarounds.
        Some issues aren't fully resolved and are discussed in the <a href="https://github.com/cgrudz/ADA_compliant_teaching_workflow#known-issues" target="blank">Known Issues Section</a>.</li> 
   <li> Con: Output PDFs through the Pandoc integration don't match the styling of the HTML documents by default, meaning you will have different formatting
        for printed and hosted documents.  For this reason, it is still recommended that you only output your Markdown documents to HTML anyway.</li>
  </ul> 
  <li>If you are familiar with command line, you can use my templates and "Makefile" for Pandoc with any editor you like. This has the following
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


##### Making HTML documents printable to standard notebook pages

###### In R Studio

Open any of the templates in the .rmd file type in the R_markdown directory.  Use the 
<a href="https://support.rstudio.com/hc/en-us/articles/200552056-Using-Sweave-and-knitr" target="blank">knit</a> option in the R Studio editor
to produce an HMTL document in the same directory.  The output HTML will be set in notebook size using the YAML frontmatter, which calls the
stylesheets in the "styles" directory.

You can also use any of the standard .rmd templates provided by R Studio, but it is recommended that you compile all documents to HTML as your
persistent, shareable format.  Note, there are <a href="https://github.com/rstudio/rstudio/issues/5447" target="blank">known bugs</a> in using
custom CSS with the R Markdown frontmatter, and if you wish to do so to re-size the page, it is recommended you follow one of my templates.

<b>Note:</b> by default, it seems that Knitr fails to include a language attribute in the output HTML document, which will need to be included manually.
This can be done with any editor, opening the HTML output and including,
```{html}
lang='en-us'
``` 
in the line at the top of the document,
```{html}
<html xmlns="http://www.w3.org/1999/xhtml">
```
so that the final document looks like,
```{html}
<html xmlns="http://www.w3.org/1999/xhtml" lang='en-us'>
```
in the hosted document.

###### In command line

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


#### Making HTML based presentations


##### Preface

I currently make all of my HTML based presentations in R Studio.  There are some alternatives for HTML based presentations, including writing these directly 
in <a href="https://github.com/hakimel/reveal.js" target="blank">Reaveal.js</a> which can be written in any editor, but the options I have seen tend to require
advanced knowledge of HTML to make these tools effective.

There are several presentation formats available in R Studio, including R Markdown documents which will convert to Ioslides or Slidy presentations.  However,
there are <a href="https://github.com/rstudio/rmarkdown/issues/1663">known issues</a> in these formats with accessibility which are pending bug-fixes. Until
bugfixes have been implemented, I have found it preferrable to write my slides in the RPres format which is only useable in R Studio.  This format also comes
with the cost that this format is not being actively developed, and has known issues with <a href="https://github.com/rstudio/rstudio/issues/5446">linking Mathjax to a remote
source</a> and with <a href="https://github.com/rstudio/rstudio/issues/5443" target="blank">accessibility standards in the default template</a>.  However,
I have been largely able to compensate for the issues in the Rpres format with my own templates.  There are still some bugs to be aware of, which are discussed
in <a href="https://github.com/cgrudz/ADA_compliant_teaching_workflow#known-issues" target="blank">the known issues section</a>. 

##### How to use templates

You can edit the default template using standard Markdown.  There are additional settings that I have included to deal with issues around accessibility.  You can preview 
the document in the R Studio viewer, and when you want to make a persistent copy, you can save this to HTML.  Note, when you create a copy of the presentation, it will
save a local copy of Mathjax for the presentation to be used when offline.  This is a handy feature, except for hosting documents online where multiple copies of Mathjax
will quickly eat up hosting space. If you need to host the document online, it is recommended to keep a local copy of Mathjax and link to this directly.  You can also
link to a remote copy, but the version included in R Presentations is not up to date with the current version and your slides may come out differently than intended.

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
into the HTML pages.  You can also use templates of the ".rmd" file type for R Markdown specifically, which can be compiled with R Studio.

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

This should be done within native Markdown or with HTML in the text.  See examples in guides on Markdown.

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

#### Non-local Mathjax in Rpres html docs
By default, when you export an HMTL document from a ```template.rpres``` document, it will include a folder called ```template_files```.  This includes an entire installation of Mathjax
in the local directory (V. 2.6.1) so you can host and load the presentation without internet connection.  However, for folks like myself who want to host their presentations on their website,
this comes with the unnecessary burden of hosting a local copy of Mathjax for every presentation, or otherwise keeping a local copy of Mathjax and editing the output HTML of every
document manually to link to the local copy.  Moreover, rpres yaml options do not respect setting a Mathjax link externally.
One option is to go through each  HTML output file and manually and resetting the Mathjax source, but this is a frustrating option for many folks.  The workaround I have found is to
include __before the yaml frontmatter__ the following lines,

```html
<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
```` 
The primary issue, however, is that developing locally in R Studio will still use an older version of Mathjax which will render differently than the current version.  When linked "live" online to
the current version of Mathjax, the output rendering of the slide can be quite different due to the differences in versions.

#### Splash screen has non-accessible color contrast levels
This is an issue where, by default, the splash screen uses contrast levels that are non-accessible to the visually impaired.  The issue can be relieved by resetting the reveal.js
css.  This can be done using, e.g., CSS linked with the header yaml of the document or manually in the frontmatter __before the yaml__.  Include the following,
```html
<style>
.section .reveal .state-background {
   background: #ffffff;
}
.section .reveal h1,
.section .reveal h2,
.section .reveal p {
   color: black;
   margin-top: 50px;
   text-align: center;
}
</style>
````
This changes the splash screen to normal white background and black text.  

Additionally, I belive it is important to include istructions on how to use the presentation for students
when they visit it later.  I include in my presentations the following lines __after the yaml__,
```html
<h2 style="text-align:left"> Instructions:</h2>
<p style='text-align:left'>Use the left and right arrow keys to navigate the presentation forward and backward respectively.  You can also use the arrows at the bottom right of the screen to navigate with a mouse.<br></p>
```
so that student are aware of how to navigate the presentation.

#### Non-descending heading levels in the output HTML
It is recommended that you do not use titles for slides using the following syntax
```
Title of slide  
========================================================
```
except for the very first slide.  This is because this defaults to an ```<h3>``` tag.  Indeed, you will by default create missing heading levels.  
You should structure your document and titles manually by using markdown heading levels for the titles in descending order without levels skipped.

#### Blank headings in the output HTML
When you check for accessibility with various checkers, you might find that there are blank heading tags such as 
```html
<h2> </h2>
```
or 
```html
<h3> </h3>
```
included inexplicably within your html presentation.  Remember, if there are blank characters above a slide separator such as
```
  
========================================================
```
this will be read as a title with an empty ```<h3>``` tag.  Avoid this, and check for blank characters above slide separators.
