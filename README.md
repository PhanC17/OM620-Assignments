# OM620-Assignments

Assignment repository for use in the Tools and Techs for Analytics class (OM 620) in CSUSM. Includes the nootebooks and data files used for the assignments.

## Safety Stock Assignment
The first two assignments of the class focused on practicing data cleaning and transformation given a random data set.

For these assignments, the context was in the field of inventory management. Specifically, each group was given a puchase history of inventory items which includes information about their manufacturing and order quantities. The goal of these two assignments was to determine the safety stock level for inventory items (SKUs) that are *made-to-stock* (MTS).

### Data Cleaning
For the data cleaning portion, we made sure that the columns of the data had the same naming convention and looked for any anomalies and missing values in the data. In our data, there were two types of anomalies that needed to be fixed.

The first type was negative values in the order quantity and unit price columns. This was impossible, especially as the data does not include any information about potential returns. So the absolute value of these values were taken to make them positive values.

The second type was unreasonably high values in the lead time column. When looking at the anomalous values, they appeared to be the other lead time values but multiplied by 100, Dividing those values by 100 was a quick fix to address that.

When looking for missing values, we saw that the data set only had missing values in the categorical data columns (i.e. manufacturing site, stock type). They were too numerous to consider removing, especially with multiple lines missing multiple values. If we removed data missing any or some categorical data, we would've lost the numerical data that we wanted to work with. So the decision was made to replace the missing values with an "Unknown" category so that we weren't missing any data for later.

### Data Transformation
With our data properly cleaned up, we could start working on looking for the safety stock levels. We started by filtering the data set so that we were only looking at items that are MTS, which was the focus of the assignments.

From there, we aggregated the SKUs by the descriptive statistics of their respective order quantity (minimum, maximum, average, median, variance, and standard deviation) and the average lead time. This transformed data allowed us to better see the data spread for each SKU.

We then calculated the safety stock level for each SKU using the following formula:
#### SS = z<sub>α</sub> * σ<sub>D</sub> * √L

where assuming a normal distribution of quantity demand, **z<sub>α</sub>** is the z-score of the service level coefficient **α**, which is the probability of satisfying an order, **σ<sub>D</sub>** is the standard deviation of the demand, and **L** is the lead time.

We created new columns to find the safety stock levels of each SKUs at three service level coefficients: 75%, 90%, and 95%. Each column uses the quantity standard deviation and the average lead time for the respective SKU plugged into the above formula. That way, in combination with the z-score that can be found on a z-table, we can easily calculate the safety stock levels for the MTS SKUs at three different service levels.