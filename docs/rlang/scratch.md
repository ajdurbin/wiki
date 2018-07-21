# links #
<https://github.com/qinwf/awesome-R>


# Python integrations #
`reticulate` is the R interface for Python and provides multiple sorts of functionality. We can call Python from R, access objects, use virtual environments, use inline Python in R Markdown documents, source Python from R scripts, and more. Accessing Python objects is still a little awkward, but we can now much easier source Python programs with arguments than using a `system` call. Primary use case would be using inline Python code in Shiny applications since Jupyter notebooks allow interactive running of chunks and R Markdown does not.

<https://github.com/rstudio/reticulate>

# Pip-like functionality #
`packrat` is the dependency management system similar to PIP.

<https://rstudio.github.io/packrat/>


# database connections #
```
library(RODBC)
library(dplyr)
library(ggplot2)
library(lubridate)
cnxn <- odbcConnect("MYSQLSERVERDSN01") # credentials optional
result <- sqlQuery(cnxn, 'select * from mytable')

# there are bugs here for end of month calculations
# this code should fix that issue
end_date <- ceiling_date(as.Date(Sys.Date()) %m-% months(6), unit = "month") - days(1)

# this is how we do relative queries
result <- sqlQuery(cnxn, paste0("select * from mytable where date>='", as.character(end_date),"'"))
```
