# NextCloud Synology

## PreRequisites

For my project, I am using the following device: 

- Synology DS 220+
- DSM 7.1
- Mac OS Big Sur (for the Terminal)
- Internet provider's router model
- Nextcloud latest stable version for home cloud

## Installation
### Pre-Condition
On your synologie NAS, instal the following packages:
- Webstation.
- Apache (latest version).
- PHP (Latest version).
- PHP My Admin (latest version). 
- MariaDB
- Text Editor

### Post-Condition
NextCloud is activated.

### Installation Detail
#### 1- On DSM

**On the Webstation**: 
- Create a dedicated PHP Scrip language setting "NextCloud". 
- Update the default server portal with lastest APACHE and the new PHP script language you just created.
<img src="https://user-images.githubusercontent.com/75790837/142220878-46bd9f69-4a3e-4aae-8a7e-7adb5ec95a2a.png" width=50% height=50%>
<img src="https://user-images.githubusercontent.com/75790837/142221130-e49acecb-4dc1-4d73-b602-7ff95c9de0f5.png" width=50% height=50%>

- Activate the SSH on your NAS. Go to "ControlPanel"/"Terminal & SNMP" / Activate SSH and configure port
<img src="https://user-images.githubusercontent.com/75790837/142221367-81803f6e-fc7f-4d85-8f93-e3a092a8455b.png" width=50% height=50%>

### 2- On Terminal
Make sure SSH is activated. 

Access your NAS via SSH via the terminal. Use the following command
`ssh YOUR_USER_NAME@NAS_IP_ADDRESS -p30`

where 30 is my port. 
_Example:_ 
`abcd@123.345.12.3 -p30`



## Security

## Error Case
