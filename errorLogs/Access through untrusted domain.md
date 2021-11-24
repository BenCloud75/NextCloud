# Access Through Unstrusted Domain

![image](https://user-images.githubusercontent.com/75790837/143216407-14dfd7a9-6eea-4ec6-8689-ab9eb2f39302.png)

This error is return whenever a user is trying to log into your Nextcloud from an untrusted domain or IP address. 
As described in the message, you need to authorize the domain/IP in the "config.php" file located inside the /Configs folder of your Nextcloud repository. 

Inside the config.php file, add the corresponding domain in 'trusted_domains' sections. 

```
Example

I wish to add the following domain "nextcloudTest.com" and my IP address "192.165.0.1" as trusted domain for my Nextcloud. 
Inside the /Configs folder of my Nextcloud repository, I open the config.php file and add the following configuration

'trusted_domains' =>
   [
    'nextcloudTest.com',
    '192.165.0.1'
  ],

  
  ```
  
  **Go further**: For more information, consult the Nextcloud documentation [here](https://docs.nextcloud.com/server/latest/admin_manual/configuration_server/config_sample_php_parameters.html).
