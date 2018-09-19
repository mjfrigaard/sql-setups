# PostgreSQL application and setup

Download the application from [this](https://postgresapp.com/) website and follow the installation instructions. 

The syntax documentation is [here](https://www.postgresql.org/docs/10/static/index.html) for Postgres.

## First steps 

In the terminal, enter the following:

```bash
sudo mkdir -p /etc/paths.d &&
echo /Applications/Postgres.app/Contents/Versions/latest/bin | sudo tee /etc/paths.d/postgresapp
```

You'll be asked to enter whatever password you need to install programs on your computer. 

## Creating users

[documentation](http://postgresguide.com/setup/users.html)

Now we can create a user. In a new terminal session (restart terminal after entering the previous commands), enter the following. 

```bash
psql -h localhost
```

This will bring up the `psql` command line. 

```bash
psql (10.5)
Type "help" for help.


```

To create a user for myself, I enter a `username` and `password`.

```sql
CREATE USER martin WITH PASSWORD 'strongpassword123';
CREATE ROLE
```

Then create a database (`countries`)

```sql
CREATE DATABASE countries;
CREATE DATABASE
```

Then grant privileges to the user on the database.

```sql
GRANT ALL PRIVILEGES ON DATABASE countries to martin;
GRANT
```

## Creating tables 

In order to load the data into the tables, they must be built first. 

Use `CREATE TABLE` to create the tables for the `countries` database. 

```sql
CREATE TABLE cities (
 name                    VARCHAR   PRIMARY KEY,
 country_code            VARCHAR,
 city_proper_pop         REAL,
 metroarea_pop           REAL,
 urbanarea_pop           REAL);
CREATE TABLE

CREATE TABLE countries (
 code                  VARCHAR     PRIMARY KEY,
 name                  VARCHAR,
 continent             VARCHAR,
 region                VARCHAR,
 surface_area          REAL,
 indep_year            INTEGER,
 local_name            VARCHAR,
 gov_form              VARCHAR,
 capital               VARCHAR,
 cap_long              REAL,
 cap_lat               REAL);
CREATE TABLE
CREATE TABLE languages (
 lang_id               INTEGER     PRIMARY KEY,
 code                  VARCHAR,
 name                  VARCHAR,
 percent               REAL,
 official              BOOLEAN);
CREATE TABLE
CREATE TABLE economies (
 econ_id               INTEGER     PRIMARY KEY,
 code                  VARCHAR,
 year                  INTEGER,
 income_group          VARCHAR,
 gdp_percapita         REAL,
 gross_savings         REAL,
 inflation_rate        REAL,
 total_investment      REAL,
 unemployment_rate     REAL,
 exports               REAL,
 imports               REAL);
CREATE TABLE
CREATE TABLE currencies (
 curr_id               INTEGER     PRIMARY KEY,
 code                  VARCHAR,
 basic_unit            VARCHAR,
 curr_code             VARCHAR,
 frac_unit             VARCHAR,
 frac_perbasic         REAL);
CREATE TABLE
CREATE TABLE populations (
 pop_id                INTEGER     PRIMARY KEY,
 country_code          VARCHAR,
 year                  INTEGER,
 fertility_rate        REAL,
 life_expectancy       REAL,
 size                  REAL);
CREATE TABLE 
CREATE TABLE countries_plus (
 name                  VARCHAR,
 continent             VARCHAR,
 code                  VARCHAR     PRIMARY KEY,
 surface_area          REAL,
 geosize_group         VARCHAR);
CREATE TABLE
CREATE TABLE economies2010 (
 code                  VARCHAR     PRIMARY KEY,
 year                  INTEGER,
 income_group          VARCHAR,
 gross_savings         REAL);
CREATE TABLE
CREATE TABLE economies2015 (
 code                  VARCHAR     PRIMARY KEY,
 year                  INTEGER,
 income_group          VARCHAR,
 gross_savings         REAL);
CREATE TABLE
```

Now that the tables exist, we can `/copy` the data from the .csv files into the database. 

*first you need to change the working directory to the folder with the .csv files*

```sql
\cd ~/SQL/Postgres/setup/data/countries/
```

if we print the contents of the `data/countries/` folder, we see: 

```bash
$ ls
cities.csv      currencies.csv      languages.csv
countries.csv       economies.csv       populations.csv
countries.sql       economies2010.csv
countries_plus.csv  economies2015.csv
```

## Copy data to database (from .csv files)

This will copy all the data to the database

```sql
\copy cities FROM 'cities.csv' DELIMITER ',' CSV HEADER;
COPY 236
\copy countries FROM 'countries.csv' DELIMITER ',' CSV HEADER;
COPY 206
\copy languages FROM 'languages.csv' DELIMITER ',' CSV HEADER;
COPY 955
\copy economies FROM 'economies.csv' DELIMITER ',' CSV HEADER;
COPY 380
\copy economies2010 FROM 'economies2010.csv' DELIMITER ',' CSV HEADER;
COPY 190
\copy economies2015 FROM 'economies2015.csv' DELIMITER ',' CSV HEADER;
COPY 190
\copy currencies FROM 'currencies.csv' DELIMITER ',' CSV HEADER;
COPY 224
\copy populations FROM 'populations.csv' DELIMITER ',' CSV HEADER;
COPY 434
\copy countries_plus FROM 'countries_plus.csv' DELIMITER ',' CSV HEADER;
COPY 206
```

This creates the `countries` database, which I can view using, `\dt`

```
\dt
                List of relations
 Schema |      Name      | Type  |     Owner      
--------+----------------+-------+----------------
 public | cities         | table | user
 public | countries      | table | user
 public | countries_plus | table | user
 public | currencies     | table | user
 public | economies      | table | user
 public | economies2010  | table | user
 public | economies2015  | table | user
 public | languages      | table | user
 public | populations    | table | user
(9 rows)
```

## DESCRIBE a table in `countries` database

The psql command for describing a table is `\d+ tablename`

```sql
\d+ cities
```


```
                                            Table "public.cities"
Column      |       Type        | Collation | Nullable | Default | Storage  | Stats target | Description 
-----------------+-------------------+-----------+----------+---------+----------+--------------+-------------
 name            | character varying |           | not null |         | extended |              | 
 country_code    | character varying |           |          |         | extended |              | 
 city_proper_pop | real              |           |          |         | plain    |              | 
 metroarea_pop   | real              |           |          |         | plain    |              | 
 urbanarea_pop   | real              |           |          |         | plain    |              | 
Indexes:
    "cities_pkey" PRIMARY KEY, btree (name)

\d+ countries
                                         Table "public.countries"
Column    |       Type        | Collation | Nullable | Default | Storage  | Stats target | Description 
--------------+-------------------+-----------+----------+---------+----------+--------------+-------------
 code         | character varying |           | not null |         | extended |              | 
 name         | character varying |           |          |         | extended |              | 
 continent    | character varying |           |          |         | extended |              | 
 region       | character varying |           |          |         | extended |              | 
 surface_area | real              |           |          |         | plain    |              | 
 indep_year   | integer           |           |          |         | plain    |              | 
 local_name   | character varying |           |          |         | extended |              | 
 gov_form     | character varying |           |          |         | extended |              | 
 capital      | character varying |           |          |         | extended |              | 
 cap_long     | real              |           |          |         | plain    |              | 
 cap_lat      | real              |           |          |         | plain    |              | 
Indexes:
    "countries_pkey" PRIMARY KEY, btree (code)
```




