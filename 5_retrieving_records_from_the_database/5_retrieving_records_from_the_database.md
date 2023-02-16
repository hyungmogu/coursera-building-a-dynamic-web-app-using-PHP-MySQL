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

2. database must be closed after each use
    - `mysqli_close` function is used to close database connection
    - `mysqli_close` is attached at the end of .php file

**Example**

includes/footer.php
```
<?php
    if (isset($conn)) {
        mysqli_close($conn)
    }
?>
```

new.php
```
<?php
    ...
?>

<!DOCTYPE html>
<html>
    <head>
        <title>Notes App</title>
        <link rel="stylesheet" href="styles/style.css">
    </head>
    <header>
                Notes App
    </header>

    <div class="titleDiv">
            <div class="backLink"><a class="nav-link" href="index.php"> Home</a></div>
            <div class="head">New Note</div>
    </div>
    <form action="new.php" method="post">     

            <span class="label">Title</span>
            <input type="text" name="title" />
            
            <span class="label">Content</span>
            <textarea name="content"> </textarea>

            <div class="chkgroup">
                <span class="label-in">Important</span>
                <input type="hidden" name="important" value="0" />
                <input type="checkbox" name="important" value="1" />
            </div>
            
        <input type="submit" />
    </form>
</html>
<?php
    require_once("includes/footer.php")
?>
```

3. SQL statement `SELECT <COLUMN_1>, ..., <COLUMN_N> FROM <TABLE_NAME>` is used to retrieve data
    - Instead of `<COLUMN_1>, ..., <COLUMN_N>`, `*` is used to retrieve values from all columns

**Example**

index.php
```
<?php
    require_once("includes/db.php");

    $sql = "SELECT * FROM notes";

    $notes = mysqli_query($conn, $sql);
?>
<!DOCTYPE html>
<html>
    <head>
        <title>Notes App</title>
        <link rel="stylesheet" href="styles/style.css">
    </head>
    <body>
        <header> 
            Notes App
        </header>
        <div>
                <div>
                    <a class="nav-link" href="new.php">Add a new note</a>
                </div>
                    <div class="note">
                        <div class="titleContainer">
                            <span class="nt-title"></span>
                            <div class="nt-links">
                                <a class="nt-link" href="#">edit note</a>
                                <a class="nt-link" href="#">[X] delete note</a>
                            </div>                 
                        </div>
                    
                         <div class="nt-content"></div>
                    </div>
        </div> 
    </body>
</html>
<?php
    require_once("includes/footer.php");
?>
```

4. `mysqli_fetch_assoc()` function converts fetched SQL result and converts it into associative array containing results

**Example**

index.php
```
<?php
    ...
    $notes = mysqli_query($conn, $sql);
?>
<html>
    <head>
        <title>Notes App</title>
        <link rel="stylesheet" href="styles/style.css">
    </head>
    <body>
        <header> 
            Notes App
        </header>
        <div>
            <div>
                <a class="nav-link" href="new.php">Add a new note</a>
            </div>
            <?php while($note = mysqli_fetch_assoc($notes)) {?>
                <div class="note">
                    <div class="titleContainer">
                        <span class="nt-title"><?php $note["title"]; ?></span>
                        <div class="nt-links">
                            <a class="nt-link" href=<?php echo 'edit.php?id=' . $note['id'];?>>edit note</a>
                            <a class="nt-link" href=<?php echo 'delete.php?id=' . $note['id'];?>>[X] delete note</a>
                        </div>                 
                    </div>
                
                    <div class="nt-content">
                        <?php if ($note["important"]) {?>
                            <span class="imp">IMPORTANT</span>
                        <?php }?>
                        <p>
                          <?php echo $note["content"];?>  
                        </p>
                    </div>
                </div>
            <?php }?>
        </div> 
    </body>
</html>
<?php
    require_once("includes/footer.php")
?>
```

## Aside

1. Inserted database entry can be checked at URL `localhost/phpmyadmin`

