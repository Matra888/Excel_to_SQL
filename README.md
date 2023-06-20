# Excel_to_SQL

**Automating tasks - importing large Excel files to a SQL database**

Import large Excel files to SQL database such as PostgreSQL with simple Python Code. 

Here is a short 3 min video on the code implementation - https://www.loom.com/share/caa0243287ea4f95a078c1faf50c5a81

Python code here: 

```python
import pandas as pd
from sqlalchemy import create_engine

# Replace with your file location
file_location = '/path/to/your/file.csv'

# Read CSV file into a pandas DataFrame (check if separator is correct!)
print("Read CSV into DataFrame")
df = pd.read_csv(file_location, sep=';')

# Clean column names (remove special characters and spaces)
# df.columns = df.columns.str.replace('[^a-zA-Z0-9_]', '')
df.columns = df.columns.str.replace(' ', '_')
df.columns = df.columns.str.lower()

print(df.head())

# Replace with your PostgreSQL username, password, and database information
username = 'your_username'
password = 'your_password'
database = 'your_database'

# Connect to the SQL database
print("Connecting to SQL database")
engine = create_engine(f'postgresql://{username}:{password}@localhost/{database}')

# Replace with your desired table name
table_name = 'your_table_name'

# Write the DataFrame to SQL, overwriting the table if it already exists
print("Writing DataFrame to SQL")
df.to_sql(table_name, engine, if_exists='replace', index=False)
print("Done")

