# Exploring the Dynamics of Real Estate Prices: An Analytical Case Study

## Executive Summary
With the data received, I looked for key insights into real estate investment using exploratory data analysis. Our findings reveal that real estate prices are influenced by age, proximity to transit, and availability of local amenities. Data analysis suggests varying degrees of correlations between these factors and property prices, with locations having minimal influence on the price. Stakeholders could benefit from our findings through a better understanding of market dynamics to guide investment and development decisions.

## Introduction and Background
- The real estate business is constantly growing.
- There is a growing interest in understanding what drives real estate prices.
- I analyzed a dataset containing information on house prices, age, proximity to MRT stations, and local amenities.
- unveiling patterns and trends could provide some actionable insights into these dynamics of real estate to buyers/sellers.
![image](https://github.com/OnonaChukwu/Real-estate/assets/155753951/57314ef8-f8e1-4c0d-8fe2-f63e3081253f)


## Challenge and Motivation
- Challenges include diverse factors influencing property prices, making predictions complex.
- The motivation for this study is to provide insights for stakeholders in the real estate market
- And to enhance the decision-making process for non-experts exploring the market in general.

## Aim and Objectives
**Aim**
- Elucidate the relationship between real estate prices and certain key factors.

**Objectives**
- Identify how age influences house prices.
- Identify how proximity to MRT affects market prices.
- Evaluate the influence of convenience stores on real estate prices.
- Identify how locations affect house prices.

## Hypothesis and Research Questions
- Do older houses have lower prices than newer ones?
- Are houses closer to MRT stations priced higher?
- Do nearby convenience stores positively impact house prices?
- Are property prices per unit area influenced by geographical location?

## Methodology
- Dataset from the “real estate within range” dataset was sourced.
- Data cleaning was done using Excel; outliers and missing values.
- Regression analysis was used to explore correlations between house prices and factors.
- For location vs. price analysis, “OLS Regression” was applied for a detailed look at the involved factors.

## Python Code Snippets for Data Analysis
```python
# Exploring the relationships between 'house price of unit area' and house age
import statsmodels.api as sm

# Prepare the data for modeling, add a constant to the independent variable to include the intercept in the model
X = sm.add_constant(real_estate_data['house age'])  # Independent variable
y = real_estate_data['house price of unit area']  # Dependent variable

# Fit the linear regression model
model = sm.OLS(y, X).fit()

# Get the R-squared value from the model's summary
print("R-squared value:", model.rsquared)

# Setting up the aesthetics for the scatterplots that will dtect relationship 
sns.set_style("whitegrid")

# Continue with graph plotting as in visualising
plt.figure(figsize=(30, 6))
plt.subplot(1, 2, 1)
sns.scatterplot(x='house age', y='house price of unit area', data=real_estate_data)
plt.title('House Age vs. Price')

# Display the R-squared value on the plot
plt.text(0.05, 0.95, f'R²: {model.rsquared:.2f}', transform=plt.gca().transAxes)


import folium

# Create a base map
mean_lat = real_estate_data['latitude'].mean()
mean_lon = real_estate_data['longitude'].mean()
map = folium.Map(location=[mean_lat, mean_lon], zoom_start=12)

# Plot each house as a circle marker
for idx, row in real_estate_data.iterrows():
    folium.CircleMarker(
        location=[row['latitude'], row['longitude']],
        radius=5,  # fixed radius for all markers
        fill=True,
        fill_color='blue' if row['house price of unit area'] < real_estate_data['house price of unit area'].median() else 'red',
        color=None,
        fill_opacity=0.7,
        popup=f"Price: {row['house price of unit area']}"
    ).add_to(map)

# Display the map
map


# Statistical analysis of the map co-ordinates
import statsmodels.api as sm

# Prepare the data for regression
X = real_estate_data[['latitude', 'longitude']]
X = sm.add_constant(X)  # adding a constant for the intercept
y = real_estate_data['house price of unit area']

# Fit the regression model
model = sm.OLS(y, X).fit()

# Print the summary of the regression
print(model.summary())

```

## [Results and Interpretations](https://public.tableau.com/app/profile/charles.ikenna.nwankwo/viz/Realestate_17133071929110/HouseAgevsPrice)

- **House Age vs. Price** shows a weak inverse correlation; older houses do not necessarily mean lower prices.
![image](https://github.com/OnonaChukwu/Real-estate/assets/155753951/43323dea-63b6-4812-bb35-de6c64dd4a92)

- **Proximity to MRT vs. Price** check shows a positive but weak correlation; closer houses to MRT tend to be slightly more expensive.
![image](https://github.com/OnonaChukwu/Real-estate/assets/155753951/bce26305-f280-48f5-8edc-40822c9177c8)

- **Convenience Stores vs. Price** comparison reveals a positive impact; more stores nearby slightly correlate with higher prices.
![image](https://github.com/OnonaChukwu/Real-estate/assets/155753951/438bd1b5-ae9b-4310-88bc-c162d99b51ac)

- **Geographic Coordinates vs. House Price** shows tha location, by itself, doesn't tell us much about the price; other factors have more effect.
![image](https://github.com/OnonaChukwu/Real-estate/assets/155753951/1c6e0a76-6dda-42fd-988b-271415160aaa)

## Conclusions and Recommendations
- Factors impact prices, but correlations are generally weak, suggesting complex interdependencies.
- Recommendations for investors include considering properties near MRT stations despite the weak correlation;
  - they may offer better long-term values. 
- Policymakers are encouraged to develop amenities in residential areas to potentially boost property values.
