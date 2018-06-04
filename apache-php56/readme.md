# Install apache 2.4 and php5.6 on Debian 8

Simple mode:  
    * copy src contents to /var/www (if need use -v)  
    * not configure virtual host

## How use

### Build

```
docker build -t freeongoo/php56 .
```

### Run docker

```
docker run -d -p 8080:80 freeongoo/php56
```

### Check

Open in browser:  
`http://localhost:8080/index.php`

# Built With
* Debian 8
* php 5.6
* apache 2.4