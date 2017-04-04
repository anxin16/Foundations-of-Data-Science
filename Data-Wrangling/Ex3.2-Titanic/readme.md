### Load the data in RStudio
titanic_df <- read.csv("F:/Online Courses/SpringBoard/Foundations of Data Science/Exercise3.2/titanic_original.csv")

### 1: Port of embarkation
titanic_df$embarked[is.na(titanic_df$embarked)] <- "S"

### 2: Age
avg <- mean(titanic_df$age, na.rm = TRUE)  
titanic_df$age[is.na(titanic_df$age)] <- avg

### 3: Lifeboat
titanic_df$boat[titanic_df$boat == ""] <- NA

### 4: Cabin
titanic_df$cabin[titanic_df$cabin == ""] <- NA  
titanic_df$has_cabin_number <- as.numeric(!is.na(titanic_df$cabin))  
titanic_df$cabin[is.na(titanic_df$cabin)] <- ""

### 5: Submit the project
write.csv(titanic_df, "F:/Online Courses/SpringBoard/Foundations of Data Science/Exercise3.2/titanic_clean.csv")
