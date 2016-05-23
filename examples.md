---
permalink: examples.html
layout: default
title: Examples
submenu: home
---

Each `plan` function is documented, with code examples being provided in many
cases.  For example, `help("plot,gantt-method")` provides documentation on
plotting gantt diagrams, and `example("plot,gantt-method")` runs some examples.

There is also a brief vignette, available with `vignette("plan")`.

A good way to learn is to use the built-in datasets, e.g. `data("gantt")`.

A complex (and realistic) example of a gantt chart for a MSc program that is
still underway. Note that the method of generating the data is one of three
available; other choices are `as.gantt()` and `read.gantt()`.

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

This yields a diagram like the one given below. Here is how it might be
interpreted, by the student ("Sally", say) and her supervisory committee...

Visual comparison of the colours of the task components with the vertical line
suggests that Sally is a bit behind on her literature review, but she is doing
well in learning the research skills she will need for her thesis. Indeed, the
actual thesis work is going quite a lot faster than planned. The diagram may
motivate Sally to set aside more time for reading, because the next big event
is a thesis-proposal defense. (We can put aside the classes as a worry, given
the grades in Sally's first term.)

This diagram is a sort of end-of-term assessment. Most likely, Sally's
supervisor will encourage her to make a similar diagram for inclusion in her
thesis proposal. That's still a few months away, and by then Sally should be
able to add tasks for individual chapters and papers.

![gantt](gantt.png)


