# qss20_finalproject_AW.AF.SD.ZS

Andy Feng, Alex Wojcik, Sherry Dong, Zach Shen

Using START data provided by Professor Johnson, we explored if evaluations of mental health, particularly reported irritability, were correlated with certain demographics (race and gender) around the times of the start of the COVID-19 lockdowns and the death of George Floyd in 2020. Using the data and notebook files below, we read in the Excel data we received from START, merged the two sheets, cleaned the data, ran a regression analysis, and visualized our results.

Data: in data/

Data can also be accessed from Google Drive, tried to avoid hard-coding path name:
https://drive.google.com/drive/u/0/folders/1zT_g7Gl2HGvFvscYAUocoXzufErBN3kW

00_pulldata.ipynb
- https://github.com/afwojcik/qss20_finalproject_AW.AF.SD.ZS/blob/main/code/00_pulldata.ipynb
    - Takes in Demographics and ABC Data sheets from Dartmouth Data Set.xlsx
    - Creates dataframes with data from these Excel sheets
    - Outputs and stores read-in data as two datatables ('data_set_abc' and 'data_set_demo')

01_merge.ipynb
- https://github.com/afwojcik/qss20_finalproject_AW.AF.SD.ZS/blob/main/code/01_merge.ipynb
    - Takes in two dataframes from the previous notebook ('data_set_abc' and 'data_set_demo'), one for each sheet from Dartmouth Data Set.xlsx
    - Outer merges the two dataframes on shared 'Local ID' and 'Region' for diagnostics
    - Keeps the rows where '_merge' equals to 'both' for the effect of an inner merge where both demographic and ABC data is available for an individual patient
    - Outputs merged dataset ('merged_df_demo_abc') and the dataset of rows that did not merge ('not_merged_df_demo_abc')

02_clean.ipynb
- https://github.com/afwojcik/qss20_finalproject_AW.AF.SD.ZS/blob/main/code/02_clean.ipynb
    - Takes in merged dataset ('merged_df_demo_abc') and the unmerged dataset ('not_merged_df_demo_abc')
    - Cleans dates ('date_reviewed') and race ('race_clean') and gender ('gender_clean') categories
    - Creates binary indicators ('is_black', 'is_male') for regression analysis
    - Defines irritability score from ABC evaluations to represent mental health condition ('irrit_score')
    - Subsets to data including only two demographic categories (black and white, male and female) for each analysis ('bw_only', 'mf_only')
    - Outputs cleaned data subsetted for each kind of analysis ('bw_only', 'mf_only')

03_bandwidths.ipynb
- https://github.com/afwojcik/qss20_finalproject_AW.AF.SD.ZS/blob/main/code/03_bandwidths.ipynb
    - Takes in cleaned subsetted data ('bw_only', 'mf_only')
    - Creates bandwidths of certain lengths before and after a certain date, represented by 'is_after' (subset_data())
    - Runs regression analysis for irritability score on the data before and after each date and demograhic (run_regression())
    - Uses OLS model to generate predicted values (run_predict())
    - Utilizes all functions with list comprehension
    - Generates tables from regression and prediction for use in LaTeX report
    - Outputs regression/correlation calculations ('viz_df_covid_race', 'viz_df_gf_race', 'viz_df_covid_gender', 'viz_df_gf_gender')

04_visualize.ipynb
- https://github.com/afwojcik/qss20_finalproject_AW.AF.SD.ZS/blob/main/code/04_visualize.ipynb
    - Takes in cleaned data, regression/correlation calculations ('viz_df_covid_race', 'viz_df_gf_race', 'viz_df_covid_gender', 'viz_df_gf_gender')
    - Visualizes regression for each analysis, faceted on 'is_after' and the binary indicator for the demographic
    - Outputs visualization of cleaned data and regression/correlation calculations, saved in output/
