# Importing and Exporting Made Easy in MySQL

If you've ever wrestled with MySQL's Import and Export Wizard, you know it's not always the smoothest ride. Sure, it's got a user-friendly interface and promises to make data transfer a breeze, but let's be real—using the import and export table wizard can be frustratingly slow when you're dealing with an enormous dataset. There's also the fact that one misplaced comma or a funky character, and the wizard throws a fit unless all the data types are set to 'text' format.

## Enter: LOAD DATA INFILE & SELECT... INTO OUTFILE

### LOAD DATA INFILE

Imagine importing a file and within seconds (yes, I said it) your dataset is instantly imported into your database. That is the power of the LOAD DATA INFILE method. Let's get into the steps you will need to take to make this possible.

- #### Knowing your path:
  It is important to first know the location from which you will be conducting your importing and exporting. Running the SQL query below will show you the path from which your file will be imported and exported.
  
  ```sql
  SHOW VARIABLES LIKE 'secure_file_priv';  
  ```
  ![Screenshot (134)](https://github.com/YuYunusa/Importing-and-Exporting-Made-Easy-in-MYSQL/assets/160647840/12f90bf3-489f-454a-8738-7f724d890266)

- #### Finding your path:
  Locating the path is the next step, an easy one too, but if your path is the same as mine, then it's most likely hidden. To show hidden folders, while your file explorer is open, go to the 'view' tab, look for the 'hidden items' checkbox, and if it's empty, tick it. Now your hidden folders are shown. Once that is done, the rest should be easy—follow the path all the way to the last folder that was shown, which in this case is 'uploads'. That folder, no, that path in general is very important, so keep it in mind.
  
  ![Screenshot (135)](https://github.com/YuYunusa/Importing-and-Exporting-Made-Easy-in-MYSQL/assets/160647840/8ed7feb7-7223-43b0-b196-a13472d698c5)

  ![Screenshot (136)](https://github.com/YuYunusa/Importing-and-Exporting-Made-Easy-in-MYSQL/assets/160647840/a680dfb0-636d-4804-85bc-337a3070f591)

  ![Screenshot (137)](https://github.com/YuYunusa/Importing-and-Exporting-Made-Easy-in-MYSQL/assets/160647840/5225ff17-38fe-42fa-929e-a88fbb2d755e)

  ![Screenshot (138)](https://github.com/YuYunusa/Importing-and-Exporting-Made-Easy-in-MYSQL/assets/160647840/f9b0758f-f7d7-4a1e-83d0-ed9129244fbd)

- #### Importing with LOAD DATA INFILE Query
  We are now familiar with the path for importing, so how do we actually use the LOAD DATA INFILE to import our dataset? Using the query below, your files will be imported as quickly as possible.
  
  ```sql
  LOAD DATA INFILE '\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\dataset.CSV'
  INTO TABLE name_of_table
  FIELDS TERMINATED BY ','
  ENCLOSED BY '"'
  LINES TERMINATED BY '\r\n'
  IGNORE 1 LINES; 
  ```

#### NOTE:
Before you just start running the query, it is important to know some key details:

1. You have to create a table with the exact column names you are trying to import.
2. A copy of the dataset should be pasted in the 'Upload' folder of the path you located.
3. The path in the first line of the query is the format the path (C:\ProgramData\MySQL\MySQL Server 8.0\Uploads) should be in.
4. The last part of the path (\\dataset.CSV') is the exact name and extension of the dataset you want to import.
5. The second line of the query with (table_name) should contain your table name.

  ![Screenshot (181)](https://github.com/YuYunusa/Importing-and-Exporting-Made-Easy-in-MYSQL/assets/160647840/eac32a8a-a782-4a78-8cfb-5ebb8377b57a)

### SELECT ... INTO OUTFILE

Since we're already aware of the inner workings of LOAD DATA INFILE, I'll get straight to the point with this one because they are similar.

```sql
SELECT *
FROM name_of_table
INTO OUTFILE '\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\dataset.CSV'
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\r\n';
```

While similar, the major difference comes in the first two lines of the query, which use a SELECT FROM statement. This lets you SELECT everything or particular columns FROM your table INTO the same path as the one used in the LOAD DATA INFILE query, where (\\dataset.CSV) this time is the name you want to save your dataset as.

  ![Screenshot (182)](https://github.com/YuYunusa/Importing-and-Exporting-Made-Easy-in-MYSQL/assets/160647840/ffeae672-f235-42ce-b9e1-403b3e2ffd54)

And there you have it! Using LOAD DATA INFILE and SELECT ... INTO OUTFILE in MySQL is a powerful way to streamline your data import and export tasks. Whether you’re dealing with massive datasets or just need a quick way to transfer data, these commands have got you covered.

Got any questions or cool tips to share about MySQL data handling? Drop them in the comments below! Happy data juggling!
