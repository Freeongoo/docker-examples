# Example create virtual host in apache 2.4 on Debian 8

### Build

See conf/apache/mylocal.loc.conf example configuration virtual host

```
docker build -t freeongoo/apache .
```

### Run docker

```
docker run -d -p 8080:80 freeongoo/apache
```

Add virtual host to /etc/hosts:  
`127.0.0.1  mylocal.loc`

### Check

Open in browser:  
`http://mylocal.loc:8080`