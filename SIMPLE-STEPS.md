# How to run the Virtual Machine and display the application in a web broswer

### The following dependencies must be installed
1. [Ruby]((https://github.com/oneclick/rubyinstaller2/releases/download/RubyInstaller-2.6.6-1/rubyinstaller-devkit-2.6.6-1-x64.exe))
2. [Vagrant]((https://releases.hashicorp.com/vagrant/))
3. [Virtual Box](https://www.virtualbox.org/wiki/Downloads)


### Cloning the repository

- We can download this Repository locally by downloading the zip folder
- We then unzip the folder and open up the command line 'favourably git bash'

### Ensuring the downloads have taken place
```commandline
vagrant --version #Should return version 2.2.7
ruby --version #Should return version 2.6.6p146
```

### Running the Virtual Machine
As we are already within the project folder, we can run the virtual machine from here
Within our provision.sh file, we have added the following command to the end
```commandline
node app.js
```
This means that our application runs when we spin up our VM, thus the whole process is automated
```commandline
vagrant up
```
When the VM has set up we should see the command ``` Your app is ready and listening on port 3000 ``` which means is 
verification that our application is ready

### Navigating to the web pages
Now that the application is up and running three web pages should now be available for us to see,
we can use any of the URL's below
```commandline
http://development.local/
http://development.local/fibonacci/4
http://development.local/posts
```