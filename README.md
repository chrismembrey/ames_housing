# Analysing Investment potential using Regression and Classification with the Ames Housing Data

![cover](https://user-images.githubusercontent.com/76961031/118164116-a1b3da00-b41a-11eb-86da-3539191a3fa7.jpeg)

A two week project that aimed to determine which non-renovatable features had the highest impact in house price (for renovatable investment) and to predict which houses had abnormal sales so that a company may be able to detect a better deal on housing. 

The dataset ca be found on kaggle, with a data dictionary of all the variables: https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data
---

## Table of Contents
- [Introduction](#introduction)
- [Part 1 - Estimating the value of homes from fixed characteristics](#Part-1---Estimating-the-value-of-homes-from-fixed-characteristics)
- [Part 2 - Determine any value of changeable property characteristics unexplained by the fixed ones](#Part-2---Determine-any-value-of-changeable-property-characteristics-unexplained-by-the-fixed-ones)
- [Part 3 - What property characteristics predict an "abnormal" sale?](#Part-3---What-property-characteristics-predict-an-"abnormal"-sale?)

---
## Introduction

In this project I'm trying to make a relevent business case out of the Ames dataset. Housing data such as this could be used by companies or individuals who invest in real estate to determine cost implications of renovations. The first part of the study aims to create a model that can accuratley predict the sale price of residential property and identify the fixed features (features that would require a planning consent to renovate) that have the greatest effect on the sale price. The using I will use the renovatable features of property to see how much of the variance left in the sale price from the first model can be explained by these features (and again see which renovatable features have the highest impact on the explaied variance). The final part of the project aims to identify the features of a property that lead to an abnormal sale.

Below are the conclusions for each part, for a deeper insight into the dataset (cleaning & EDA as well as a few extra models), please feel free to read the jupiter notebook attached to this readme.

## Part 1 - Estimating the value of homes from fixed characteristics

To gauge how expencive a property will initially be, we need to predict the sales price using the fixed features only. We can also use this model for cost implications of major renovations.

Here are the results for the linear regresion models ran. The index represents the degree of polynomiality for one of the features (year the house was built). As you can see a third degree of polynomiality in a ridge regression has the highest r2 score and thus, is the best model.

<img width="738" alt="Screenshot 2021-05-13 at 21 14 33" src="https://user-images.githubusercontent.com/76961031/118182220-a3889800-b430-11eb-9d8b-0c052400f6c7.png">

Here are the coefficients and thier graphical representation.

<img width="296" alt="Screenshot 2021-05-13 at 21 04 19" src="https://user-images.githubusercontent.com/76961031/118181229-68d23000-b42f-11eb-8df7-bd613ad0faa7.png">

<img width="630" alt="Screenshot 2021-05-13 at 21 03 04" src="https://user-images.githubusercontent.com/76961031/118181302-830c0e00-b42f-11eb-8810-0b5cebce74d7.png">


Below you can see the unit values representing the change in the sales price when a feature is increased by one. This is naturally higher for binary variables such as is the property in neighborhood NoRidge (Northridge).

<img width="373" alt="Screenshot 2021-05-13 at 21 03 56" src="https://user-images.githubusercontent.com/76961031/118181240-6c65b700-b42f-11eb-965e-35fabc6f3025.png">

## Part 2 - Determine any value of changeable property characteristics unexplained by the fixed ones

By looking at the renovatable features in this way, we can see the effect of them on the sales price compared to the fixed as a whole unit compared to lots of individual renovatable features. However, this does also highlight which individual features have the highest impact on sales price ad by looking at the coefficients of the features, a building company/investment company can decide how to ameliorate the asset value. 

Using the model from the ridge regression from part 1, you can see below how 16% of the variability in the sales price can be explained by the renovatable features.

<img width="354" alt="Screenshot 2021-05-13 at 21 29 01" src="https://user-images.githubusercontent.com/76961031/118183668-455cb480-b432-11eb-873c-26839ecfb2b3.png">

Here are the features that have the highest impact on the sales price (given the impact is a positive one, for example having a fireplace will increase the value of the house).

<img width="470" alt="Screenshot 2021-05-13 at 21 27 48" src="https://user-images.githubusercontent.com/76961031/118183697-50174980-b432-11eb-9011-5064213f65f9.png">

Here we are taking into account variables that have a negative effect on sales price as well as a positive effect (shown by the negative and positive coefficients).

<img width="446" alt="Screenshot 2021-05-13 at 21 27 58" src="https://user-images.githubusercontent.com/76961031/118183723-57d6ee00-b432-11eb-9d0d-99f501bba871.png">

## Part 3 - What property characteristics predict an "abnormal" sale?

An example of an abnormal sale for this dataset is a foreclosure (failing to keep up with mortgage payments, causing the mortgagor to have thier property taken) or short sale (investing such that the asset fails). By predicting whether a house could be under this bracket, investors will be able to make money by preventing the features that cause abnormal sales in thier won properties or by investing in short sales of other companies real estate. 

Here is the performance table of the models ran. Its important to note hat the class imbalance was so servere (93%) that SMOTE oversampling had to be used in the preprocessing stages.

![Screenshot 2021-05-14 at 08 26 29](https://user-images.githubusercontent.com/76961031/118236526-16742c00-b48e-11eb-99ca-942b9c75bacb.png)

The top features for the ridge model are below, the greater the value of x (the coefficient for that variable), the greater the impact it has in determining a property as abnormal. From the graph we can see the best predictor for an abnormal sale is the sale type. A newly built house is less likely to be sold in an abnormal condition. Houses without a masonary veneer are also less likely to be sold under abnormal conditions.

![Screenshot 2021-05-14 at 08 25 57](https://user-images.githubusercontent.com/76961031/118236466-03f9f280-b48e-11eb-8c1f-751ac1433dee.png)


The ideally we would want increased precision, limiting the number of false positives to make the safest investments. Here is the classification report for the ridge regression, showing the precision and recall, and the confusion matrix which breaks down how the model predicted each class.

![Screenshot 2021-05-14 at 13 38 11](https://user-images.githubusercontent.com/76961031/118272204-2c97e180-b4ba-11eb-94f7-4cd1f691b977.png)

![Screenshot 2021-05-14 at 13 22 36](https://user-images.githubusercontent.com/76961031/118272213-2f92d200-b4ba-11eb-97fc-17f96d56e95c.png)








