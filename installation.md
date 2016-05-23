---
permalink: installation.html
layout: default
title: Installation
submenu: installation
---

An official version of plan is supplied on CRAN, and it may be installed with
```R
install.packages("plan")
```
 within an R session.  To get the newest version (still in development), use
```R
install_github("dankelley/plan", ref="develop")
```
(Remove the `ref` argument to use the more stable `master` branch.)

If the previous fails, you may need to install the `devtools` package, with
```R
install.packages("devtools")
```
which is a step you won't need to repeat unless you uninstall `devtools`.


