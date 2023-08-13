# CSV Tools

## `csvkit`

It's a manipulation toolkit for CSV files.

### Installation

```bash
sudo apt install csvkit
```

### Commands

#### `csvclean`

Finds and cleans common syntax errors in CSV files.

- Clean a file: `csvclean file.csv`
- Show location on error: `csvclean -n file.csv`

#### `csvcut`

Filter and truncate CSV files. Like Unix's `cut` command, but for tabular data.

- Print names and indices of all columns: `csvcut -n file.csv`
- Select columns (e.g., columns 1, 3, and 4): `csvcut -c 1,3,4 file.csv`
- Select columns by name: `csvcut -c id,"first name" file.csv`
- Exclude columns: `csvcut -C 2,5 file.csv`

#### `csvformat`

Convert a CSV file to a custom output format.

- Convert to tab-delimited: `csvformat -T file.csv`
- Convert to custom delimiter (e.g., `/`): `csvformat -D "/" file.csv`

#### `csvgrep`

Filter CSV rows with string and pattern matching.

- Find rows with certain pattern in a column: `csvgrep -c <column(s)> -m <string> file.csv`
- Find rows that match a regular expression: `csvgrep -c <column(s)> -r <regular_expression> file.csv`
- Invert filtering (rows that don't match the pattern): `csvgrep -i -c <column(s)> -r <regular_expression> file.csv`

#### `csvlook`

Render a CSV file in the console as a fixed-width table.

- View file: `csvlook file.csv`

#### `csvsort`

Sort csv files.

- Sort by column: `csvsort -c <column> file.csv`
- Sort by column in descending order: `csvsort -r -c <column> file.csv`
- Sort by multiple columns: `csvsort -c <column1> <column2> file.csv`

#### `csvstat`

Print descriptive statistics for all columns in a CSV file.

- Show all stats: `csvstat file.csv`
- Show all stats for column(s): `csvstat -c 2,3 file.csv`
- Show sum of columns: `csvstat --sum -c <column> file.csv`
- Show show number of unique values in a column: `csvstat -c <column> --unique file.csv`
- Other functions to apply to columns:
  - Data Type: `--type`
  - Whether it has nulls: `--null`
  - Smallest values: `--min`
  - Largest values: `--max`
  - Means: `--mean`
  - Medians: `--median`
  - Standard deviations: `--stdev`
  - The length of the longest values: `--len`
  - Lists of frequent values: `--freq`
  - Total row count: `--count`

#### `csvsql`

Generate SQL statements for a CSV file or execute those statements directly on a database.

Usecases:

- Insert a csv file to a SQL database: `csvsql --insert --db "mysql://user:password@host/database" data.csv`
- Insert a csv file to a SQlite database: `csvsql --db sqlite:///new_database.db --insert your_data.csv`
- Run query against a csv file: `csvsql --query "select * from 'data'" data.csv`

##### `csvsql` flags

- `-d <DELIMITER>`: specify delimiter
- `-t`: Use tabs as delimiter
- `--blanks`: Do not convert "", "na", "n/a", "none", "null", "." to NULL
- `-H`: No header
- `-K N` or `--skip-lines N`: Skip the first `N` lines.
- `-l` or `--linenumbers`: Insert a column of line numbers.
- `--db CONNECTION_STRING`: If present, a sqlalchemy connection string to use to directly execute generated SQL on a database.
- `--query QUERY`: Execute one or more SQL queries delimited by ";" and output the result of the last query as CSV.
- `--insert`: In addition to creating the table, also insert the data into the table. Only valid when --db is specified.
- `--prefix PREFIX`: Add an expression following the INSERT keyword, like OR IGNORE or OR REPLACE.
- `--tables TABLE_NAMES`: Specify the names of the tables to be created. By default, the tables will be named after the filenames without extensions or "stdin".

One of the main usecases for this command is to run query directly against a csv file.

- Query a csv file: `csvsql --query 'select * from mytable' mytable.csv`
- Specify table name: `csvsql --query 'select * from mydata' mytable.csv --table mydata`
- Run query against multiple files: `csvsql select * from part1 union all select * from part2` part1.csv part2.csv
- Create a table and insert file into database: `csvsql --db sqlite:///database.db --insert mytable.csv --table data`
  - `--insert` flag is only valid when `--db` is specified.
  - `--table` is to specify table name (optional)
  - You can use `sql2csv`  to query the tables. Alternatively, use the database binary to query the database: `sqlite3 database.db "select * from data"`. For more information see `sqlite` section.

#### `in2csv`

Convert tabular data from various formats into CSV.

- Convert Excel file to CSV: `in2csv file.xlsx > file.csv`
- Convert Excel file to CSV with specific sheet: `in2csv file.xlsx --sheet "Sheet1" > file.csv`
- Convert JSON file to CSV: `in2csv file.json > file.csv`
- Combine with `jq`: `jq .results[0] file.json | in2csv -f json > file.csv`

##### `in2csv` flags

- `-f <FORMAT>`: Specify input format. Supported formats: `csv`, `dbf`, `fixed`, `xls`, `xlsx`, `json`, `ndjson`, `html`, `ltsv`, `ods`, `tsv`, `sqlite`
- `-s <SHEET>` or `--sheet <SHEET>`: Specify sheet name for Excel files

#### `sql2csv`

Query a SQL database and output results in CSV format:

```bash
csvsql --db "sqlite:///database.db" --insert data.csv --table data # Insert data into database
sql2csv --db "sqlite:///database.db" --query "select * from data" > data.csv # query the database
```

#### `csvjson`

Convert CSV to JSON and GeoJSON. Example: `csv2json file.csv > file.json`
Normally, the output is a list of dictionaries. To get dictionary as output, use `-k` flag you can specify a column to be used as key.

- `--lat <COLUMN>`: Specify column name for latitude
- `--lon <COLUMN>`: Specify column name for longitude
- `--k <COLUMN>`: Specify column name for key
- `--crs <CRS>`: Specify coordinate reference system
- `--indent <N>`: Specify indentation level
- `--geometry <GEOMETRY>`: Specify geometry type

#### `csvjoin`

Execute a SQL-like join to merge CSV files on a specified column or columns.
Consider the following tables:

```bash
# names.csv
| id | name    |
|----|---------|
| 1  | Alice   |
| 2  | Bob     |
| 3  | Charlie |

# grades.csv
| id | subject  | grade |
|----|----------|-------|
| 1  | Math     | A     |
| 1  | Science  | B     |
| 2  | Math     | B+    |
| 3  | Science  | A+    |
```

csvjoin will merge the two tables based on the `id` column: `csvjoin -c id names.csv grades.csv`. `-c` flag is used to specify the column(s) to join on. It can be either a single column or multiple columns separated by comma. The column can be specified by name or index.
Join types:

- `--left`: Left join
- `--right`: Right join
- `--outer`: Outer join

#### `csvstack`

Stack up the rows from multiple CSV files, optionally adding a grouping value.

- Simple stacking (stack all rows): `csvstack file1.csv file2.csv`
- Stack with grouping: `csvstack -g "file1,file2" file1.csv file2.csv`
  > It adds a column named `group` and the value of the column is the name of the file.
- Stack with grouping (specify column name): `csvstack -g "file1,file2" -n "file" file1.csv file2.csv`
  > It adds a column named `file` and the value of the column is the name of the file.
