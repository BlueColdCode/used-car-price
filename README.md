Create a used car price prediction model

This exercise aimed to apply CRISP-DM process to analyze and create prediction model
based on car sales historic records.

Business impact

Providing accurate prices to used cars can expedite business transactions,
and guarantee fairness to both business owners and customers. 

Technical challenge

There are many factors and the car's own features that determine the
sale price of a used car. Based on the transactional data collected on historical car
sales from different regions, we are expect to build a car sale price prediction model
to accurately reflect the true value of a used car.

Data cleaning

There are 18 columns of features in each record. Each column needed careful scrutiny,
selection, modification:

 - Some are irrelevant, such as ID and VIN, which can be dropped.
 - Many are nominal data, such as fuel, state, drive, which are
   to be transformed using OneHotEncoder.
 - Some are ordinal data, such as cylinders, condition, which are
   to be transformed using OrdinalEncoder.
 - There are also records that are missing critical information,
   and should be eliminated from the modeling, such as rows with
   NaN values, or price==0, or odometer==1.
 - EVs have no cylinders. Therefore, the cylinder value is turned
   to 0.
 - Cars costing more than 100,000 is not considered because
   of insufficient data above that range.
 - Cars that has 4 million miles odometer are considered outliers,
   and are removed as well.
 - The values of 'region' is 403, and there is no proper way of converting
   a value of 'region' into a numeric value, therefore it is dropped.
 - Similar to 'region', 'model' is also dropped.
 
 After adjusting the dataset according to the above analysis, we got to reduce the 
 number of records from 426880 to 76333, about 18% of the original dataset.
 
 Modeling
 
Through this CRIPS-DM exercise, we got to familiarize ourselves with the complete process of data mining, 
and realized the importance of data preprocessing before exploring regression models to fit the data.

According to similar results of two slightly different regression and prediction models, we confirmed
the validity and accuracy of each of the data analysis methods.

Going back to the original business drivers behind the data mining project, we can offer some valuable
guidance in considerations of used car features in the determination of their sale prices, which 
include the following items in the order of decending weight:

- odometer reading
- fuel type
- body type
- age/year of production
- number of cylinders
- drive
- condition

With this simplified view of the data, we rebuild the data model and estimation methods, hoping getting
a more accurate estimate of the car price.

Deployment

Out of the two models explored, gridsearch and pipeline2, we found that gridsearch model provides
lower MSEs in terms of the training data and the testing data. The parameters contained in the model
can be exported to the backend Python library hosted on webservers, and be presented to car dealers
with a simple API to get inputs regarding the critical parameters of the used car. According to the 
customer inputs, the model will output an estimated sale price as a reference for the dealer.

Of course, the used car sales also depend on supply and demand of the market, which was not modeled
in this exercise.
