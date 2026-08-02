# Average-temperature-VS-population-density-analysis
# The aim of this project was to analyse if avgerage temperatures are affected by population density in big cities. (Please download the csv files before running the code)

Project Aim

This project investigates the relationship between urban population density and average annual temperature across cities worldwide. By combining global urban population data with temperature observations, the analysis explores whether more densely populated urban areas tend to experience higher average temperatures. The project also examines whether transforming population density improves the interpretation of this relationship and highlights the influence of urbanisation on local climate patterns.

Methodology
Imported and cleaned global datasets containing city population density and average annual temperature.
Merged the datasets using common city identifiers to create a single analytical dataset.
Calculated population density metrics and applied logarithmic transformations to reduce the effect of extreme values.
Performed exploratory data analysis using scatter plots and descriptive statistics to identify overall trends.
Fitted linear regression models to quantify the relationship between temperature and population density.
Compared models using both raw and log-transformed population density to assess how data transformation affects the results.
Produced publication-quality visualisations illustrating the distribution of observations, fitted regression lines, and the overall relationship between urban density and temperature.
Interpreted the statistical results to evaluate whether population density is a significant predictor of average urban temperature and discussed the limitations of using a single explanatory variable.

RESULTS:
Scatter plots and Pearson correlation analysis were used to examine the relationship between population density and average temperature in urban areas for 1990, 2000 and 2015. The plots showed a weak positive relationship across all three years, meaning that areas with higher temperatures tended to have slightly higher population densities. However, the data points were widely spread out, suggesting that the relationship is not particularly strong. A number of highly populated cities also appeared as outliers, highlighting large differences between urban areas around the world.

The Pearson correlation coefficients were relatively low, indicating that average temperature alone is not a strong predictor of population density. Despite this, some of the p-values showed statistical significance, likely because of the large size of the dataset. The trend lines followed a similar pattern in all three years, suggesting that the relationship between temperature and population density remained fairly consistent over time.

Overall, the analysis suggests there may be a small association between warmer climates and higher urban population density, but the relationship is weak and is likely influenced by many other factors such as economic development, geography and infrastructure.

<img width="1983" height="590" alt="fig1" src="https://github.com/user-attachments/assets/7767a8a4-d85d-45da-a5a4-cf5a2d36a08d" />
Figure 1. Population Density versus Average Temperature (1990, 2000 and 2015).
Scatter plots showing the relationship between urban population density and average annual temperature for three time periods. The fitted regression lines indicate a weak positive relationship, with substantial variability across cities.

<img width="1984" height="590" alt="fig2" src="https://github.com/user-attachments/assets/d1b13a17-2405-4246-9f2e-cc67cee81948" />
Figure 2. Log-Transformed Population Density versus Average Temperature.
Scatter plots using logarithmic population density to reduce the influence of extremely dense cities. The transformation produces a more even distribution of observations while maintaining the overall weak positive trend.

<img width="1983" height="590" alt="fig3" src="https://github.com/user-attachments/assets/accaf485-5076-4667-824d-78e720fc222b" />
Figure 3.Log-Temperature–Density Relationship for Large Urban Areas.
Analysis restricted to larger built-up areas demonstrates that the positive association between temperature and population density remains present, although the relationship is still relatively weak.

LARGER URBAN AREAS RESULTS
1990
Correlation coefficient (r): 0.2862
P-value: 0.046205
Result: Statistically significant

2000
Correlation coefficient (r): 0.3476
P-value: 0.014385
Result: Statistically significant

2015
Correlation coefficient (r): 0.3917
P-value: 0.005379
Result: Statistically significant
