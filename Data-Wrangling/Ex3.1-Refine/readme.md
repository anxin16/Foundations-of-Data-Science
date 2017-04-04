### Install packages
install.packages("dplyr")  
install.packages("tidyr")  
library(dplyr)  
library(tidyr)  

### Load the data in RStudio
refine_df <- read.csv("F:/Online Courses/SpringBoard/Foundations of Data Science/Exercise3.1/refine_original.csv")

### Clean up brand names
refine_df$company <- tolower(refine_df$company)  
idp <- agrep(pattern = "phillips", x = refine_df$company, ignore.case = FALSE, value = FALSE, max.distance = 2)   
refine_df$company[idp] <- "phillips"  
ida <- agrep(pattern = "akzo", x = refine_df$company, ignore.case = FALSE, value = FALSE, max.distance = 2)   
refine_df$company[ida] <- "akzo"  
idv <- agrep(pattern = "van houten", x = refine_df$company, ignore.case = FALSE, value = FALSE, max.distance = 2)   
refine_df$company[idv] <- "van houten"  
idu <- agrep(pattern = "unilever", x = refine_df$company, ignore.case = FALSE, value = FALSE, max.distance = 2)   
refine_df$company[idu] <- "unilever"  

### Separate product code and number
refine_df <- separate(refine_df, Product.code...number, c("product_code", "product_number"), sep = "-", remove = FALSE)

### Add product categories
lut <- c("p" = "Smartphone", "v" = "TV", "x" = "Laptop", "q" = "Tablet")  
refine_df$product_category <- lut[refine_df$product_code]  

### Add full address for geocoding
refine_df <- unite(refine_df, full_address, address, city, country, sep = ", ", remove = FALSE)

### Create dummy variables for company and product category
refine_df$company_philips <- as.numeric(refine_df$company == "phillips")  
refine_df$company_akzo <- as.numeric(refine_df$company == "akzo")  
refine_df$company_van_houten <- as.numeric(refine_df$company == "van houten")  
refine_df$company_unilever <- as.numeric(refine_df$company == "unilever")  
refine_df$product_smartphone <- as.numeric(refine_df$product_category == "Smartphone")  
refine_df$product_tv <- as.numeric(refine_df$product_category == "TV")  
refine_df$product_laptop <- as.numeric(refine_df$product_category == "Laptop")  
refine_df$product_tablet <- as.numeric(refine_df$product_category == "Tablet")

### Submit the project
write.csv(refine_df, "F:/Online Courses/SpringBoard/Foundations of Data Science/Exercise3.1/refine_clean.csv")
