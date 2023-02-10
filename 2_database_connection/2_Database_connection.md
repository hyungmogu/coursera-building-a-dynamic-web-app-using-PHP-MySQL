# Database connection

- XAMPP creates http server on the local machine.
    - Using this allows to use server name `localhost`

- To make mysql connection, the function `mysqli_connect` is used

```
<?php
    $servername = "localhost";
    $username = "sqluser";
    $password = "sqlpass";
    $dbname = "notes";
    $conn = mysqli_connect($servername, $username, $password, $dbname);
?>
```

- Use if statement to make a check whether error occurs due to
    1. Database doesn't exist
    2. username and password are incorrect
    3. server is down or not available

    - `mysqli_error` function is used to print error statement
    - `mysqli_connect_error` function is used to print error regarding connection
    - `die` is equivalent to raising exception in Javascript or Python

```
<?php
    $servername = "localhost";
    $username = "sqluser";
    $password = "sqlpass";
    $dbname = "notes";
    $conn = mysqli_connect($servername, $username, $password, $dbname);

    if (!$conn) {
        die("Connection failed" . mysqli_connect_error());
    }
?>
```


- To check, go to the path where the .php file containing `mysqli_connect` is located starting from the root
    - e.g. localhost/new.php