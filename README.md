Please run this code in your Jupyter Notebook to view the dashboard. If you don't have any of the libraries installed, please install them and then run the dashboard in your command prompt using streamlit run theAPPname.py


import pandas as pd
import plotly.express as px
import streamlit as st

# Load data
demographics_data = pd.read_csv('C:/Users/EliteBook 840 G4/Downloads/m5_survey_data_demographics.csv')
technologies_data = pd.read_csv('C:/Users/EliteBook 840 G4/Downloads/m5_survey_data_technologies_normalised.csv')

# Setup tabs
tab1, tab2, tab3 = st.tabs(["Current Technology Usage", "Future Technology Trend", "Demographics"])

# Current Technology Usage Dashboard
# Visualization 1: Top 10 Languages Worked With
top_languages = technologies_data['LanguageWorkedWith'].value_counts().head(10)
fig1 = px.bar(top_languages, title="Top 10 Languages Worked With")
tab1.write(fig1)

# Visualization 2: Top 10 Databases Worked With
top_databases = technologies_data['DatabaseWorkedWith'].value_counts().head(10)
fig2 = px.bar(top_databases, title="Top 10 Databases Worked With")
tab1.write(fig2)

# Assuming 'WebFrameWorkedWith' is the correct column name
top_webframes = technologies_data['WebFrameWorkedWith'].value_counts().head(10)
fig_webframes = px.bar(top_webframes, title="Top 10 Web Frames Worked With")
tab1.write(fig_webframes)

# Future Technology Trend Dashboard
# Top 10 Languages Desired Next Year
top_languages_next_year = technologies_data['LanguageDesireNextYear'].value_counts().head(10)
fig3 = px.bar(top_languages_next_year, title="Top 10 Languages Desired Next Year")
tab2.write(fig3)

# Top 10 Databases Desired Next Year
top_databases_next_year = technologies_data['DatabaseDesireNextYear'].value_counts().head(10)
fig4 = px.bar(top_databases_next_year, title="Top 10 Databases Desired Next Year")
tab2.write(fig4)

# Platform Desired Next Year
platform_desire_next_year = technologies_data['PlatformDesireNextYear'].value_counts()
fig5 = px.treemap(platform_desire_next_year, path=[platform_desire_next_year.index], title="Platform Desire Next Year")
tab2.write(fig5)

# Top 10 Web Frames Desired Next Year
top_webframes_next_year = technologies_data['WebFrameDesireNextYear'].value_counts().head(10)
fig6 = px.scatter(top_webframes_next_year, size=top_webframes_next_year.values, color=top_webframes_next_year.index, title="Top 10 Web Frames Desired Next Year")
tab2.write(fig6)

# Demographics Dashboard
# Respondent classified by Gender
gender_count = demographics_data['Gender'].value_counts().reset_index()
gender_count.columns = ['Gender', 'Count']
fig7 = px.pie(gender_count, values='Count', names='Gender', title="Respondent Classified by Gender")
tab3.write(fig7)

# Respondent Count for Countries
country_count = demographics_data['Country'].value_counts().reset_index()
country_count.columns = ['Country', 'Count']
fig8 = px.bar(country_count, x='Country', y='Count', title="Respondent Count for Countries")
tab3.write(fig8)

# Respondent Count by Age
age_count = demographics_data['Age'].value_counts().sort_index().reset_index()
age_count.columns = ['Age', 'Count']
fig9 = px.line(age_count, x='Age', y='Count', title="Respondent Count by Age", markers=True)
tab3.write(fig9)

# Respondent Count by Gender, classified by Formal Education Level
education_gender = demographics_data.groupby(['EdLevel', 'Gender']).size().unstack().reset_index()
fig10 = px.bar(education_gender, x='EdLevel', y=education_gender.columns[1:], barmode='stack', title="Respondent Count by Gender, Classified by Education Level")
tab3.write(fig10)
