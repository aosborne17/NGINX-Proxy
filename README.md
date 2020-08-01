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

- A reverse proxy is a server that sits in front of one or more web servers, intercepting requests sent from the client
- The reverse proxy will then sent requests to and receive requests from the origin server


![Proxy Image](images/Reverse-Proxy-Flow.svg)

- Usually all requests from computer D would go directly to server F.
- With a reverse proxy however, all request go from D to E and then E will forward the requests to F,
the appropriate response will then be sent back from F to E and then to the client D

### Benefits Of A Reverse Proxy

1. **Protection From Attacks**
- With having reverse proxies in place, the origin server never needs to reveal their IP address
making it much harder to be a victim of cyber attacks

2. **Caching**
- A reverse proxy can temporarily store data when a request is made to a web site, if another person tries
to access this same site in a nearby area, the content would load much faster as the request only has to go to the
reverse proxy and back

3. **Load Balancing**
- Reverse proxies can evenly distribute incoming traffic to different servers to make sure no single server becomes
overloaded


Forward Proxy | Reverse Proxy
-----|------
Sits in front of a client|Sits in front of an origin server 
Ensures no origin server ever communicates directly with that specific client| Ensures that no client ever communicates directly with that origin server
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
