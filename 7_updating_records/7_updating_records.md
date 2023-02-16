# Updating Records

1. 

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

