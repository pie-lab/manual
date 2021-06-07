# Useful Links

## R and RMarkdown

- [Big Book of R](https://www.bigbookofr.com/) -- A collection of every book using R!

### Beginners

- [R for Data Science](https://r4ds.had.co.nz/)
- [YaRrr! The Pirate's Guide to R](https://bookdown.org/ndphillips/YaRrr/) -- this one is great for undergraduates
- [Learning Statistics with R](https://learningstatisticswithr-bookdown.netlify.app/)
- [Cookbook for R](http://www.cookbook-r.com/)
- [R for Psychological Science](http://psyr.djnavarro.net/)

### Cheatsheets

All cheatsheets can be downloaded [here](https://rstudio.com/resources/cheatsheets/).

Especially useful cheatsheets include:

- RMarkdown Reference
- Data Viz
- Transformation
- Iteration
- Purrr
- Stringr

### Data Visualization

- [How to make better spaghetti plots](https://njt-rstudio20.netlify.app/#1)
- [DiagrammR](http://rich-iannone.github.io/DiagrammeR/index.html) -- flowcharts and diagrams
- [DAG models](https://ggdag.malco.io/articles/intro-to-dags.html)

### Markdown

- [RMarkdown: The Definitive Guide](https://bookdown.org/yihui/rmarkdown/)
  
  - See the section on [Websites](https://bookdown.org/yihui/rmarkdown/websites.html)
  
- [Advanced R Markdown (customization and extensions)](https://slides.yihui.org/2019-rstudio-conf-rmarkdown-workshop.htm#1) -- lots of useful tips in here, once you're familiar with Markdown.
  
- [Awesome tables with kable (PDF)](https://haozhu233.github.io/kableExtra/awesome_table_in_pdf.pdf)
- [Awesome tables with kable (HTML)](http://haozhu233.github.io/kableExtra/awesome_table_in_html.html)
- [How to convert a Google doc to RMarkdown](https://www.storybench.org/convert-google-doc-rmarkdown-publish-github-pages/)
- [Making slides](https://arm.rbind.io/slides/xaringan.html#1)

### Using Zotero with RMarkdown

1. [Download and install](https://www.zotero.org/download/) Zotero.
2. [Download and install](https://retorque.re/zotero-better-bibtex/installation/) the Better BibTex add-on.
3. Open Zotero, and go to Preference.
    - Under the Export tab, make sure Default Format is "Better BibTex Citation Key Quick Copy."
    - Under the Better BibTex tab, make sure the Citation key format is something you'll find useful. (I recommend `[auth:lower][veryshorttitle:lower:alphanum][year]`). 
4. At this point, you can choose to export your Zotero library to a .bib file, save it to the working directory of your RMarkdown file, and make sure the bibliography line is pointing to that file. Once that's done, you can simply drag from Zotero to your RMarkdown file, to create in-line citations, and the references section at the end will be created for you.

OR, you can install the `citr` package, which works with your Zotero library, so you don't need to create a new .bib file manually for each paper. Seems really convenient! ([More information here](https://github.com/crsh/citr).)

### GitHub

- [Happy Git with GitHub and R](https://happygitwithr.com/)
- [Cheatsheet for terminal commands](https://gist.github.com/cferdinandi/ef665330286fd5d7127d)

### Text Analysis

- [Text mining Twitter with TidyText](https://www.earthdatascience.org/courses/earth-analytics/get-data-using-apis/text-mining-twitter-data-intro-r/) -- includes n-gram network plot
- [Word vectors with tidy data principles](https://www.r-bloggers.com/word-vectors-with-tidy-data-principles/)

### Iteration

- [Purrr](https://emoriebeck.github.io/R-tutorials/purrr/)

### Writing functions

- [Non-standard evaluation](http://adv-r.had.co.nz/Computing-on-the-language.html)

### Making tables

- [`gt` package](https://themockup.blog/static/gt-cookbook.html)

### Reproducibility

- [8 things to make research more findable](http://datacolada.org/69)


## Writing

- [Dan Simons -- writing guide](http://www.dansimons.com/resources/writing_tips.html)
- [EJ Wagenmakers -- Teaching graduate students how to write clearly](http://www.ejwagenmakers.com/2009/TeachingTipsWriting.pdf)
- [Writing Workshop](https://osf.io/z4n3t/) -- includes both tips on how to write (content), as well as the practice of writing regularly. This book also provide the foundation for starting a writing group. 
- [Practical Typography](https://practicaltypography.com/)

### Grammar and syntax

- [Verb tenses](https://academicguides.waldenu.edu/writingcenter/grammar/verbtenses)

### Finding articles

- [CrossRef](https://doi.crossref.org/simpleTextQuery) -- get DOI's quickly
- [Connected Papers](https://www.connectedpapers.com/) -- find other articles related to a specific research article

### Bibliography

- [Zotero](https://zotero.org)
- [ZBib](https://zbib.org/)

### Reviewing the literature
- [Guide from the University of South Australia](https://lo.unisa.edu.au/mod/page/view.php?id=489316)

### Responding to reviews

- [Workflow for R&R](https://getsyeducated.blogspot.com/2020/08/a-workflow-for-dealing-with-dread-of.html)

## Presentations

- [Public speaking for academics](https://mfr.osf.io/render?url=https%3A%2F%2Fosf.io%2Fd8wm9%2Fdownload)
- [Free PowerPoint templates](https://www.slidescarnival.com/category/free-templates)


## Authorship

- [tenzing](https://martonbalazskovacs.shinyapps.io/tenzing/) -- this is a useful Shiny app for creating text (for Word or papaja) that includes author affiliations and also creditorship using the CRediT system. Espescially handy for large teams. 

## Statistics

### Probability

- [Seeing Theory](https://seeing-theory.brown.edu/)

### Generalized Linear Model

- [Logistic regression is not fucked](http://jakewestfall.org/blog/index.php/2018/03/12/logistic-regression-is-not-fucked/)
- [Melt the clock: tidy time series analysis](https://slides.earo.me/rstudioconf19/#1)
- [_Causal Inference: What If_ by Miguel A. Hernán & James M. Robins](https://www.hsph.harvard.edu/miguel-hernan/causal-inference-book/) -- Chapter titles: A defintion of causal effect, Randomized experiments, Observational studies, Effect modification, Interaction, Graphical representation of causal effects, Confounding, Selection bias, Measurement bias, Random variability, Why model, IP weighting and marginal structural models, Standardization and the parametric g-function, G-estimation of structural nested models, Outcome regression and propensity scores, Instrumental variable estimation, Causal survival analysis, Variable selection for causal inference, Time-varying treatments, Treatment-confounder feedback, G-methods for time-varying treatments, Target trial emulation

### Machine learning+

- [Statistical rethinking](http://xcelab.net/rm/statistical-rethinking/)
- [Machine learning for psychologists: A gentle introduction](https://github.com/tyarkoni/ML4PS)

- [Specification curves](https://github.com/dcosme/specification-curves/blob/master/SCA_tutorial.md)

### Text analysis

- [Structual Topic Models](https://juliasilge.com/blog/evaluating-stm/)
- [Erin Buchanan (Stats of Doom) NLP](https://statisticsofdoom.com/page/natural-language-processing/)

### Statistical Power

- [Powering interactions](https://approachingblog.wordpress.com/2018/01/24/powering-your-interaction-2/)
- [Explore researcher degrees of freedom](https://joachim-gassen.github.io/2019/03/explore-your-researcher-degrees-of-freedom/)

### Structural Equation Modeling

- [Michael Hallquist's SEM course](https://psu-psychology.github.io/psy-597-SEM)
- [Erin Buchanan (Stats of Doom) SEM](https://statisticsofdoom.com/page/structural-equation-modeling/) 

### Mediation and Moderation
- [Erin Buchanan (Stats of Doom) Mediation/Moderation](https://statisticsofdoom.com/page/med-mod/)

### Longitudinal data analysis
- [Personality Development Collaborative](https://www.personalitydevelopmentcollaborative.org/) -- also includes links to datasets that may be useful.


## Graduate School

- [The Illustrated Guide to a Ph.D.](http://matt.might.net/articles/phd-school-in-pictures/)
- [Raul Pacheco's resources](http://www.raulpacheco.org/resources/) -- a good collection of tips for everything from time management, to how to read and write, to using social media.
- [Escaping the hamster wheel by Elliot Berkman](https://www.psychologytoday.com/us/blog/the-motivated-brain/201709/advice-grad-students-and-senior-faculty)

## Life

- Note that being a GE and having a research fellowship are considered different forms of compensation. [Here’s a guide to preparing your (2019) federal taxes](http://pfforphds.com/prepare-grad-student-tax-return/).

