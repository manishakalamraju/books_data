# books_data
This repository contains data about three category of books sold in India for the years 2018 and 2019.It involves data cleaning and data analysis using R to find the category with highest sales.
Let us consider the data related to books sold for the years 2018 & 2019 in the category of school,college and competition to find which category of books has the highest sales.

## Step 1: Using R packages
In this project we will use Tidyverse package for analysis and Here,Skimr and Janitor packages for data cleaning purpose.
```{r installing packages,echo=TRUE}
install.packages("tidyverse")
install.packages("here")
install.packages("skimr")
install.packages("janitor")
install.packages("magrittr")
```
Once packages are installed we can load them by using library() function with package name inside parentheses as shown

```{r loading packages,echo=TRUE}
library(tidyverse)
```
```{r,echo=TRUE}
library(here)
library(skimr)
library(janitor)
library(magrittr)
```

## Step 2: Viewing data
Now,we can upload the data by selecting the data file in 'From text(readr)' from import dataset in the Environment pane.Let us consider a new data frame as 'books'. 

```{r loading data,echo=TRUE}
books <- read.csv("books_data_india.csv")
head(books)
```
In order to view the column names use colnames() function as shown
```{r}
colnames(books)
```
## Step 3: Data cleaning
In order to find the most purchased category of books select the required columns and rename for ease of access.
```{r data cleaning,echo=TRUE}
books_sold <- books %>% select("Quantity","Ship.State","Category")%>%
  rename(state="Ship.State")
books_sold$Category <- tolower(books_sold$Category)
books_sold$state <- toupper(books_sold$state)
```
## Step 4: Analysis
Using summarize() function find the total no.of books for each category.
```{r summarize, echo=TRUE}
books_sold %>% group_by(Category) %>% summarize(total_books=sum(Quantity))
```
## # A tibble: 3 x 2
##    Category     total_books
##     <chr>        <int>
## 1  "college"      793
## 2 "competition"   872
## 3   school"       1990
Thus, it is clear that 'school'category books are most selled for the years 2018 & 2019.
