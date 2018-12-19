# Rental Listing Inquiries Prediction

For this project I worked on a Kaggle competition for Two Sigma’s portfolio company RentHop. Full walk-trough with code can be found in the **Rental_Listing_Inquiries_Prediction.pdf** document.

## Overview:  

Data provided is divided in train and test sets, with 49,352 entries and 74,659 entries
respectively. There is a total of 14 features (columns) and the target variable: ‘high’, ‘medium’, or ‘low’ inquiries. My goal was to build a model to predict number of inquiries in test set. See below for data
description:

![pic1](https://github.com/PyAntony/Renthop-Inquiry-Prediction/blob/master/images1/pic1.png)

submission was evaluated using the muti-class logarithmic loss formula:

![pic2](https://github.com/PyAntony/Renthop-Inquiry-Prediction/blob/master/images1/pic2.png)

### Data Exploration 

Let’s review some plots I made to explore the data. Let’s start with the target distribution:

![pic3](https://github.com/PyAntony/Renthop-Inquiry-Prediction/blob/master/images1/pic3.png)

Now, let’s see the distribution of the interest levels in the number of bedrooms, bathrooms,
days and months:

![pic4](https://github.com/PyAntony/Renthop-Inquiry-Prediction/blob/master/images1/pic4.png)

Let’s explore price now:

![pic5](https://github.com/PyAntony/Renthop-Inquiry-Prediction/blob/master/images1/pic5.png)

Let’s find outliers in the price:

![pic6](https://github.com/PyAntony/Renthop-Inquiry-Prediction/blob/master/images2/pic6.png)

### Data Preparation

These are some steps I took to prepare the data:

- Encode (assign numbers) the ‘building_id’ and ‘manager_id’ features since
they contained numbers mixed with letters.

- Parse the ‘created’ (for date) feature into month, day, and hour to find out if there is any variance
explained by time difference. 

- Extract the length for text features. For ‘description’, I created a new feature called
‘description_lenght’, and for ‘features’ (things like doorman, elevator, fitness center, etc.) I created
‘features_num’, both indicating the number of words in the text. 

- As for text, I decided to do the same with the number of photos. I created the feature ‘photos_num’.

- Next, I had to do something with ‘building_id’ and ‘manager_id’ beyond encoding. I ended up with
more than 1000 IDs per feature so I had the necessity to compress these categories into a more
manageable number (due to the number of dimensions). I used the frequency number of these IDs to
compress them into 116 and 150 categories respectively. 

- For addresses and location, I decided to work only with ’latitude’ and ‘longitude’.


### Model selection and Implementation

After running a quick and dirty Random Forest I realized how slow this endeavor was going to be (due to processing time), even after reducing many categories/features in the data preparation step. I decided to further reduce the data using the Random Forest feature selection technique and get only the top 10 features displayed here: 

![pic7](https://github.com/PyAntony/Renthop-Inquiry-Prediction/blob/master/images2/pic7.png)

I run 2 models: Random Forest again with Cross-Validation and Logistic Regression with/without GridSearch:

![pic8](https://github.com/PyAntony/Renthop-Inquiry-Prediction/blob/master/images2/pic8.png)
![pic9](https://github.com/PyAntony/Renthop-Inquiry-Prediction/blob/master/images2/pic9.png)
![pic10](https://github.com/PyAntony/Renthop-Inquiry-Prediction/blob/master/images2/pic10.png)  

### Conclusion

I wanted to try so many other things but I had to stop due to time constraints. It is extremely time consuming to test new features, new models, new ensembles, etc. (no wonder people always team up to win these competitions). I was satisfied with my “above-70%” accuracy, while not impressive by any standard, at least it indicated that I didn’t make any gross mistake and I was on the right path. I gained a solid understanding of the machine learning project process and I am sure, given a few more days, I would have been able to greatly improve my score.

All my respect to the top Kagglers, it is just and insane amount of work! :bow: 
