# Slides with marp 
This repository contains a talk about which tricks you can get for "free" to make good enough scientific software and why you should care about it. 


## Abstract 

As a scientific developer you are expected to deliver good enough science and code to 




## Usage 
The content of this talk is placed in the file called `talk.md` and is mostly written in markdown. Styling that not (yet) exists in markdown is controlled with `CSS` or `HTML`. 

### Convert to html with a template file
Pure markdown files can (currently) not split a slide in column without html. 

To convert the slidedeck into a '*.html' file: 

    marp --theme-set ngi-theme.css --html -w talk.md


### Some nice issues to pay attention to 

- [Import document](https://github.com/marp-team/marpit/issues/135) style. 


