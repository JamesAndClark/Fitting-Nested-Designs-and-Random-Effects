# Fitting-Nested-Designs-and-Random-Effects
When a variable is nested in the dataset, not much needs to be done. But if a nested variable is not properly set up in a dataset, it has to be set up in R.

# Nested in r with a random effect
fungi <- read.csv("fungal_spores.csv")  
fungi$slide <- as.factor(fungi$slide)  
fungi$temperature <- as.factor(fungi$temperature)  
fungi$location <- as.factor(fungi$location)  
fit1 <- aov(percent_spores ~ temperature + Error(temperature:slide), data=fungi)  
summary(fit1)  
The use of the Error() function allows us to not only nest slide within temperature, but it also lets us code it as a random effect.  

# Nested in CSV with a random effect
Here is an alternative dataset which has nested variables specified in its csv. This allows us to avoid the use of aov and Error. Instead we can use a linear mixed effects model.  

surch <- read.csv("seaurchin.csv")  
library(nlme) // This is the package that uses linear mixed effects  
fit2 <- lme(algae ~ treat, random = ~ 1 | patch,  data=surch) // The tilda 1 | Patch allows us to code patch as a random effect.  
summary(fit2)  
In this model, we do not need to specify whether the treat variable or patch variable is nested, as it is done so within the dataset.  
Since we use a random effect, we analyse our residual variances rather than looking at our F or P-values.  
