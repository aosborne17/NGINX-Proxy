# NGINX Reverse Proxy :computer:

Earlier on in the week we discussed that typing an IP address into the URL bar would be difficult for any user,
these are lengthy numbers and people aren't likely to remember them, so instead we used "development.local:3000/"

When handing over a server to a client, we want to be able to remove the "/3000" at the end, we can do this via
reverse proxy. Therefore, our Node Application will run from that address.

NGINX will listen for requests on port 80 and pass them onto our app on port 3000

To be able to do this, we must first get into the theory about what a proxy server is

## Topics 

### 1) Proxy Server and Reverse Proxy

### 2) Creating Our Own Reverse Proxy

### 3) Automating This Process Using Bash Scripts

---


### Proxy Server and Reverse Proxy

- A proxy server retrieves data on the internet on the behalf of a user, acting as the middle man.

### Why we use proxy servers

1. **Increases Speed**
- The proxy server can store a web page into a centralised cache database, this means the server doesnt have to go out to
the internet to receive the information, it only has to search it's database.
- This also means the proxy server reduces bandwidth

![Proxy Server Speed](images/proxy-server-cache.png)


2. **Privacy**
- Proxy servers hide your IP address. As the proxy server retrieves the data, only the proxy server IP adress can be seen
viewing the web page

3. **Activity Logging**
- Organisations can keep track of what their employees are browsing and how long they are spending on those sites
- Companies can also block certain sites from being viewed

Proxy servers however cannot encrypt data as you surf the net, meaning it can be intercepted by hackers/
To overcome this, we can use a Virtual Private Network (VPN) which hides our IP address and encrypts data

---

### What is A Reverse Proxy

- A type of proxy server that sits behind the firewall in a private network and directs client requests to the appropriate
backend server.
- Reverse Proxies are implemented to help security, performance as well as managing flow of traffic to the website



![Proxy Image](images/Reverse-Proxy-Flow.svg)

---

### Creating Our Reverse Proxy

- Within sites-available, we have a default server that acts as the homepage for NGINX, in order to change the process we must
delete the default page and recreate a new one with the configurations we would like

- Once the VM is up and running, vagrant ssh into the VM named app and make your way to the location of 'sites available'
which can be found on the path below:

```bash
cd /etc/nginx/sites-available
```

- Once here we can delete the default file by running ..
```
sudo rm -r default
```
We can now create a new default file and enter it ... 

```bash
sudo touch default
sudo nano default
```
Then add the configurations that we would like..

```bash
server {
    listen 80;
    server_name _;
    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}

```

```bash

```
---

### Automating This Process Using Bash Scripts












```bash
echo "server{listen 80;
  listen 80;
  location / {
      proxy_pass http://192.168.10.100.3000;
  }
}" >> reverse-proxy.conf
```
