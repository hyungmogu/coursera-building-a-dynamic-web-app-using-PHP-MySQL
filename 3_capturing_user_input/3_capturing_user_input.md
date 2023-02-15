# Capturing User Input

1. `REQUEST_METHOD` key under `$_SERVER` global variable is used to check whether the incoming request is one of DELETE, UPDATE, GET, POST

**Example**

```
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    ...
}
```

2. Data sent under POST method can be retrieved under `$_POST` global variable