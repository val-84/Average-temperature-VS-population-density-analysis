# Average-temperature-VS-population-density-analysis
# The aim of this project was to analyse if avgerage temperatures are affected by population density in big cities. Please download the csv files before running the code.

import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
from scipy.stats import pearsonr

ghs_stat = pd.read_csv(
    "GHS_STAT_UCDB2015MT_GLOBE_R2019A_V1_2.csv",
    encoding='iso-8859-1'
)


cols = [
    'E_WR_T_90', 'E_WR_T_00', 'E_WR_T_14',
    'P90', 'P00', 'P15',
    'B90', 'B00', 'B15'
]

ghs_stat = ghs_stat[cols].copy()


# Convert all columns to numeric
ghs_stat = ghs_stat.apply(pd.to_numeric, errors='coerce')

# Replace infinite values with NaN
ghs_stat.replace([np.inf, -np.inf], np.nan, inplace=True)

# Remove missing values
ghs_stat.dropna(inplace=True)

# Remove rows where built-up area is zero
# (avoids division by zero errors)

ghs_stat = ghs_stat[
    (ghs_stat['B90'] > 0) &
    (ghs_stat['B00'] > 0) &
    (ghs_stat['B15'] > 0)
]

print(ghs_stat.shape)


ghs_stat['D90'] = ghs_stat['P90'] / ghs_stat['B90']
ghs_stat['D00'] = ghs_stat['P00'] / ghs_stat['B00']
ghs_stat['D15'] = ghs_stat['P15'] / ghs_stat['B15']


# Log transformation helps reduce skewness
# and makes patterns easier to visualise

ghs_stat['log_D90'] = np.log10(ghs_stat['D90'])
ghs_stat['log_D00'] = np.log10(ghs_stat['D00'])
ghs_stat['log_D15'] = np.log10(ghs_stat['D15'])

# Remove any infinite values created by log transform
ghs_stat.replace([np.inf, -np.inf], np.nan, inplace=True)
ghs_stat.dropna(inplace=True)


print(ghs_stat.head())

print("\nData Types:\n")
print(ghs_stat.dtypes)

print("\nMissing Values:\n")
print(ghs_stat.isnull().sum())
# ORIGINAL DENSITY VS TEMPERATURE

sns.set_theme(style="whitegrid")

fig, axes = plt.subplots(1, 3, figsize=(20, 6))

years = [
    ('E_WR_T_90', 'D90', '1990'),
    ('E_WR_T_00', 'D00', '2000'),
    ('E_WR_T_14', 'D15', '2015')
]

for ax, (temp, density, year) in zip(axes, years):

    sns.regplot(
        data=ghs_stat,
        x=temp,
        y=density,
        scatter_kws={
            'alpha': 0.4,
            's': 15
        },
        line_kws={
            'color': 'red'
        },
        ax=ax
    )

    ax.set_title(f'{year}')
    ax.set_xlabel('Average Temperature (°C)')
    ax.set_ylabel('Population Density')

plt.suptitle(
    'Population Density vs Average Temperature',
    fontsize=16
)

plt.tight_layout()
plt.show()
# LOG POPULATION DENSITY VS TEMPERATURE

fig, axes = plt.subplots(1, 3, figsize=(20, 6))

log_years = [
    ('E_WR_T_90', 'log_D90', '1990'),
    ('E_WR_T_00', 'log_D00', '2000'),
    ('E_WR_T_14', 'log_D15', '2015')
]

for ax, (temp, density, year) in zip(axes, log_years):

    sns.regplot(
        data=ghs_stat,
        x=temp,
        y=density,
        scatter_kws={
            'alpha': 0.4,
            's': 15
        },
        line_kws={
            'color': 'red'
        },
        ax=ax
    )

    ax.set_title(f'{year}')
    ax.set_xlabel('Average Temperature (°C)')
    ax.set_ylabel('Log Population Density')

plt.suptitle(
    'Log Population Density vs Average Temperature',
    fontsize=16
)

plt.tight_layout()
plt.show()
# PEARSON CORRELATION ANALYSIS

print("PEARSON CORRELATION RESULTS")

for temp, density, year in years:

    r, p = pearsonr(
        ghs_stat[temp],
        ghs_stat[density]
    )

    print(f"{year}")
    print(f"Correlation coefficient (r): {r:.4f}")
    print(f"P-value: {p:.6f}")

    if p < 0.05:
        print("Result: Statistically significant")
    else:
        print("Result: Not statistically significant")

    print()

# PEARSON CORRELATION ANALYSIS LOG DENSITIES

print("LOG DENSITY CORRELATION RESULTS")

for temp, density, year in log_years:

    r, p = pearsonr(
        ghs_stat[temp],
        ghs_stat[density]
    )

    print(f"{year}")
    print(f"Correlation coefficient (r): {r:.4f}")
    print(f"P-value: {p:.6f}")

    if p < 0.05:
        print("Result: Statistically significant")
    else:
        print("Result: Not statistically significant")

    print()
# ANALYSIS FOR LARGER BUILT-UP AREAS ONLY

ghs_stat2 = ghs_stat.copy()

# Keep only larger urban areas
ghs_stat2 = ghs_stat2[ghs_stat2['B15'] > 700]

print("\nShape of larger urban areas dataset:")
print(ghs_stat2.shape)

# PLOT FOR LARGER URBAN AREAS

fig, axes = plt.subplots(1, 3, figsize=(20, 6))

for ax, (temp, density, year) in zip(axes, log_years):

    sns.regplot(
        data=ghs_stat2,
        x=temp,
        y=density,
        scatter_kws={
            'alpha': 0.5,
            's': 20
        },
        line_kws={
            'color': 'red'
        },
        ax=ax
    )

    ax.set_title(f'{year}')
    ax.set_xlabel('Average Temperature (°C)')
    ax.set_ylabel('Log Population Density')

plt.suptitle(
    'Larger Urban Areas: Log Density vs Temperature',
    fontsize=16
)

plt.tight_layout()
plt.show()
# CORRELATION FOR LARGER URBAN AREAS

print("LARGER URBAN AREAS RESULTS")

for temp, density, year in log_years:

    r, p = pearsonr(
        ghs_stat2[temp],
        ghs_stat2[density]
    )

    print(f"{year}")
    print(f"Correlation coefficient (r): {r:.4f}")
    print(f"P-value: {p:.6f}")

    if p < 0.05:
        print("Result: Statistically significant")
    else:
        print("Result: Not statistically significant")

    print()
Scatter plots and Pearson correlation analysis were used to examine the relationship between population density and average temperature in urban areas for 1990, 2000 and 2015. The plots showed a weak positive relationship across all three years, meaning that areas with higher temperatures tended to have slightly higher population densities. However, the data points were widely spread out, suggesting that the relationship is not particularly strong. A number of highly populated cities also appeared as outliers, highlighting large differences between urban areas around the world.

The Pearson correlation coefficients were relatively low, indicating that average temperature alone is not a strong predictor of population density. Despite this, some of the p-values showed statistical significance, likely because of the large size of the dataset. The trend lines followed a similar pattern in all three years, suggesting that the relationship between temperature and population density remained fairly consistent over time.

Overall, the analysis suggests there may be a small association between warmer climates and higher urban population density, but the relationship is weak and is likely influenced by many other factors such as economic development, geography and infrastructure.
