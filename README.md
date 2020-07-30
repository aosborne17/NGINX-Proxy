# NGINX Reverse Proxy

Earlier on in the week we discussed that typing an IP address into the URL bar would be difficult for any user,
these are lengthy numbers and people aren't likely to remember them, so instead we used "development.local:3000/"

When handing over a server to a client

What is Reverse Proxying





- When you create a profile inside a vm, it will inherit everything inside .bashrc
- Our vagrant file and our Virtual Machine are two different things, when we do vagrant destroy
our VM is destroyed but our vagrant folder is still there
thus .profile is still present.


### Additional ways
```bash
echo "server{listen 80;
  listen 80;
  location / {
      proxy_pass http://192.168.10.100.3000;
  }
}" >> reverse-proxy.conf
```

``` > ``` redirects output to a file, overwriting the file
``` >> ``` redirects output to a file appending the redirected output at the end

ctrl k at start of the line ---> Removes whole line


killall node