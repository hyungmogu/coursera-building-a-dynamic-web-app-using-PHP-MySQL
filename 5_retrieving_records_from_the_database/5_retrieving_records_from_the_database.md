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
<br/>
new.php
```

```

## Aside

1. Inserted database entry can be checked at URL `localhost/phpmyadmin`

