# NextCloud Synology
## 1 PreRequisites

For my project, I am using the following device: 

- Synology DS 220+
- DSM 7.1
- Mac OS Big Sur (for the Terminal)
- Internet provider's router model
- Nextcloud latest stable version for home cloud

## 2 Installation
### 2.1 Pre-Condition
On your synologie NAS, instal the following packages:
- Webstation.
- Apache (latest version).
- PHP (Latest version).
- PHP My Admin (latest version). 
- MariaDB
- Text Editor
<img src="https://user-images.githubusercontent.com/75790837/142227035-e64ad85c-b564-4fc1-adc1-44ab404e54b2.png" width=40% height=40%>

### 2.2 Post-Condition
NextCloud is activated.

### 2.3 Installation Detail
#### 2.3.1 On DSM

**On the Webstation**: 
- Create a dedicated PHP Scrip language setting "NextCloud". 
- Update the default server portal with lastest APACHE and the new PHP script language you just created.
<img src="https://user-images.githubusercontent.com/75790837/142220878-46bd9f69-4a3e-4aae-8a7e-7adb5ec95a2a.png" width=50% height=50%>
<img src="https://user-images.githubusercontent.com/75790837/142221130-e49acecb-4dc1-4d73-b602-7ff95c9de0f5.png" width=50% height=50%>

- Activate the SSH on your NAS. Go to "ControlPanel"/"Terminal & SNMP" / Activate SSH and configure port
<img src="https://user-images.githubusercontent.com/75790837/142221367-81803f6e-fc7f-4d85-8f93-e3a092a8455b.png" width=50% height=50%>

**On Configuration Panel / ShareFolder**: 
All your NextCloud file will be stored on DSM under a SharedFile that I will call "NextCloud" for the rest of this guide. To do so, create a "NextCloud" ShareFolder on synology.

<img src="https://user-images.githubusercontent.com/75790837/142231391-bb4f7c36-bf13-4cdb-ba0b-ab7068f9ad3a.png" width=20% height=20%>

### 2.3.2 On Terminal
#### <font color="blue"> Enable SSH </font>
For each step described below, make sure SSH is activated. 

Access your NAS via SSH via the terminal. Use the following command
```
ssh YOUR_USER_NAME@NAS_IP_ADDRESS -p30
```

where 30 is my port. 
</br>_Example:_ 
```
abcd@123.345.12.3 -p30
```
#### <font color="blue"> Create Maria DB </font>
Access your MariaDB with the following command
```
mysql -u root -p
```
Then: 
- Create the MariaDB database
- Create the dataBase User
- Grant all privileges to the new user
- Flush all the privileges and Ext from the MariaDB shell
```
CREATE DATABASE your_NextCloud_Data_Base_Name;

CREATE USER 'your_Next_Cloud_User'@'localhost' IDENTIFIED BY 'your_Password';

GRANT ALL ON your_NextCloud_Data_Base_Name .* TO 'your_NextCloud_User'@'localhost';

FLUSH PRIVILEGES;
EXIT;
```
Your database should be <font color="red"> created </font>!

#### <font color="blue"> Download NextCloud Image </font>
Access your NAS via SSH (make sure SSH is enable on DSM). 
```
ssh YOUR_USER_NAME@NAS_IP_ADDRESS -p30
```
Acquire the NAS with root priviledge with `sudo -i`. System will ask for your NAS admin password. 

You are now connected as admin to your NAS. This will allow you to perform modification as an Admin.

When you installed the "WebStation" package, a new folder "web" should have been created in your Volume (e.g. /volume1/web/). Check this is the case `cd /volume1/web/`and `ls`. The folder `web_images`should be returned. With this command, you are now located inside the folder "web".

Now that you make sure the folder "web" exists in your NAS, you will need to download the latest stable version of NextCloud. The version is available here: https://nextcloud.com/install/#instructions-server . Right click on the DOWNLOAD button to "**copy the link address**" of the latest NextCloud version. Then, download the new version to your "web" folder with the command line `curl -O https://download.nextcloud.com/server/releases/nextcloud-22.2.3.zip`. Press Enter. 

Nextcloud ZIP file "nextcloud-22.2.3" should be downloaded in your "web" folder. Extract the .zip file with the command `7z x nextcloud-22.2.3.zip`

Give the right rights to the new folder "nextcloud" extracted in web and the ShareFolder "NextCloud" created in **2.3.1** inside Volume1 with `chown -R http:http nextcloud` + `chmod -R 0770 nextcloud` + `chown -R http:http volume1/NextCloud` + `chmod -R 0770 NextCloud`.
```
sudo -i
ENTER YOUR PASSWORD
cd/volume1/web/
ls
curl -O https://download.nextcloud.com/server/releases/nextcloud-22.2.3.zip
7z x nextcloud-22.2.3.zip

chown -R http:http nextcloud
chmod -R 0770 nextcloud
chown -R http:http /volume1/NextCloud/
chmod -R 0770 /volume1/NextCloud

------------------------------
where: 
- volume1 is your main volume. 
- web is the folder used by your webstation on DSM
- https://download.nextcloud.com/server/releases/nextcloud-22.2.3.zip** is the link address to download synology.

```

#### <font color="blue"> Access NextCloud </font>
NextCloud should be configured. 
Access it via `your_NAS_IP/nextcloud/`. You should end-up in the logging page of NextCloud (as shown below). 

Configure with: 
- a new admin user name
- a new password for your admin user
- SELECT MySQL/MariaDB
- your_NextCloud_User
- your_Password
- your_NextCloud_Data_Base_user
- 127.0.0.1:3307
<img src="https://user-images.githubusercontent.com/75790837/142233143-f2271823-7135-4eb7-bf1b-2f1332282675.png" width=30% height=30%>

You are now connected to NextCloud!! Enjoy! :)
## 3 Security

## 4 Error Case
