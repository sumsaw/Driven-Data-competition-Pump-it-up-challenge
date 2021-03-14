# Driven-Data-competition-Pump-it-up-challenge
A multiclass classification problem to predict functional and non-functional pumps . I tacked this using Gradient boosting techniques

I love working on driven data competition and dataset as they always have a environmental and  societal  spin towards their competition. This competition was one such. It was a 
tabular competition which are becoming rare . 

# About the competition<br>
Can you predict which water pumps are faulty?

Using data from Taarifa and the Tanzanian Ministry of Water, can you predict which pumps are functional, which need some repairs, and which don't work at all? This is an intermediate-level practice competition. Predict one of these three classes based on a number of variables about what kind of pump is operating, when it was installed, and how it is managed. A smart understanding of which waterpoints will fail can improve maintenance operations and ensure that clean, potable water is available to communities across Tanzania.

# Running the file 
- The above notebook can be run by using the copy and edit option in my Kaggle notebook:https://www.kaggle.com/sumeetsawant/pump-it-up-driven-data-competition 

# Description of the dataset 
This dataset was a mix of catergorical and numerical variables. I did some EDA in my kaggle notebook and I am listing the main observation from it . Below are the columns and what they are

### Data Description 
Your goal is to predict the operating condition of a waterpoint for each record in the dataset. You are provided the following set of information about the waterpoints:

1.  **amount_tsh** - Total static head (amount water available to waterpoint)<br>
2. **date_recorded**- The date the row was entered <br>
3. **funder** - Who funded the well <br>
4. **gps_height** - Altitude of the well<br>
5. **installer** - Organization that installed the well<br>
6. **longitude** - GPS coordinate <br>
7. **latitude** - GPS coordinate<br>
8. **wpt_name** - Name of the waterpoint if there is one<br>
9. **num_private** -is it private <br>
10. **basin** - Geographic water basin<br>
11. **subvillage** - Geographic location<br>
12. **region** - Geographic location<br>
13. **region_code** - Geographic location (coded)<br>
14. **district_code** - Geographic location (coded)<br>
15. **lga** - Geographic location<br>
16. **ward** - Geographic location<br>
17. **population** - Population around the well<br>
18. **public_meeting**- True/False<br>
19. **recorded_by** - Group entering this row of data<br>
20. **scheme_management** - Who operates the waterpoint<br>
21. **scheme_name**- Who operates the waterpoint<br>
22. **permit**- If the waterpoint is permitted<br>
23. **construction_year** - Year the waterpoint was constructed<br>
24. **extraction_type** - The kind of extraction the waterpoint uses<br>
25. **extraction_type_group** - The kind of extraction the waterpoint uses<br>
26. **extraction_type_class**- The kind of extraction the waterpoint uses<br>
27. **management**- How the waterpoint is managed<br>
28. **management_group** - How the waterpoint is managed<br>
29. **payment** - What the water costs<br>
30. **payment_type** - What the water costs<br>
31. **water_quality** - The quality of the water<br>
32. **quality_group** - The quality of the water<br>
33. **quantity** - The quantity of water<br>
34. **quantity_group** - The quantity of water<br>
35. **source**- The source of the water<br>
36. **source_type** - The source of the water<br>
37. **source_class** - The source of the water<br>
38. **waterpoint_type** - The kind of waterpoint<br>
39. **waterpoint_type_group** - The kind of waterpoint<br>

I performed some EDA on this dataset . But below is the summary of my findings.  I went through each column in the dataset and saw many columns where repeated . So between two columns of the same type one catergorical column will have more levels than the other.  

### Some points to consider 

1. Plotting latitude vs longtitude vs basin/ region we see that both point to the same feature . So taking region feature as it has more categories 

2. Imputing points outside the area of Tanzania with the mean of the latitude and longitute column 

3. Reducing the number of levels in scheme managment 

4. All null values for Funder and installer are occuring together with the recording year being 2011

5. Lot of construction year is missing 

6. basin,region and region code are the same things 

7. lga ( local government authority),ward and subvillage are just smaller unit of admistration 

8. waterpoint_type_group and waterpoint_type columns are identical so one can be dropped 

9.  source type ,source and source class are the same , One has more distinction/sub-division

10. payment and payment_type is the same column .  

11. extraction and extraction_type_group and extraction_type_class are similar

12. water quality and quality_group are also similar 

13. quantity and quantity group are also similar 

14. managment and managment group also the same columns

# Key Insights gained 
- I was able to try out Gradient boosting model ( namely XGboost and Light GBM) 
-Taking care of data-leakage so as to have tight control over CV as the data points provided where less . Was able to get close Public and Private LB scores 
-Successfully handle curse of dimensionality by removing duplicate columns and also columns which had the same data in a different form .
-Used random seed to create multiple model 
-Successfully used RandomSearchCV and Optuna to for hyper-parameter tuning. 
-Created new features and checked their importance using mutual info classif from sklearn library.

# Competition model 
- I used a ensemble of XGboost and Light GBM  15 models each. Both the model was hyper-parameter tuned. I used five fold validation so in totoal 15*5*2=150 models .
The difference between various models was its initiation using different random seed . After this I used hard voting to select the final class. 

# Final Submission 
My final submission accuracy score was 0.8147 on private test set . I was able to increase the score from 0.78 to 0.80 to 0.8147. The competition 1st rank was at 
0.8294 at the time of writing this repo. 
