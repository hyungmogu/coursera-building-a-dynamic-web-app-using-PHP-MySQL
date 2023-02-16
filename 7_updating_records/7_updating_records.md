# Updating Records

1. There are two parts in edit.php
    - fetching data
    - updating data

2. Fetching data is done by GET request

**Example**

edit.php
```
<?php
    require_once("includes/db.php");

    if (!isset($_GET["id"])) {
        header("Location: index.php");
    }

    $id = $_GET["id"];
    $sql = "SELECT * FROM notes WHERE id = $id LIMIT 1";
    $result = mysql_query($conn, $sql);
    $note = mysqli_fetch_assoc($result);
?>
```

3. `mysqli_free_result()` function is used to free memory after fetching sql result 


edit.php
```
<?php
    require_once("includes/db.php");

    if (!isset($_GET["id"])) {
        header("Location: index.php");
    }

    $id = $_GET["id"];
    $sql = "SELECT * FROM notes WHERE id = $id LIMIT 1";
    $result = mysql_query($conn, $sql);
    $note = mysqli_fetch_assoc($result);
    mysqli_free_result($result);
?>
```

3. For updating, it's put in the same file, separated by if statement
    - `$_SERVER["REQUEST_METHOD"]` is used to determine whether the request method is `POST` or `GET`
    - `UPDATE <TABLE_NAME> SET <COLUMN_1> = <VALUE_1>, ... , <COLUMN_N> = <VALUE_N>` is used to update table entry

edit.php
```
<?php
    require_once("includes/db.php");
    require_once("includes/function.php");

    // POST
    if ($_SERVER["REQUEST_METHOD"] == "POST") {
        $title = prep_input($_POST['title']);
        $content = prep_input($_POST['content']);
        $important = prep_input($_POST['important']);

    }

    // GET
    if ($_SERVER["REQUEST_METHOD"] == "GET") {
        if (!isset($_GET["id"])) {
            header("Location: index.php");
        }

        $id = $_GET["id"];
        $sql = "SELECT * FROM notes where id = $id LIMIT 1";
        $result = mysqli_query($conn, $sql);
        $note = mysqli_fetch_assoc($result);
        mysqli_free_result($result);
    }
?>
```

## Aside

1. Inserted database entry can be checked at URL `localhost/phpmyadmin`

2. `mysqli_sql()` function is used to perform sql query

```
<?php
    $servername = "localhost";
    $username = "sqluser";
    $password = "sqlpass";
    $dbname = "notes";
    $conn = mysqli_connect($servername, $username, $password, $dbname);

    if (!$conn) {
        die("Connection failed: " . mysqli_connect_error());
    } else {
        echo "Connected successfully";
    }

    mysqli_sql($conn, $sql);
?>
```

2. `header` function can be used to redirect to any php page including home page

```
<?php
    require_once("incldues/db.php");

    if (!isset($_GET["id"])) {
        header("Location: index.php");
    }
?>
```

