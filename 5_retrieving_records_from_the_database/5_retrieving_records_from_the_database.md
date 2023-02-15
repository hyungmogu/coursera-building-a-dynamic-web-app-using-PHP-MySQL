# Retrieving Records from the Database

1. a block of code can be imported using `require_once()` function

**Example**

includes/db.php
```
<?php
    $servername = "localhost";
    $username = "sqluser";
    $password = "sqlpass";
    $dbname = "notes";
    $conn = mysqli_connect($servername, $username, $password, $dbname);

    if (!$conn) {
        die("Connection failed: " . mysqli_connect_error());
    }

?>
```

new.php
```
<?php
    require_once("includes/db.php");

    if ($_SERVER["REQUEST_METHOD"] == "POST") {
        $title = $_POST["title"];
        $content = $_POST["content"];
        $important = $_POST["important"];

        echo $title;
        echo $content;
        echo $important;
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

#