1. Challenge - While counting missing values ("-") in the Starbucks nutrition dataset, PySpark repeatedly threw an AnalysisException because it could not correctly resolve column names containing special characters, such as spaces, periods, and parentheses ex, Carb. (g).
    
solution - changed the code from col(c) to col(f"`{c}`") to nullify the effect of the special characters.

2. Challenge - While importing Starbucks drinks dataset from Excel file using pd.read_excel(), I discovered inconsistent data types in two columns: Total Fat (g) and Caffeine (mg).

solution - I used the dtype parameter and converted all the datatypes to string while loading so that there are no inconsistancies

3. Challenge - The Starbucks drinks file uses - for “no data”, so numeric columns were stored as text. While using cast(), I got CAST_INVALID_INPUT error.

solution - Used try_cast("double"), which turns bad text into NULL, then checked that the NULL counts matched the - counts.

4. Challenge - The item-name column had no header, so pandas named it Unnamed: 0
solution - Had it renamed as "Item".

5. Challenge - One fat value in the expanded file was turned into a date, and some caffeine values were the text “Varies”.

solution - Converted them to NULL. 

6. Challenge - A blank cell became NaN, which isNull() doesn’t count. Applying isnan to text columns also crashed.

solution - Counted NULL and NaN together, and applied isnan only to numeric (double) columns.

7. Challenge - A step kept failing with OutOfMemoryError: Java heap space. Later got to know the cause was the size of the query plan.

solution - After researching a bit, I got to know that the function convert_nutrients_to_numbers() using withColumn() was building the heap space exponentially so replaced it with select.

8. Challenge - I found it difficult to use the starbucks expanded drinks file as 
    - It’s organized by size and milk type, so it’s not comparable item by item.
    - Only 3 items matched the other drinks file, and there’s no way to know which size’s calories to use.

solution - So I skipped the file for comparison and worked with the other 3 files

9. - The brands have different menus (burgers vs pastries), no serving sizes, and unequal numbers of drinks. The distributions are not proper. (It actually feels like comparing apples to oranges just because they are fruits.)

solution - Compared food with food and drinks with drinks, used ratio measures (per 100 kcal, share of calories), used medians as a check, and stated the limits in report.txt
