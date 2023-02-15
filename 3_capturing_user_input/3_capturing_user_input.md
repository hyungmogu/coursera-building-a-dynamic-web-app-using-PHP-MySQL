# Capturing User Input

1. `REQUEST_METHOD` key under `$_SERVER` global variable is used to check whether the incoming request is one of DELETE, UPDATE, GET, POST

**Example**

```
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    ...
}
```

2. Data sent under POST method can be retrieved under `$_POST` global variable

**Example**

```
<?php
    ...
    
    if ($_SERVER["REQUEST_METHOD"] == "POST") {
        $title = $_POST["title"];
    }
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
</html>
```

#