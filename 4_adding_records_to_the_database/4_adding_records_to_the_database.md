# Addings Records to Database

1. SQL or `Structured Query Language` is used to insert data into database
    - Here, we are using MySQL

2. The syntax for adding records is `INSERT INTO <TABLE_NAME> (<COLUMN_1>, <COLUMN_2>, ..., <COLUMN_N>) VALUES (<VALUE_1>, <VALUE_2>, ..., <VALUE_N>)`

**Example**

```
$sql = "INSERT INTO notes (title, content, important) VALUES ('";
$sql .= $title "',";
$sql .= $content "',";
$sql .= $important "'";
$sql .= ")";
```

3. `mysqli_query` is used to make a SQL query

**Example**
```
$sql = "INSERT INTO notes (title, content, important) VALUES ('";
$sql .= $title "',";
$sql .= $content "',";
$sql .= $important "'";
$sql .= ")";

if (mysqli_query($conn, $sql)) {
    echo "success";
}
```