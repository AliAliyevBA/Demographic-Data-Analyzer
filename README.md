# Demographic-Data-Analyzer
# demographic_data_analyzer.py
import pandas as pd
df = pd.read_csv('path_to_your_data_file.csv')  # Replace with your actual CSV file path
race_counts = df['race'].value_counts()

average_age_men = round(df[df['sex'] == 'Male']['age'].mean(), 1)

percentage_bachelors = round((df['education'] == 'Bachelors').mean() * 100, 1)

advanced_education = df['education'].isin(['Bachelors', 'Masters', 'Doctorate'])
percentage_high_income_advanced = round((df[advanced_education]['salary'] == '>50K').mean() * 100, 1)

non_advanced_education = ~advanced_education
percentage_high_income_non_advanced = round((df[non_advanced_education]['salary'] == '>50K').mean() * 100, 1)

min_hours_per_week = df['hours-per-week'].min()

percentage_min_hours_high_income = round((df[df['hours-per-week'] == min_hours_per_week]['salary'] == '>50K').mean() * 100, 1)

country_high_income_percentage = df[df['salary'] == '>50K']['native-country'].value_counts(normalize=True) * 100
highest_country = country_high_income_percentage.idxmax()
highest_percentage = round(country_high_income_percentage.max(), 1)

most_popular_occupation_india = df[(df['salary'] == '>50K') & (df['native-country'] == 'India')]['occupation'].value_counts().idxmax()

print("1. Race counts:\n", race_counts)
print("2. Average age of men:", average_age_men)
print("3. Percentage with Bachelor's degree:", percentage_bachelors)
print("4. Percentage of advanced education earning >50K:", percentage_high_income_advanced)
print("5. Percentage of non-advanced education earning >50K:", percentage_high_income_non_advanced)
print("6. Minimum hours per week:", min_hours_per_week)
print("7. Percentage with min hours earning >50K:", percentage_min_hours_high_income)
print("8. Country with highest percentage earning >50K:", highest_country, "with percentage:", highest_percentage)
print("9. Most popular occupation for >50K earners in India:", most_popular_occupation_india)
