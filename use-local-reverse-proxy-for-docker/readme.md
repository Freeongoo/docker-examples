# Example create reverse proxy for docker

## How use

### Build

```
docker build -t freeongoo/python .
```

### Run docker

```
docker run -d -p 8080:80 freeongoo/python
```

### Check

Open in browser:  
`http://localhost:8080`

## Add proxy from apache

### Install and conf apache
```
sudo apt-get install apache2
sudo a2enmod proxy
sudo a2enmod proxy_http
```

### Add virtual host for proxy

Create virtual host in /etc/apache2/sites-available/python.loc.conf:
```
<VirtualHost *:80>
    ServerAlias python.loc www.python.loc

    ProxyPreserveHost On
    ProxyRequests off

    <Proxy *>
        Order deny,allow
        Allow from all
    </Proxy>

    ProxyPass / http://localhost:8080/
    ProxyPassReverse / http://localhost:8080/

</VirtualHost>
```

Include virtual host in apache:

```
sudo a2ensite python.loc
sudo /etc/init.d/apache2 restart
```

Add python.loc to /etc/hosts:
```
127.0.0.1 python.loc
```

### Check

Open in browser:  
`http://python.loc`

# Built With
* Python 2.7
* apache 2.4