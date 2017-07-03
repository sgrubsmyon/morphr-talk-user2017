---
title: "Morphological Analysis with R"
subtitle: "useR!2017 Brussels"
author: "Markus Voge"
date: "2017-07-07"
job: "EA European Academy of Technology and Innovation Assessment"
# framework: io2012        # {io2012, html5slides, shower, dzslides, ...}
# theme: default
# highlighter: highlight.js  # {highlight.js, prettify, highlight}
# hitheme: tomorrow      # 
# widgets: [bootstrap, mathjax, shiny] # {mathjax, quiz, bootstrap}
# mode: selfcontained # {selfcontained, standalone, draft}
# knit        : slidify::knit2slides
# output: ioslides_presentation
output:
  ioslides_presentation:
    widescreen: true
    # css: styles.css
#     logo: uni-bonn-logo.png
#     mathjax: local
#     self_contained: no
#     widescreen: yes
runtime: shiny
---

## Morphological Analysis (MA)

### What is MA?

> * A qualitative modelling method for systematically structuring complex problems
> * Useful tool for scenario development
> * "Simply an ordered way of looking at things" (Fritz Zwicky, 1948,
    *Morphological astronomy*)
> * Very flexible and general, also called *General Morphological Analysis*
> * Typically used in workshops with a team of subject matter experts

<!--
> * Holistic approach: "A method for structuring and investigating **the total set of
    relationships** contained in multi-dimensional, non-quantifiable, problem
    complexes" (Tom Ritchey, 2011, *Wicked Problems &mdash; Social Messes*)

> * Use cases:
>   * From classifying astronomical objects via developing jet engines to
      investigating legal aspects of space colonization
-->

### What MA is not

> * Very specialized theory/method, e.g. in biology, geology, linguistics, ...
> * Mathematical morphology as used in image processing (CRAN packages `Morpho`
    and `mmand`)


## Why use MA?

* To tackle "wicked problems" (Ritchey, 2011)
* For "garbage detection"
  * Remove irrelevant variables
  * Remove inconsistent relations
* For interactive visualization of a (qualitative) model

<!--
  * Complex and messy (multi-dimensional)
  * Difficult to define (ambiguous)
  * Changing all the time
  * Everything depends on everything else
  * "*Society*", "*people*"
  * Non-quantifiable $\rightarrow$ mathematical modelling/simulation useless
-->


## Some credits

<div class="pull-right" style="width: 300px; margin-left: 25px;">
  <img style="height: 480px;" src="Zwicky.png" alt="Fritz Zwicky">
  <span style="font-size: 12pt;">
  Fritz Zwicky (Source: <a href="https://www.flickr.com/photos/kevandotorg/2426466260/in/photolist-pM1yzJ-4GqgTb-5KRWpv">Kevan: Spherical Bastard</a>,
  <a href="https://creativecommons.org/licenses/by-nc/2.0/">CC BY-NC 2.0</a>, modified)
  </span>
</div>

* MA originally developed by Swiss astrophysicist Fritz Zwicky from
  1940s to 1970s (Fritz Zwicky, 1948, *Morphological astronomy*)

* Adopted by *Swedish Morphological Society*
  (Tom Ritchey, 2011, *Wicked Problems &mdash; Social Messes*; http://www.swemorph.com/)
  * Full-featured software MA/Carma™ developed since 1990s
  * Used in consultancy work


## The morphological field

* A tabular display of multi-dimensional problem space
* Each *column* is one *parameter*
* Each column's *rows* list the possible values of the parameter
* Parameters are by definition categorical


|Parameter A |Parameter B |Parameter C |Parameter D |
|:-----------|:-----------|:-----------|:-----------|
|A1          |B1          |C1          |D1          |
|A2          |B2          |C2          |D2          |
|A3          |B3          |C3          |            |
|A4          |            |C4          |            |

<!--

 | table | column |
 |-------|--------|
 | 1     | 2      |

-->


## The cross-consistency matrix (CCM)

* Each paramater value is checked pairwise for consistency with all values of
  all other parameters
* Results put into half-sided matrix (e.g. lower triangle)
* With CCM, many combinations of paramater values can be excluded as inconsistent</br>
  $\rightarrow$ reduces size of problem space

---

<table>
    <thead>
        <tr>
            <td colspan="2" rowspan="2" class="off"></th>
            <th colspan="4" class="header-span">Parameter A</th>
            <th colspan="3" class="header-span">Parameter B</th>
            <th colspan="4" class="header-span">Parameter C</th>
        </tr>
        <tr>
            <th class="header">A1</th>
            <th class="header">A2</th>
            <th class="header">A3</th>
            <th class="header">A4</th>
            <th class="header">B1</th>
            <th class="header">B2</th>
            <th class="header">B3</th>
            <th class="header">C1</th>
            <th class="header">C2</th>
            <th class="header">C3</th>
            <th class="header">C4</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="3" class="header-span">Parameter B</td>
            <td class="header">B1</td>
            <td class="dark"><i class="fa fa-check"></i></td>
            <td class="dark"><i class="fa fa-check"></i></td>
            <td class="dark"></td>
            <td class="dark"></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
        </tr>
        <tr>
            <td class="header">B2</td>
            <td class="dark"></td>
            <td class="dark"><i class="fa fa-check"></i></td>
            <td class="dark"><i class="fa fa-check"></i></td>
            <td class="dark"></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
        </tr>
        <tr>
            <td class="header">B3</td>
            <td class="dark"></td>
            <td class="dark"></td>
            <td class="dark"><i class="fa fa-check"></i></td>
            <td class="dark"><i class="fa fa-check"></i></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
        </tr>
        <tr>
            <td rowspan="4" class="header-span">Parameter C</td>
            <td class="header">C1</td>
            <td class="light"></td>
            <td class="light"><i class="fa fa-check"></i></td>
            <td class="light"><i class="fa fa-check"></i></td>
            <td class="light"></td>
            <td class="dark"></td>
            <td class="dark"></td>
            <td class="dark"><i class="fa fa-check"></i></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
        </tr>
        <tr>
            <td class="header">C2</td>
            <td class="light"><i class="fa fa-check"></i></td>
            <td class="light"></td>
            <td class="light"></td>
            <td class="light"></td>
            <td class="dark"><i class="fa fa-check"></i></td>
            <td class="dark"></td>
            <td class="dark"></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
        </tr>
        <tr>
            <td class="header">C3</td>
            <td class="light"><i class="fa fa-check"></i></td>
            <td class="light"><i class="fa fa-check"></i></td>
            <td class="light"></td>
            <td class="light"></td>
            <td class="dark"></td>
            <td class="dark"><i class="fa fa-check"></i></td>
            <td class="dark"><i class="fa fa-check"></i></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
        </tr>
        <tr>
            <td class="header">C4</td>
            <td class="light"><i class="fa fa-check"></i></td>
            <td class="light"></td>
            <td class="light"></td>
            <td class="light"></td>
            <td class="dark"></td>
            <td class="dark"></td>
            <td class="dark"></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
            <td class="off"></td>
        </tr>
        <tr>
            <td rowspan="2" class="header-span">Parameter D</td>
            <td class="header">D1</td>
            <td class="dark"></td>
            <td class="dark"><i class="fa fa-check"></i></td>
            <td class="dark"><i class="fa fa-check"></i></td>
            <td class="dark"><i class="fa fa-check"></i></td>
            <td class="light"><i class="fa fa-check"></i></td>
            <td class="light"><i class="fa fa-check"></i></td>
            <td class="light"></td>
            <td class="dark"><i class="fa fa-check"></i></td>
            <td class="dark"></td>
            <td class="dark"></td>
            <td class="dark"></td>
        </tr>
        <tr>
            <td class="header">D2</td>
            <td class="dark"><i class="fa fa-check"></i></td>
            <td class="dark"></td>
            <td class="dark"></td>
            <td class="dark"></td>
            <td class="light"></td>
            <td class="light"></td>
            <td class="light"><i class="fa fa-check"></i></td>
            <td class="dark"></td>
            <td class="dark"><i class="fa fa-check"></i></td>
            <td class="dark"><i class="fa fa-check"></i></td>
            <td class="dark"><i class="fa fa-check"></i></td>
        </tr>
    </tbody>
</table>

---

## The R package `morphr`

* Goals:
  * Make MA accessible in R
  * Make MA software platform-independent and open source
  * Allow use of MA on the web (e.g. for distributed teams)
* Implementation:
  * Based on RStudio's `DT` package (fork), i.e. using jQuery plugin *DataTables*
  * Using Shiny to provide interactivity
  * A morphological field is installed using function `installMorphField()`

---

## Installation

Install from github using `devtools`:


```r
devtools::install_github("sgrubsmyon/morphr")
```

---

## Example usage




```
## 
## Attaching package: 'shiny'
```

```
## The following objects are masked from 'package:morphr':
## 
##     dataTableOutput, renderDataTable
```

```
## Warning: replacing previous import by 'shiny::includeHTML' when loading
## 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::knit_print.shiny.tag' when
## loading 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::code' when loading
## 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::includeScript' when loading
## 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::includeMarkdown' when loading
## 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::tags' when loading
## 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::is.singleton' when loading
## 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::withTags' when loading
## 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::img' when loading 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::tagAppendAttributes' when
## loading 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::knit_print.shiny.tag.list'
## when loading 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::knit_print.html' when loading
## 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::tagAppendChild' when loading
## 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::includeCSS' when loading
## 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::br' when loading 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::singleton' when loading
## 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::span' when loading
## 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::a' when loading 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::tagList' when loading
## 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::strong' when loading
## 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::tag' when loading 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::p' when loading 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::validateCssUnit' when loading
## 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::HTML' when loading
## 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::h1' when loading 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::h2' when loading 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::h3' when loading 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::h4' when loading 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::h5' when loading 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::h6' when loading 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::tagAppendChildren' when
## loading 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::em' when loading 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::div' when loading 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::pre' when loading 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::htmlTemplate' when loading
## 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::suppressDependencies' when
## loading 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::tagSetChildren' when loading
## 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::includeText' when loading
## 'crosstalk'
```

```
## Warning: replacing previous import by 'shiny::hr' when loading 'crosstalk'
```

```
## Error in appshot.shiny.appobj(structure(list(httpHandler = function (req) : appshot of Shiny app objects is not yet supported.
```
