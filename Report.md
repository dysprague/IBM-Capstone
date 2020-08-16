### Business Problem

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
1 indicating the least impact on traffic and 4 indicating the greatest impact on traffic. In pre-processing
the data I decided to remove and alter a number of variables. The multitude of location information was
condensed down to just city and county, as the local level would probably provide the most informaiton;
TMC code and distance of accident were removed as they would not be helpful in predicting the severity
of a future crash. Time data was condensed into the duration of the accident and whether it took place
during night or day based on astronomical twilight. The attributes were then converted into the proper
data formats, and NaN values were either replaced by mode for categorical variables or mean for continuous
variables. The final processed dataset now has 26 columns, 25 features and 1 target variable. The final features
now include the side the car was hit on, the city and county of the accident, weather features like temperature 
and visibility, the duration of the accident, and road features present or involved in the accident.
