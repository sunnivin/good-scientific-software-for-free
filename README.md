# Slides with marp 
The code quality is essential for reproducibility and maintainability. In this talk I will show some tricks you can use to automatically increase the quality of your Python code at "zero" cost. 

Keywords: pre-commits, python, good enough practices




## Usage 
The content of this talk is placed in the file called `talk.md` and is mostly written in markdown. Styling that not (yet) exists in markdown is controlled with `CSS` or `HTML`. 

### Convert to html with a template file
Pure markdown files can (currently) not split a slide in column without html. 

To convert the slidedeck into a '*.html' file: 

    marp --theme-set ngi-theme.css --html -w talk.md


### Some nice issues to pay attention to 

- [Import document](https://github.com/marp-team/marpit/issues/135) style. 


