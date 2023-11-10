# MySql-Installation-Centos7
1. ** Remove previous installed packages and clear cache **
```sh
# look for the mysql installed packages
sudo yum list installed | grep mysql

sudo yum remove mysql80-community-release.noarch

sudo yum clean all --verbose
```
2. ** Manually Remove Remaining MySql Cache Folders
   ```sh
   sudo rm -R /var/cache/yum/x86_64/7/mysql*
   ```
3. ** Setup Yum Repository
```sh
sudo update
rpm -Uvh https://repo.mysql.com/mysql80-community-release-el7-3.noarch.rpm
```
4. ** Disable All Repositories In MySql Repository File
 ```sh
sed -i 's/enabled=1/enabled=0/' /etc/yum.repos.d/mysql-community.repo
```
5. ** Install MySQL Community Server
```sh
yum --enablerepo=mysql80-community install mysql-community-server 
```
### If you get below error then use below command otherwise skip it
_ The GPG keys listed for the "MySQL 8.0 Community Server" repository are already installed but they are not correct for this package.
Check that the correct key URLs are configured for this repository.


 Failing package is: mysql-community-client-8.0.28-1.el7.x86_64
 GPG Keys are configured as: file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql _
 ### Import New GPG Key:
 ```sh
rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
yum --enablerepo=mysql80-community install mysql-community-server
```
6. ** Start MySql **
   ```sh
   sudo systemctl start mysqld
   sudo systemctl status mysqld
   sudo systemctl enable mysqld  
   ```

# How To Access MySql

1. ** Get Temporary Password Of MySql **
   ```sh
   sudo  grep 'temporary password' /var/log/mysqld.log
   ```
 2.  ** Access MySQL and Change the Password: **
       ```sh
         mysql -u root -p
      ```
       Note:
       It will prompt you for the password. Enter the temporary password from the log file.
         After logging in, you can set a new password for the root user:
3. ** Reset Root Password **
   ```sh
   ALTER USER 'root'@'localhost' IDENTIFIED BY 'your_new_password';

   ```
   Replace 'your_new_password' with the actual password you want to set.
