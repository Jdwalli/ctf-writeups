# I've Been There Too
Forensics, 100 points

## Description:
Attached to this challenge is a sqlite file. It's a simulated student database where someone has come in afterward to make a few modifications. In my entire career, I've never had a student break into the student information system to change their grade or add credits they didn't earn, but it's always something I've thought about. I see it as a classic paradox of risk analysis and game theory. But this isn't the place for that discussion. Enjoy the challenge!

## Solution:

To analyze the provided SQLite database, I used the `sqlite3` tool.

First, I listed the tables within the database using `.tables`:

```shell
sqlite> .tables
new_students
```

This revealed a single table named ``new_students``. Next, I examined the table's schema using ``.schema``

```shell
sqlite> .schema new_students
CREATE TABLE new_students (
	id INT PRIMARY KEY,
	name TEXT NOT NULL,
	photo BLOB NOT NULL,
	gpa FLOAT NOT NULL,
	has_covid_vaccine BOOLEAN NOT NULL,
	year_graduated INT NOT NULL
);
```

After looking through some of the columns, I noticed that the ``name`` field contained some names that resembled the structure of the flag.

```shell
sqlite> SELECT DISTINCT name FROM new_students;
Akemy
Andrea
...
poctf{
uwsp_d0_4ndr01d5
Jessicawong
Jlee
...
_dr34m}
Visualsofdana
Zach
```

Combining these names allowed us to build the correct flag. 

The flag: ``poctf{uwsp_d0_4ndr01d5_dr34m}``