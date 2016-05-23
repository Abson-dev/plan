---
permalink: examples.html
layout: default
title: Examples
submenu: home
---

Each `plan` function is documented, with code examples being provided in many
cases.  For example, `help("plot,gantt-method")` provides documentation on
plotting gantt diagrams, and `example("plot,gantt-method")` runs some examples.
There is also a vignette, available with `vignette("plan")`. Still, it may help
to show some of the capabilities on this web page.

**Burndown Chart Example**

The following shows how the author monitored the writing of the `burndown` functions.

First, he created a text file called `burndown.dat`, with contents as follows.
{% highlight %}
Start,    2006-04-08 12:00:00 
Deadline, 2006-04-11 20:00:00 
Key, Description,             Effort
  1, Code read.burndown(),    4
  2, Code summary.burndown(), 1
  3, Code plot.burndown(),    5
  4, Create R package,        2
  5, Write documentation,     2
  6, Set up website,          1
Key, Done,  Time
  1,     5, 2006-04-08 13:00:00
  2,     5, 2006-04-08 13:30:00
  1,    10, 2006-04-08 14:00:00
  2,    50, 2006-04-08 15:00:00
  4,     5, 2006-04-08 19:30:00
  5,     5, 2006-04-08 20:00:00
  4,   100, 2006-04-08 21:16:00
  1,    50, 2006-04-09 09:10:00
  3,     5, 2006-04-09 09:41:00
  3,    30, 2006-04-09 10:18:00
  3,    80, 2006-04-09 11:00:00
  2,    60, 2006-04-09 12:00:00
  2,   100, 2006-04-09 12:10:00
  1,    70, 2006-04-09 12:30:00
  5,    30, 2006-04-09 13:50:00
  5,    90, 2006-04-09 14:20:00
  5,   100, 2006-04-09 14:30:00
  1,   100, 2006-04-09 14:35:00
  3,   100, 2006-04-09 14:40:00
  6,   100, 2006-04-09 16:00:00
{% endhighlight %}

Then, he executed
{% highlight r %}
burndown <- read.burndown("burndown.dat")
plot(burndown)
{% endhighlight %}


<!--
png("burndown.png",width=7,height=4,unit="in",res=100,pointsize=10)
-->
The results are as follows

![burndown](burndown.png)



**Gantt Diagram Example**

The code below creates a gantt chart for an imaginary MSc program that is still
underway. It employs `new()` and `ganttAddTask()` to create the gantt data.
This could also be done with either `as.gantt()` or `read.gantt()`.

<!-- png("gantt.png",width=7,height=4,unit="in",res=100,pointsize=10) -->

{% highlight r %}
library("plan")
g <- new("gantt")
g <- ganttAddTask(g, "Courses") # no times, so a heading
g <- ganttAddTask(g, "Physical Oceanography (A)", "2016-09-03", "2016-12-05", done=100)
g <- ganttAddTask(g, "Chemistry Oceanography (B)", "2016-09-03", "2016-12-05", done=100)
g <- ganttAddTask(g, "Fluid Dynamics (A+)", "2016-09-03", "2016-12-05", done=100)
g <- ganttAddTask(g, "Biological Oceanography", "2017-01-03", "2017-04-05")
g <- ganttAddTask(g, "Geological Oceanography", "2017-01-03", "2017-04-05")
g <- ganttAddTask(g, "Time-series Analysis", "2017-01-03", "2017-04-05")
g <- ganttAddTask(g, "Research") # no times, so a heading
g <- ganttAddTask(g, "Literature review", "2016-09-03", "2017-02-01", done=20)
g <- ganttAddTask(g, "Develop analysis skills", "2016-09-03", "2017-08-01", done=30)
g <- ganttAddTask(g, "Thesis work", "2016-10-01", "2018-07-15", done=30)
g <- ganttAddTask(g, "Thesis proposal", "2017-05-01", "2017-06-01")
g <- ganttAddTask(g, "Writing (papers & thesis)", "2017-03-01", "2018-07-15")
g <- ganttAddTask(g, "Defend thesis", "2018-09-01", "2018-09-05")
plot(g, ylabel=list(font=ifelse(is.na(g[["start"]]), 2, 1)),
     event.time="2016-12-13", event.label="Report Date")
par(lend="square") # default is round
legend("topright", pch=22, pt.cex=2, pt.bg=gray(c(0.3, 0.9)),
       border="black", 
       legend=c("Completed", "Not Yet Done"), title="MSc plan", bg="white")
{% endhighlight %}

This yields a diagram like the one given below.

![gantt](gantt.png)

How might the student and her advisory committee, interpret this diagram?

To begin with, the grades are good, so there's no need to worry
about those classes coming up in the second term. It makes sense to focus
instead on the research component.

The vertical line indicates the time the diagram was made.  Visual comparison
of this line with the colour breaks in the task bars indicates three things.
(a) The literature review is behind schedule.  (b) Progress in building up
analysis skills is good. (c) The thesis work is ahead of schedule.

The next big task is to write and defend a thesis proposal. If the diagram is a
true indication, it will be important to set aside sufficient time for reading
the literature, but this should not be a problem because the research is going
so well.

It can be helpful to regenerate such diagrams regularly throughout a research
program, in order to assess progress and make decisions about changes to plans.
For example, the thesis proposal would likely contain a similar diagram that
additionally had components for sub-tasks in the research, and perhaps for
publications or thesis chapters.
