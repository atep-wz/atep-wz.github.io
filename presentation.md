
class: center, middle

# Extending Markdown with Citations

Wenhan Zhu (Cosmos)

---
layout: false
.left-column[
  ## Markdown
  ### - What is it?
]
.right-column[
  [Markdown](https://daringfireball.net/projects/markdown/) is a lightweight markup language with plain text formatting syntax first written in [Perl](https://www.perl.org/) by *John Gruber*.

  Markdown by design:

  - Plain text formatting syntax

  - Easy to read, easy to write

  - Converts to structurally valid XHTML (or HTML)


  Great properties due to design:

  - Easy to share

  - Easy to do styling with regular CSS

  - Easy to collaborate with others

  - Easy to manage versions with SCM (Software configuration management) tool

]

---
.left-column[
 ## Markdown
 ### - What is it?
 ### - Example
]
.right-column[
```markdown
## Hello World

Example List
- One
- *Two*
- ~~Three~~
- **Four**
```

```HTML
<h2>Hello World</h2>
<p>Example List</p>
<ul>
<li>One</li>
<li><em>Two</em></li>
<li><s>Three</s></li>
<li><strong>Four</strong></li>
</ul>
```

<h2>Hello World</h2>
<p>Example List</p>
<ul>
<li>One</li>
<li><em>Two</em></li>
<li><s>Three</s></li>
<li><strong>Four</strong></li>
</ul>
]

---
### Project Idea
Extend Markdown syntax to support *bibtex* style citations.

#### Motivation
Short document (< 5 pages):

- Easy to Read/Edit/Share

- Portable

- Math equations

- References

- Printable

---

.left-column[
  ## Markdown
  ### - What is it?
  ### - Example
  ### - Why Markdown
]
.right-column[

  #### Easy to Read/Edit/Share
  Method | Read | Edit | Share
  ------ | ---- | ---- | -----
  PDF    | Yes | No | Yes
  Word* | Yes | Yes | Yes
  Word | Yes | No | No
  Latex | No | No | No
  HTML | Yes | No | No
  Markdown | Yes | Yes | Yes

.footnote[.red.bold[Word*] Assumes a copy of the editing software]
]

???
Assumes for a normal person, the capability of their computer.

Sharing:
- How to share the source files.

### PDF (Adobe Acrobat)
- R: Browser and other Software
- E: Can added comment, hard to modify

### Word*
- R/E When both have a exact same copy of the editing Software

### Word
- R/E Editing software not present

### Latex
- R: Meaningless content for markups
- E: For most cases require proper Software
- S: Often not a single file to Share

### HTML
- R: Assume present of a browser
- E: Assume basic processing tools
- S: Fully featured site is not easy to Share

---

.left-column[
  ## Markdown
  ### - What is it?
  ### - Example
  ### - Why Markdown
]
.right-column[
  #### Portability
  How easy it is to set up the development environment when I have a barebones computer system.

  PDF | Word | Latex | HTML | markdown
  -|-|-|-|-
  Hard | Medium | Hard | Hard | Easy

]

---

.left-column[
  ## Markdown
  ### - What is it?
  ### - Example
  ### - Why Markdown
]
.right-column[
  #### Math equations, References, Printable
  #### Easy to Read/Edit/Share

  Method | Math | Reference | Printable
  - | - | - | -
  PDF    | Yes | Manual | Yes
  Word | Yes | Yes | Yes
  Latex | Yes | Yes | Yes
  HTML | Yes | Manual | Yes*
  Markdown | No | Manual | No

  .footnote[.red[* ] Printing in HTML is done through browser, will cover in more details in later slides]

]

---
.left-column[
  ## Markdown
  ### - What is it?
  ### - Example
  ### - Why Markdown
  ### - Extensibility
]
.right-column[
  #### Extensibility
  Part of the initial description of Markdown is ambiguous, and have unanswered questions. Due to the simplicity of plain text file, many implementations and extensions of Markdown appeared over the years.

  ##### Dialects
  Different flavors of Markdown are some time referred to as dialects.

  - [CommonMark](http://commonmark.org/)

  - [GFM](https://github.github.com/gfm/) (GitHub Flavored Markdown)

  - [MultiMark](http://fletcherpenney.net/multimarkdown/)

  - [RMarkDown](https://rmarkdown.rstudio.com/)

]

---
.left-column[
  ## Markdown Extensions
  ### - CommonMark
]
.right-column[
  #### What is CommonMark
   > A standard, unambiguous syntax specification for Markdown, along with a suite of comprehensive tests to validate Markdown implementations against this specification

   From CommonMark's official website.

   Noticeable extensions:

   - Fenced code blocks

   - Start number of an ordered list is significant
]

---
.left-column[
  ## Markdown Extensions
  ### - CommonMark
  ### - GFM
]
.right-column[
  #### GitHub Flavored Markdown

   Noticeable extensions:

   - Tables

   - Task list

   - Strikethrough (~~Example~~)

]

---
.left-column[
  ## Markdown Extensions
  ### - CommonMark
  ### - GFM
  ### - MultiMarkDown and RMarkDown
]

.right-column[
  #### More than a extension of the markup syntax
  Require extra program for some functionality (MMD) or itself is a entire program (RMD).

  <img src="https://d33wubrfki0l68.cloudfront.net/b8ea889386094107f8a5cd511ff05b0ce8336a51/3a9c7/images/bandtwo2.png" width="600">
]

---
class: middle
### Project Approach
Extensions needed:

- Math Display

- Citation

<div class="mermaid">
graph LR
        .css --> output.html
        input.md --> parser
        parser --> raw.html
        raw.html --> output.html

        extra.html --> output.html

</div>

---
.left-column[
  ## Math Display
  ### - Methods
]
.right-column[
  Ways of displaying

  - As an image

  - Use JavaScript-based libraries (MathJax, Katex)

  - Natively through MathML

  <center><img src="http://latex2png.com/output//latex_0e6b6358434f5bbaf45759468871db9f.png" width=120></center>

  $$   \sum_{i = 1}^{\infty} \frac{1}{n^2} = \frac{\pi}{6} $$

  ```latex
  \sum_{i = 1}^{\infty} \frac{1}{n^2} = \frac{\pi}{6}
  ```


]

---
.left-column[
  ## Math Display
  ### - Methods
]
.right-column[

```MathML
<math xmlns="http://www.w3.org/1998/Math/MathML" display="block">
  <munderover>
    <mo>&#x2211;<!-- ∑ --></mo>
    <mrow class="MJX-TeXAtom-ORD">
      <mi>i</mi>
      <mo>=</mo>
      <mn>1</mn>
    </mrow>
    <mrow class="MJX-TeXAtom-ORD">
      <mo movablelimits="true" form="prefix">inf</mo>
    </mrow>
  </munderover>
  <mfrac>
    <mn>1</mn>
    <msup>
      <mi>n</mi>
      <mn>2</mn>
    </msup>
  </mfrac>
  <mo>=</mo>
  <mfrac>
    <mi>&#x03C0;<!-- π --></mi>
    <mn>6</mn>
  </mfrac>
</math>
```
]
---
.left-column[
  ## Math Display
  ### - Methods
  ### - Result
]
.right-column[
  With all the methods explored, clearly using Javascript based libraries would be a better case.

  **How do we extend this feature to our markdown syntax?**

]
---
.left-column[
  ## Math Display
  ### - Methods
  ### - Result
]
.right-column[
  With all the methods explored, clearly using Javascript based libraries would be a better case.

  How do we extend this feature to our markdown syntax?

  **We don't.**

]

---
.left-column[
  ## Math Display
  ### - Methods
  ### - Result
  ### - Framework
]
.right-column[
  When we have an equation to render in markdown.

  ```markdown
  $$\sum_{i = 1}^{\inf} \frac{1}{n^2} = \frac{\pi}{6}$$
  ```

  In `raw.html`:
  ```html
  <p> $$\sum_{i = 1}^{\inf} \frac{1}{n^2} = \frac{\pi}{6}$$ </p>
  ```
  Which will render as

  <div class="tex2jax_ignore"> $$\sum_{i = 1}^{\inf} \frac{1}{n^2} = \frac{\pi}{6}$$ </div>

  With `extra.html` added to `raw.html` to form `output.html` we added the configuration of the javascript library and it will take care of the conversion from latex to math.
  $$ \sum_{i = 1}^{\infty} \frac{1}{n^2} = \frac{\pi}{6} $$

]

---

.left-column[
  ## Citation
  ### - What is it?
]
.right-column[
  > a citation is an abbreviated alphanumeric expression embedded in the body of an intellectual work that denotes an entry in the bibliographic references section of the work for the purpose of acknowledging the relevance of the works of others to the topic of discussion at the spot where the citation appears.

  From Wiki.

]

---
.left-column[
  ## Citation
  ### - What is it?
  ### - Bibtex
]
.right-column[
  ### [Bibtex](http://www.bibtex.org)
  Bibtex is probably the most used tool to describe and process lists of references. [Citation needed]

  The plain text file format `.bib` is widely adopted by many third party application to do reference management.

  Unlike Math rendering, we need to extend the Markdown Syntax for this.
]

---
.left-column[
  ## Citation
  ### - What is it?
  ### - Bibtex
  ### - Markdown Syntax
]
.right-column[

  ### Similar Syntax Extensions

  - Footnote `[^fn1]`


  ### Previous approaches for citations

  - MultiMarkDown
    `[#smith:2003]`

  - RMarkDown
    `[@smith03]`
]

---
.left-column[
  ## Citation
  ### - Bibtex
  ### - Markdown Syntax
  ### - Example

]
.right-column[
  ### Example Bibtex entry
  ```text
  @article{einstein,
      author =       "Albert Einstein",
      title =        "{Zur Elektrodynamik bewegter K{\"o}rper}. ({German})
          [{On} the electrodynamics of moving bodies]",
      journal =      "Annalen der Physik",
      volume =       "322",
      number =       "10",
      pages =        "891--921",
      year =         "1905",
      DOI =          "http://dx.doi.org/10.1002/andp.19053221004"
  }
  ```

<ul>
<li>
  <span class="">
    <a class="bibtexVar" extra="BIBTEXKEY">
        <span style="text-decoration: underline;" class="title">Zur Elektrodynamik bewegter Körper. (German)
      [On the electrodynamics of moving bodies]</span>,
    </a>
  </span>

  <div class="">
    <span class="author">Albert Einstein</span>
  </div>
  <div>
    <span class=""><em><span class="journal">Annalen der Physik</span></em>,</span>
    <span class=""><span class="volume">322</span>,</span>
    <span class="">(<span class="number">10</span>),</span>
    <span class=""> pages <span class="pages">891-921</span>,</span>

    <span class=""><span class="year">1905</span>.</span>

    <a class="bibtexVar" role="button" data-toggle="collapse" href="#bibeinstein" aria-expanded="false" aria-controls="bibeinstein" extra="BIBTEXKEY">
</a>
  </div>
  <div style="display:none"><span class="bibtextype">journal</span></div>
  <div style="display:none"></div>
</li>
</ul>

]

---
.left-column[
  ## Citation
  ### - What is it?
  ### - Bibtex
  ### - Markdown Syntax
  ### - Example
]
.right-column[
### Markdow file
```markdown
## Title
This is an example citation[@einstein].

Another random paragraph.
```

### Output html
```html
<h2> Title </h1>

<p> This is an example citation<span class="citation" id="cite-einstein"> [einstein] </span> </p>.

<p> Another random paragraph </p>

<h3> Reference </h3>
<!-- Code for rendering the citation base on bibtex entry -->
```
]

---
.left-column[
  ## Citation
  ### - What is it?
  ### - Bibtex
  ### - Markdown Syntax
  ### - Example
]
.right-column[
<h2> Title </h1>

<p> This is an example citation<span class="citation" id="cite-einstein"> [einstein] </span> .</p>

<p> Another random paragraph </p>

<h3> Reference </h3>

### Reference
<ul>
<li>
  <span class="">
    <a class="bibtexVar" extra="BIBTEXKEY">
        <span style="text-decoration: underline;" class="title">Zur Elektrodynamik bewegter Körper. (German)
      [On the electrodynamics of moving bodies]</span>,
    </a>
  </span>

  <div class="">
    <span class="author">Albert Einstein</span>
  </div>
  <div>
    <span class=""><em><span class="journal">Annalen der Physik</span></em>,</span>
    <span class=""><span class="volume">322</span>,</span>
    <span class="">(<span class="number">10</span>),</span>
    <span class=""> pages <span class="pages">891-921</span>,</span>

    <span class=""><span class="year">1905</span>.</span>

    <a class="bibtexVar" role="button" data-toggle="collapse" href="#bibeinstein" aria-expanded="false"     aria-controls="bibeinstein" extra="BIBTEXKEY">
    </a>
  </div>
  <div style="display:none"><span class="bibtextype">journal</span></div>
  <div style="display:none"></div>
</li>
</ul>

]


---
.left-column[
  ## Citation
  ### - What is it?
  ### - Bibtex
  ### - Markdown Syntax
  ### - Example
  ### - Implementation
]
.right-column[
  ### Parser

  - Capable of Client side only functionality

  - Javascript based

  - Extensible



  ### Options

  - [Showdown](https://github.com/showdownjs/showdown)

  - [Markdown-it](https://github.com/markdown-it/markdown-it)

  - ...
]

---
.left-column[
  ## Citation
  ### - What is it?
  ### - Bibtex
  ### - Markdown Syntax
  ### - Example
  ### - Implementation
]
.right-column[
  ### Tasks for the parser extension

  - Replace the citation syntax as proper html class and tags.

  - Insert at the correct location of the raw html file for JavaScript libraries on Bibtex processing to work


  ### Tasks for `extra.html`

  - Correctly render the required reference list based on the information from parser extension.


  Fortunately someone have already written a javascript library [bibtex-js](https://github.com/pcooksey/bibtex-js)) to parse a `.bib` file format and render reference list nicely. The task left for `extra.html` will be integration.
]

---
class: middle, center

# [Demo](markdown-citation/index.html) of current work

---
class: middle, center
# Thank you!

.footnote[Slides created using [remark](https://github.com/gnab/remark)]
