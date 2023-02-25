# Milestone II Project: Predicting Prices of Airbnb Listings in the Western United States

Full report: https://docs.google.com/document/d/1Hrtkn64zvmSz0Vtb6gIQu9Y-JyxLLlTljwzNvWA87bU/edit?usp=sharing

## I. Introduction
### I.I Predicting the price of a short-term rental unit

Airbnb, founded in 2008, has grown to become one of the most popular platforms for short-term rentals worldwide. With over six million listings, it is estimated that Airbnb holds approximately 20% of the market share in the short-term rental industry (source: Search Logistics).

This project explores the creation of a predictive pricing model. The pricing of a home, whether for rental or ownership, is influenced by a multitude of factors, which is a fascinating topic to me. In pursuit of this project, I curated a dataset of 180,000 listings from Airbnb.com. The objectives of this research project are two-fold: (1) to develop a model that accurately predicts the optimal pricing of a short-term rental unit and (2) to identify the most significant factors that impact pricing.

#### Potential impacts of work
* Create a model that allows short-term rental listing owners to maximize their potential revenue from a property.
* Determine the factors that have the most influence on increasing the nightly price of a short-term rental property.


### I.III Solution Approach
To develop a solution for this project, I implemented the following steps:


* First, I created a web scraper to extract 180,000 U.S. rental listings from Airbnb.com, spanning from the California coast to the Colorado-Kansas border. I subsequently merged this data with county- and state-level statistics pertaining to the community surrounding each listing.
* Next, I engineered three categories of additional variables, which included distance to tourist destinations, image quality analytics on the first five photos of each listing, and one-hot encoding of common unigrams from the description. Furthermore, I conducted unsupervised learning to generate reduced principal components and clustered labels for features.
* Finally, I performed a search across multiple supervised learning methods, including linear- and tree-based models, to identify a model that maximizes the R-Squared score while minimizing the Mean Absolute Error.


### I.IV Executive summary of findings
The final supervised regression model, a tuned XGBoost Regression model, effectively delivers a pricing model that predicts the nightly rate for Airbnb listings (see Visual B). Over a 5-fold validation, this model has an R-Squared score of 0.730, a mean absolute error of $51.72, and an RMSE of $77.51. For a pricing prediction model on an open marketplace, this performance should be regarded as robust. In my research, most models I could find delivered R-Squared scores ranging from 0.5 to 0.6. Some models reach 0.7, but these were trained on a single city; my model was trained on 1.17 million square miles' worth of data.

However, the pricing errors tend to increase as listings become more expensive, with a tendency to underpredict the price. The model is not capturing something about the value of pricier listings (those priced at $450+/night). Additionally, some listings appear to have incorrect data, with discrepancies between the listed bedroom and bathroom counts and the information provided in the listing's description.

Based on ablation studies, it was discovered that some of the most influential features for explaining pricing variance are not the listing's attributes themselves, but rather its location in relation to tourist destinations. This observation was reinforced by the strong and interpretable principle components that were derived from geolocation data in the unsupervised portion of the project.

### I.V Future work

I have a hypothesis that the R-Squared score of this model could be improved if I found a way to capture features that describe the value of higher priced listings. There are a few future avenues that could be pursued to explore this.
* Image data: some rudimentary image analytics were conducted in the feature engineering portion of this project, but image classification could help identify higher quality listings. Data scientists at Airbnb have explored object detection in listing images, while other researchers have explored more custom algorithms that classify the luxury level of an image. Other papers have explored extracting data on how verified images influence earnings. 
* Handling luxury listings: higher priced luxury listings have slightly different pages than standard Airbnb listings. This suggests opportunities for web scraping to identify additional features and signals from the webpage that help a model reduce underpricing errors.
