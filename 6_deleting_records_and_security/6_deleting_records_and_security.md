# Deleting Records and Security

1. Delete is done by performing the following SQL statement `DELETE FROM <TABLE_NAME> WHERE id=<TARGET_ENTRY_ID>`

```
"DELETE FROM notes WHERE id='" . $id . "' LIMIT 1 ";
```

**Example**

delete.php
```
<?php
    require_once("includes/db.php");

    if (!isset($_GET["id"])) {
        header("Location: index.php");
    }

    $id = $_GET["id"];
    $sql = "DELETE FROM notes WHERE id = $id LIMIT 1";

    if (mysqli_query($conn, $sql)) {
        header("Location: index.php");
    }
?>
```

2. To prevent injection of malicious code into SQL (called **SQL Injection Attack**), function `htmlspecialchars()` is used

**Example**

includes/function.php
```
<?php
    function prep_input($data) {
        $data = trim($data);
        $data = stripslashes($data);
        $data = htmlspecialchars($data);

        return $data;
    }
?>
```

new.php 
```
<?php
    require_once("includes/db.php");
    require_once("includes/functions.php");

    if ($_SERVER["REQUEST_METHOD"] == "POST") {
        $title = prep_input($_POST["title"]);
        $content = prep_input($_POST["content"]);
        $important = prep_input($_POST["important"]);

        ...
    }

    $sql = "INSERT INTO notes (title, content, important) VALUES ('";
    $sql .= $title "',";
    $sql .= $content "',";
    $sql .= $important "'";
    $sql .= ")";

    if (mysqli_query($conn, $sql)) {
        echo "success";
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

