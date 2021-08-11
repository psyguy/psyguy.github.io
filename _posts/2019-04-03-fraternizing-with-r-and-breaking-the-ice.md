---
published: true
---
Or, **_Learning R: Why and How -- A guide for absolute strangers_**

I am a retired electrical engineer (majoring in telecommunication) and have done a master's in AI before pursuing a master's in (primarily quantitative) psychology, which has led me to where I am, doing a Ph.D. in the methodology of psychological processes. I used to be quite proficient in Matlab (as I had enough of it in my EE and AI). However, after switching tracks to behavioral sciences, I now identify as a radical R evangelist.

Sadly, too many fellow psychologists, even those working in quantitative psychology, are total strangers to R---and that is genuinely heart-breaking.

When speaking to non-R users, one frequently hears only a handful of excuses why people are reluctant to start using R.  Here, I try to address them. However, I will not talk much about R's computational power and efficiency compared to other languages (more specifically, Matlab, Python, and Julia), as I believe an average user in psychology would not notice any issues regarding the speed or efficiency; as a pretty advanced user, I have not encountered any significant efficiency problems in the past few years. In what follows, I try to encourage you to learn _the true and only way of doing statistics,_ which, as everyone knows, is **R**.

**Disclaimer:** only the first figure belongs to me; others can be removed upon request.

## _Why do you think I need to learn R?_ 

SPSS and Matlab are products of filthy Capitalism: They are very costly---which you would probably not care if you use university/student licenses or pirate them---and they do not belong to the open-source culture. I believe they are barriers on our way to a utopian open science future. Moreover, in general, SPSS sucks big time; it is limited in its functionality and the analyses it can do. It shouldn't be surprising that SPSS is getting closer and closer to its death, although the inertia

Matlab, on the other hand, is not well-suited for [quantitative] psychology; it lacks essential functions and packages and doesn't handle the kind of data we encounter in social and behavioral sciences properly. Yes, it is a functional language for [hardcore] signal analysis and control engineering (and perhaps some numerical analyses/simulations in science and engineering). However, in many cases, Python and/or Julia are better alternatives. Also, although Matlab has always been a dominant language in engineering, there are indications that it is losing it to R.

One can spot these declines in [Google Trends](https://trends.google.com/trends/explore?date=2004-01-01%202021-08-11&q=%2Fm%2F053_x,%2Fm%2F018fh1,%2Fm%2F0212jm#TIMESERIES)--although it is not a definite indicator of this claim. It is worth noting that Matlab owes much of its popularity to _pirates,_ mostly users from countries (such as Iran) where there are no (proper) copyright laws in order. Just take a close look at the Google Trends link, and compare Iran's rank for Matlab (1st) to its rank for R and Python (66th and 59th, respectively).

![image This is a plot showing the search trend of Matlab, R, and SPSS in Google search. R has made the most growth, surpassing Matlab around 2012.](https://user-images.githubusercontent.com/8527082/129043634-8fcb87ff-262d-4077-a83b-63cd8e519072.png)


## _I am already familiar with Matlab/SPSS and I'm quite 'happy' with it._

Are you _really_ happy, though?

People, especially SPSS users, are usually entrapped in an abusive relationship; they rely on it for their work and have to deal with its sufferings since they are too afraid to leave it and move on to a better alternative. Some are even suffering from some sort of Stockholm syndrome.

You are not alone there.

![image This is a meme, in which an SPSS user asks an R user whether his dog bites. The R user (the dog owner) says "no, but he can hurt you in other ways." Then dog then utters "SPSS is for NOOBS", and the SPSS user breaks into tears.](https://user-images.githubusercontent.com/8527082/55495028-507e6d00-563c-11e9-9169-c02553fb4c5c.png)

## _What can R offer that others do not?_

R is fabulous. It is superior to other languages in countless ways when it comes to statistical analyses. Most importantly, it has a very active community and a ton of useful packages which satisfy most---if not all---of your needs. You can perform advanced statistical modelings and analyses that otherwise require special, costly software; you can easily do advanced latent trait modelings (IRT, EFA, CFA, and SEM) and make complex hierarchical generalized linear models. You also can go full Bayesian in R with JAGS. Except for some advanced dynamic structural equation models (e.g., with latent mean centering) that are better achieved by Mplus, you can do virtually anything with the power of R---you may even run (and automate) your Mplus analysis [from within R](https://github.com/michaelhallquist/MplusAutomation).

![image This is a meme in which the a guy is talking about how he intends to use SPSS for his analyses, and hiw dogs overhears the conversation, and soffocates the owner with a pillow later that night.](https://user-images.githubusercontent.com/8527082/129057565-835570d1-ab4c-46c8-a921-226af1a7c035.png)

With R (and its siblings, Rmarkdown and Shiny) you can do things so easily that is hard to imagine elsewhere. You can make excellent LaTeX or HTML reproducible (APA) papers, technical reports, books, and blogs with [Rmarkdown](https://bookdown.org/yihui/rmarkdown/), [bookdown](https://bookdown.org/yihui/bookdown/), and [blogdown](https://bookdown.org/yihui/blogdown/). You can create interactive apps with [Shiny](https://shiny.rstudio.com/gallery/) to [collect experiment data](https://psyr.org/shiny.html), make tutorials, and make powerful [BI dashboards](https://rviews.rstudio.com/2017/09/20/dashboards-with-r-and-databases/), and deploy them to [RStudio Shiny Server](https://www.shinyapps.io) or your own server. You can build [interactive maps](http://rmaps.github.io/) and produce [magnificent visualizations](https://www.r-graph-gallery.com/). You can do machine learning in R ([this](https://lgatto.github.io/IntroMachineLearningWithR/) and [this](https://www.datacamp.com/community/tutorials/machine-learning-in-r) for a start) and you can, like [Andrew Piper](https://twitter.com/_akpiper) and others, use R in [digital humanities](https://humanitiesdata.org/).


## _But I'm too old for this :(_

This graph (from Navarro’s [intro slides](https://psyr.djnavarro.net/misc/overview.pdf)) summarizes why you should still start learning R:

![image A plot showing that after some initial efforts, learning R or Python brings much more reward](https://user-images.githubusercontent.com/8527082/55494231-a94d0600-563a-11e9-816d-2bbfd6cab64f.png)
 
I can assure you that it is quite easy to reach the point where R surpasses the maximum reward you can get from SPSS, even if you start from an absolute zero. You do not need to learn all of the stuff mentioned above at once; you first lay a fundamental basis of R knowledge and then learn more advanced topics and techniques according to your needs.

## _Owkay, but I don't know where to start :(_

There are literally thousands of free resources to learn R out there; just have a look at Mine Dogucu's [**learnR4free**](https://www.learnr4free.com/en/index.html). This overload of information prevents most people from starting the journey. Hence, I only mention two handy (and relatively concise) resources which I have recently found:

1. [Danielle Navarro](https://twitter.com/djnavarro)'s [_**R for Psychological Science**_](https://psyr.djnavarro.net/), which is well-tailored for psychologists; and

2. Ben Whalley's [_**Just Enough R**_](https://benwhalley.github.io/just-enough-r/), which, as the name suggests, is just enough to kickstart your journey.

However, **for an even faster, more efficient learning,** you can also benefit from [RStudio cheat sheets](https://www.rstudio.com/resources/cheatsheets/) after you have the fundamental knowledge of R. I suggest to follow them in this order:
-    Base R
-    RStudio IDE Cheat Sheet
-    Data Import Cheat Sheet
-    Advanced R
-    Data Transformation Cheat Sheet
-    R Markdown Cheat Sheet
-    Data Visualization Cheat Sheet
-    Apply Functions Cheat Sheet 

**Now that you are beginning**, I very strongly suggest mastering packages `plyr` and `dplyr` so you do not look like a troglodyte to other R users. The former offers a better way of writing `apply` functions. The latter is the best way of handling data intuitively and efficiently with pipe operator (`%>%`) and its data manipulation functions. You can gain a good understanding of `plyr` in Hadley Wickham's [paper](https://www.jstatsoft.org/index.php/jss/article/view/v040i01/v40i01.pdf) in the Journal of Statistical Software (2011) or [this tutorial](https://seananderson.ca/2013/12/01/plyr/). For `dplyr`, you may benefit from Garrett Grolemund’s data wrangling tutorial ([webinar](https://www.rstudio.com/resources/webinars/data-wrangling-with-r-and-rstudio/) and [slides](https://github.com/rstudio/webinars/blob/master/05-Data-Wrangling-with-R-and-RStudio/wrangling-webinar.pdf)). 


**You should also know that** Google, Stack Overflow, and Stack Exchange are your allies. In +90% of the cases, you can find literally the exact pieces of code you need in less than a minute or two. If you couldn't find a proper answer to your question (or had difficulty understanding what you have discovered), simply ask it on [Cross Validated](https://stats.stackexchange.com), where a kind stranger will help you quite soon. Interestingly, you can cite questions and answers you find on Stack Overflow and Stack Exchange; they give you BibTeX citation code. It's worth mentioning that some people receive quicker responses if they post their questions on [Reddit](https://www.reddit.com/r/rstats/). In the end, it's up to you.

![image A joke about O'Reilly's books, whit a book whose title reads "Essential Copying and Pasting From StackOverflow"](https://user-images.githubusercontent.com/8527082/55495100-760b7680-563c-11e9-8f3d-e04e10c1c6c3.png)

## _But I'm super busy :( How long does it all take?_

This is perhaps the most solid excuse to postpone learning useful skills, whether they are about programming (learning another language, or practicing a [decent coding style](https://google.github.io/styleguide/Rguide.xml)), using a new tool (like [Git versioning](https://happygitwithr.com/)), or deepening your superficial theoretical background on a subject. One should never forget this lesson, which a King of Jerusalem, probably King Solomon, draws from his life experience:

>If the ax is dull and its edge unsharpened, more strength is needed, but skill will bring success.
-- (Ecclesiastes, 10:10)

![image A comic showing that a person save a lot of time by sharpening their saw before dstarting to cut a tree](https://user-images.githubusercontent.com/8527082/55495515-5a54a000-563d-11e9-9486-3c321ddbeb02.png)

I think that the tutorials I mentioned above should take less than a couple days to finish. Also, you can always benefit from the cheat sheets when you need them. The data wrangling slides (`dplyr`) took me less than an hour (20-30 minutes?) to master, and `plyr` shouldn't be much different.

To be amazed---and constantly surprized---by the power and wonders of R, I strongly suggest following [**R function a Day**](https://twitter.com/rfunctionaday) and [**R posts you might have missed!**](https://twitter.com/icymi_r) on Twitter (the latter has a [monthly digest](https://thedatasciencedigest.substack.com/) you can subscribe to).

## _Before you go,_

As a gift for reading this far, I would like to introduce [Ditto clipboard manager](https://ditto-cp.sourceforge.io/), a tool that helps you keep dozens (or even thousands) of copied/cut images and texts (also files!) in your clipboard with a very tiny overload on your PC. You can always search in the list, and you may use it as a draft pad for quick notes. It takes few minutes to figure it out, and you will soon wonder how you had managed to work with a computer without it.

Since _Sharing is Caring,_ sharing this article is appreciated, and feel free to leave comments.
