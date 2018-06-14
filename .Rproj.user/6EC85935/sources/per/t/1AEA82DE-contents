# Code by Olof Rännbäck-Garpinger 20180614, Knightec AB

# Install the tidyverse packages unless you already have: install.packages("tidyverse")

# To run code, select one or several lines of code and press "Ctrl + Enter" 


# Load the tidyverse packages
library(tidyverse)

### readr ###

# Load dataset using read_csv from readr, producing a data frame (called tibble)
train = read_csv("train_users_2.csv")

# Print data frame
train


### Data manipulation with dplyr ### 

# Choose columns with select
train_selected = select(train, id, timestamp_first_active, age, gender)
train_selected

# Sort rows with arrange
arrange(train_selected, age)

train_arranged = arrange(train_selected, desc(age))
train_arranged

# Pick rows by values with filter
train_filtered = filter(train_arranged, age < 120)
train_filtered

# Transform and create new variables with mutate
library(lubridate) # load lubridate package for time related functions
train_mutated = mutate(train_filtered,
                      timestamp_first_active = ymd_hms(timestamp_first_active))
train_mutated

# Calculations over groups using group_by and summarise
train_group_by = group_by(train_mutated, gender)
train_summarised = summarise(train_group_by,
                            mean_age = mean(age),
                            count = n())
train_summarised


### Visualizations with ggplot2 ###

# ggplot(data = <DATA>) +
#  <GEOM_FUNCTION>(
#    mapping = aes(<MAPPINGS>)
#  )

# Histogram over user age
ggplot(data = train_filtered) +
  geom_histogram(aes(x = age), binwidth = 1)

# Frequency polygons instead of stacked histograms when splitting up in categories
ggplot(data = train_filtered) +
  geom_freqpoly(aes(x = age, color = gender), 
                lwd = 1.5,
                binwidth = 1)




# Bonus for those interested: #

### Pipelining with the pipe %>% ###

# Short command for %>% is: "Ctrl + Shift + M"

# Pipeline the above dplyr chain of events
train %>% 
  select(id, date_account_created, timestamp_first_active, age, gender) %>% 
  arrange(desc(age)) %>% 
  filter(age < 120) %>% 
  mutate(timestamp_first_active = ymd_hms(timestamp_first_active)) %>% 
  group_by(gender) %>% 
  summarise(mean_age = mean(age),
            count = n())

### ggplot2 ###

# Subplots with facet_wrap
ggplot(data = train_filtered) +
  geom_histogram(aes(x = age), binwidth = 1) +
  facet_wrap( ~ gender)

# The same plot written differently
train_filtered %>% 
  ggplot() +
  geom_histogram(aes(age), binwidth = 1) +
  facet_wrap( ~ gender)




