# Data Cleaning Project Using Pandas

This project focuses on cleaning and preprocessing a messy dataset using Python, specifically pandas. The dataset had missing values, duplicate records, inconsistent formats, unnecessary columns, and null values.

## Dataset

 * Source: Kaggle
 * Size: 30,758 rows and 8 columns
 * Type: E-Commerce Dataset

## Problems in the Dataset

* Missing/null values
* Duplicate rows
* Inconsistent column names
* Incorrect data types
* Extra spaces / messy text

## Data Cleaning Steps

Step 1: Load the dataset using `pd.read_csv()`

Step 2: Use `drop_duplicates()` to delete duplicate rows

Step 3: Check the data types of all columns

Step 4: Strip the unnecessary part of the MRP column using
`df["MRP"].str.strip("Rs\n")`

Step 5: Convert the MRP column to numeric using
`pd.to_numeric(df['MRP'], errors='coerce')`
Here, `errors='coerce'` replaces invalid values with NaN

Step 6: Create a new column and fill NaN values with the mean MRP grouped by 'Category' using
`df.groupby('Category')['MRP'].transform('mean')`

Step 7: Drop the old MRP column

Step 8: Clean the Discount column, convert it to numeric, and create a new column.
Fill NaN values with median grouped by 'BrandName', and replace remaining NaN with 0 (for brands with no discount):

```python
df['Discount_percent'] = df['Discount'].fillna(
    df.groupby('BrandName')['Discount'].transform('median')
).fillna(0)
```

Then delete the old Discount column

Step 9: Similar steps are applied to SellPrice, but NaN values are filled using:
`df['MRP_'] * (df['Discount_percent'] / 100)`

Step 10: Rename the 'Category' column to 'Womens_Category' using
`df.rename(columns={'Category':'Womens_Category'}, inplace=True)`

Step 11: Replace all NaN / empty values in the Size column with `pd.NA`

Step 12: Handle remaining NaN values in 'Details' and 'BrandName' columns and drop those rows

## Final Result

* Clean and structured dataset
* No missing or duplicate values
* Consistent formatting across all columns
* Ready for analysis or visualization

## Tools Used

* Python
* Pandas

## Files

* `NoteBook_1.ipynb` → data cleaning process
* `cleaned_data.csv` → final cleaned dataset

## Conclusion

This project demonstrates practical data cleaning techniques using pandas, transforming raw messy data into a usable format for analysis.
