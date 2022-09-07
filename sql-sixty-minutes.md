### Queries from [Learn SQL In 60 Minutes](https://youtu.be/p3qvj9hO_Bo)

- List all databases:

```sql
SHOW databases;
```

- Create a database:

```sql
CREATE DATABASE record_company;
```
- Use a database:

```sql
USE record_company;
```
- Create a table with a column:

```sql
CREATE TABLE test (
  test_column INT 
);
```
- Add another column to a table:

```sql
ALTER TABLE test
ADD another_column VARCHAR(255);
```

- Remove a table:

```sql
DROP TABLE test;
```

- Full query for the `bands` and `albums` tables:

```sql
CREATE DATABASE record_company;
USE record_company;
CREATE TABLE bands (
  id INT NOT NULL AUTO_INCREMENT,
  name VARCHAR(255) NOT NULL,
  PRIMARY KEY (id)
);
CREATE TABLE albums (
  id INT NOT NULL AUTO_INCREMENT,
  name VARCHAR(255) NOT NULL,
  release_year INT,
  band_id INT NOT NULL,
  PRIMARY KEY (id),
  FOREIGN KEY (band_id) references bands(id)
);
```

- Insert data into the `bands` table:

```sql
INSERT INTO bands (name)
VALUES ('Iron Maiden');
INSERT INTO bands (name)
VALUES ('Deuce'), ('Avenged Sevenfold'), ('Ankor');
```

- Query everuthing from the `bands` table:
  
```sql
SELECT * FROM bands;
```
- Query first two entries from the `bands` table:
  
```sql
SELECT * FROM bands LIMIT 2;
```
- Query the names of the columns from the `bands` table:
  
```sql
SELECT name FROM bands;
```
- As/Alias columns:
  
```sql
SELECT id AS 'ID', name AS 'Band name' FROM bands;
```
- Order by:
  
```sql
SELECT * FROM bands ORDER BY name DESC;
```

- Insert into:
  
```sql
INSERT INTO albums (name, release_year, band_id)
VALUES
('The number of the beats', 1985, 1),
('Power slave', 1984, 1),
('Nightmare', 2018, 2),
('Test album', NULL, 3);
```

- Unique select:
  
```sql
SELECT DISTINCT name from albums;
```

- Update row:
  
```sql
UPDATE albums
SET release_year = 1982
WHERE id = 1;
```

- Less than:
  
```sql
SELECT * FROM albums
WHERE release_year < 2000;
```

- Like string filter:
  
```sql
SELECT * FROM albums
WHERE name LIKE '%al%';
```

- Or:
  
```sql
SELECT * FROM albums
WHERE name LIKE '%al%' OR band_id = 2;
```
- And:
  
```sql
SELECT * FROM albums
WHERE release_year = 1984 AND band_id = 1;
```

- Between:
  
```sql
SELECT * FROM albums
WHERE release_year BETWEEN 2000 AND 2018;
```

- Null:
  
```sql
SELECT * FROM albums
WHERE release_year IS NULL;
```

- Delete:
  
```sql
DELETE FROM albums WHERE id = 5;
```

- Join:
  
```sql
SELECT * FROM bands
JOIN albums ON bands.id = albums.band_id;
```
- Right join:
  
```sql
SELECT * FROM albums
RIGHT JOIN bands ON bands.id = albums.band_id;
```

- Aggregate functions:
  
```sql
SELECT AVG(release_year) FROM albums;
```
  
```sql
SELECT band_id, COUNT(band_id) FROM albums
GROUP BY band_id;
```

- Alias table:

```sql
SELECT b.name AS band_name, COUNT(a.id) AS num_albums
FROM bands AS b
LEFT JOIN albums AS a ON b.id = a.band_id
GROUP BY b.id;
```

- Having vs. Where:

```sql
SELECT b.name AS band_name, COUNT(a.id) AS num_albums
FROM bands AS b
LEFT JOIN albums AS a ON b.id = a.band_id
WHERE b.name = 'Deuce'
GROUP BY b.id
HAVING num_albums = 1;
```

- https://github.com/WebDevSimplified/Learn-SQL