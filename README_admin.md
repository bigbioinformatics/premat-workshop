# How to set up RStudio Server

1. Create a virtual machine (VM). In this example, I used an AWS EC2 t2.medium with 36GB of storage running
Ubuntu 18.04.
2. Create SSH, HTTP, and HTTPS access from all IP addresses 
3. Login to the machine with SSH
4. Edit the ssh and sshd config files (`/etc/ssh/ssh_config` & `/etc/ssh/sshd_config`) to
allow password authentication:
```
PasswordAuthentication yes
```
5. Restart ssh 
```
sudo systemctl restart ssh
```
6. Create a new user and password:
```
sudo useradd test_user
sudo passwd test_user
```
7. Verify that you are able to login via ssh with `test_user`
8. Add the correct repo for `R` to your `/etc/apt/sources.list` file. Since
we are using Ubuntu 18.04, we choose the repository for `bionic`.
```
deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran40/
```
9. Add the secure apt key:
```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
```
10. Update and download `r-base`:
```
sudo apt update
sudo apt install r-base
```
11. Get rstudio server (for 18.04):
```
sudo apt-get install gdebi-core
wget https://download2.rstudio.org/server/bionic/amd64/rstudio-server-1.3.959-amd64.deb
sudo gdebi rstudio-server-1.3.959-amd64.deb
```
12. Open the server for HTTP traffic (port is `8787` by default). 
Edit the file `/etc/rstudio/rserver.conf` to include the line:
```
www-port=80
```
13. You should now be able to navigate to the address of your server and log in with the `test_user` credentials. 





