# Install apache 2.4 and php7.1 on Debian 8

Simple mode:  
    * copy src contents to /var/www (if need use -v)  
    * not configure virtual host

## How use

### Build

```
docker build -t freeongoo/php71 .
```

### Run docker

```
docker run -d -p 8080:80 freeongoo/php71
```

### Check

Open in browser:  
`http://localhost:8080/index.php`

# Built With
* Debian 8
* php 7.1
* apache 2.4