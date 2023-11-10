# MySql-Installation-Centos7
1. ** Remove previous installed packages and clear cache
```sh
# look for the mysql installed packages
sudo yum list installed | grep mysql

sudo yum remove mysql80-community-release.noarch

sudo yum clean all --verbose
```
2. 
