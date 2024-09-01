<H1> Time Table </H1>

This project is a combination of R and LaTeX and designs an aesthetic timetable for FCCU courses.

<H2> Instructions </H2>

1. Open the .proj file to load the environment.
2. In the R code chunk, navigate to the "Extract Courses" Section.
3. Choose your courses.
4. Render the document.

Note: The code requires that you have at least one course per day. If your timetable does not meet this requirement then you will need to modify the code a bit.

For example, assume you do not have classes on Monday, then
- In "Transform Data", comment tempM
```
tempM <- data.frame(day = "1", selected[which(str_detect(selected[,8], "M")),c(3:11)])
tempM <- arrange(tempM, day, start)
tempM <- tempM %>%
    mutate(course = paste0(code, ": ", title, " (", sec, ") (", credits, ")")) %>%
    mutate(code = NULL, title = NULL, sec = NULL, credits = NULL, days = NULL)
tempM <- tempM[,c(1,6,3,4,5,2)]
```
- In "Generate LaTeX Code", comment tempML
```
tempML <- 1:nrow(tempM)
for (i in 1:nrow(tempM)) {
    tempML[i] <- paste0(
        "&", tempM[i,2], "&", tempM[i,3], "&", tempM[i,4], "&", tempM[i,5], "&", tempM[i,6], "\\\\")
}
tempML <- paste0(tempML, collapse = "")
```
- In LateX code, comment the multirow
```
\phantom{} \\ \hline
\multirow{`r nrow(tempM)`}{*}{\textbf{\textcolor{teal!60!black}{Monday}}} `r tempML` \hline
```
