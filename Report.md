### Introduction

Car accidents are one of the leading causes of death in the United States and cause billions of dollars in damages. 
This creates significant incentives for car developers and politicians to understand the factors that 
affect whether an accident will occur and how sever the accident may be. It is important to 
not only be able to predict the severity of an accident, but also to evaluate which factors most strongly 
lead to a more severe accident. This will allow car manufactures to better determine what 
safety features to include or update in new car models and allow policy makers to better 
determine what changes should be made to traffic laws/patterns and road infrastructure. For example,
if more accidents occur at night, then cities should invest in more street lights. If more accidents 
happen in cold weather, then perhaps car manufacturers should invest in better windshield defogging
or anti-slick technologies. An analytical model using data science will not instantly tell us
exactly what solutions will be necessary or effective, but it can certainly help us isolate what 
factors would be most effective to intervene on.

### Data

The dataset is taken from Kaggle and contains countrywide traffic accident data from 49 states
in the US form February 2016 to March 2019. The dataset has about 2.24 million entries and 49
attributes. Attributes include weather conditions, location, time of day, road features, and a 
variety of other accident features. The target variable is severity: a number between 1 and 4 with 
1 indicating the least impact on traffic and 4 indicating the greatest impact on traffic. The attributes
are of all different data types: some strings, some ints, some floats, and some booleans. 

### Methodology

In pre-processing the data I decided to remove and alter a number of variables. The multitude of location information was
condensed down to just the latitude and longitude, as continuous variables would be easier to model than categorical;
TMC code and distance of accident were removed as they would not be helpful in predicting the severity
of a future crash. Time data was condensed into the duration of the accident and whether it took place
during night or day based on astronomical twilight. The attributes were then converted into the proper
data formats, and NaN values were either replaced by mode for categorical variables or mean for continuous
variables. The final processed dataset now has 23 columns, 22 features and 1 target variable. The final features
now include the side the car was hit on, the longitude and latitude of the accident, weather features like temperature 
and visibility, the duration of the accident, and road features present or involved in the accident. The longitude 
and latitude values were also visualized with case severity on a map of the US.

I decided to use a random forest algorithm to analyze the data. Random forests are great for this type of data 
because they are highly interpretable, can work with both continuous and discrete variables, and work well with
a large number of attributes. The data set was split into training, testing, and validation sets to allow for training,
hyper parameter tuning, and testing for generalizability.

### Results

Using the random forest algorithm, I was able to achieve 52.3% testing accuracy. While this does not seem particularly high,
it is actually significantly better than baseline since there are 4 possible values for the target variable. Furthermore,
looking at the confusion matrix shows that even when the algorithm gets values wrong, it rarely gets it very wrong. When an 
accident is a 1, there is a 98% chance that the algorithm predicts it as a 1. If an accident is a 2, there is a 50% chance 
the algorithm predicts it as a 2, but an 85% chance it is predicted between 1 and 3. If an accident is a 3, there is a 54%
chance the algorithm predicts it as a 3, but a 94% chance it is predicted between 2 and 4. For 4, there is an 85% chance it is 
predicted as either a 3 or 4. This means that the accuracy is not perfect, but the algorithm does a good job of predicting 
whether an accident will have a low or high severity. 

The random forest algorithm also allows for easily evaluation of feature importance. The most important features were the
starting longitude and latitude. This makes sense because geographic region will certainly play a large role in the commonality
of severe accidents. It seems from our initial visualization that regions of high population density (the coasts) tend to have 
higher severity. The next most important features have to do with weather conditions. Oddly, pressure, humidity, and temperature
are the biggest predictors. This may be becase they are better proxies for things like road conditions that could cause accidents
than precipitation in inches or even visibility. The most common road features that predict accident severity are traffic signals and
crossings. This makes sense as intersections where many cars interact are likely to be locations of larger accidents. Strangely, the time
of day did not seem to be an especially high predictor of accident severity. 

### Discussion

The results of this research do not necessarily give clear solutions that would certainly reduce accident severity, but they certainly 
do give an indication for what factors most influence severity. It seems that the largest predictor is location. Certain cities and regions,
likely the more densely populated ones, are more likely to have severe accidents. The more actionable factors are likely the weather conditions 
and road features. Lower pressure seems to be correlated with increased severity of accidents. This liekly correlates with more extreme weather 
conditions. Part of the problem is that for almost attribute there is accidents of all severities across the whole range of values.
This makes it difficult to get clear recommendations for actionable items; especially because it is already well known that more severe weather 
leads to more severe accidents. More research should be done into how pressure affects driving conditions independent of other factors like
temperature and precipiation. Traffic signals and crossings also seem to be predictors of more severe accidents. This means city planners should
try to minimize these intersections or implement better policies for prevcenting accidents at these intersections.

### Conclusion

From the results of this analysis, it seems clear that it is fairly to distinguish between a low severity accident and a higher severity one. However
it is much more difficult to predict the relative severity of the more severe accidents. This is likely because the severity of an accident has as much
to do with individual human error as it does with environmental conditions. There is not much use in simply predicting the severity of an accident if it
does not tell us what we can do to reduce the severity of future accidents. Our analysis has shown that weather conditions and location are the largest
predictors of accident severity. This means that policymakers should look at the road and climate conditions in their specific region and further identify
what areas are the most problematic. This would allow them to isolate areas within their cities that are most vulnerable to changes in road conditions
and try to fortify them against changing weather. 
