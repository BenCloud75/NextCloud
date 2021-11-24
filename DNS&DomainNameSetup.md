# Create a domain name for your NextCloud account

## 1 PreRequisites
### 1.1 Tooling
For my project I used the following tools: 

- I rented a domain name on [OVH](https://www.ovhcloud.com/en/domains/?xtor=SEC-13-GOO-[noi_ovh_fr_se_web_domain_defensive_Generic()]-[562743691637]-S-[ovh%20domain%20name]&xts=563736&gclid=CjwKCAiA4veMBhAMEiwAU4XRrwcaI5QgNF8JCH_ZXVrWWDbVGIsMf0LfsaOC0v_1AsI8DT-KOix_PRoClkMQAvD_BwE)
- DSM 7.1 installed
- Orange LiveBox router

### 1.2 General Concept

Before describing the different steps to perform for your installation, it is important to understand the general concept of the internet. 

Each device, website and other resource accessing the internet is identified with an IP address `192.165.0.1`. With the multiplication of webpages and resources accessible online, a solution was made available to prevent memorizing IP addresses but rather link them to a given name called DNS. Domain Name System is then a correspondance of domain name to IP address. 
![image](https://user-images.githubusercontent.com/75790837/143220526-f19eca16-9b9b-42ff-abf6-7f448e55d5c6.png)

Domain Names are hosted in DNS zones. A DNS zone contains all the configuration related to one domain name (e.g. services for website, mail servers etc). DNS zones are then hosted in a DNS server.
![image](https://user-images.githubusercontent.com/75790837/143221410-27567193-1d19-44b8-b94f-cb531d7d48d0.png)

When a domain name `exampledomain.com` is called, your request is oriented to the right DNS server that orients it to the right DNS zone. The DNS zone associates the domain name to the webpage's IP address. The website is displayed.

![image](https://user-images.githubusercontent.com/75790837/143221644-cc37452c-cc74-4dcf-9a13-56e3966bdd9c.png)

The goal of the configuration will be to link your domain name to the IP Address of your nextcloud image.

## 2 Installation
### 2.1 Pre-Condition
On your Synology NAS
- Have NextCloud operational (accessible via your IP in the URL). 
On your DNS Provider (OVH for me)
- Possess a Domain Name.
### 2.2 Post-Condition
- NextCloud is accessible via your domain name `exampledomain.com`

### 2.3 Installation Detail
#### 2.3.1 On DSM
The first thing to do on DSM is to create a Virtual Host on your webstation. The virtual host allows you to configure websites on Synology accessible via different domain names.

Go on your DSM Webstation / web Service Portal / Create / Create Service Portal / Virtual Host

![image](https://user-images.githubusercontent.com/75790837/143224280-29adece4-8849-49de-8329-23df60ca8881.png)

Configure your portal by putting: 
- your domain name `exampledomain.com`.
- open Ports 80/443 (we will later configure the router part).
- Document Root => Volume of your NextCloud repository
- HTTP back-end server in latest version of Apache
- PHP pointing to your configuration (done when setting up NextCloud, please [read the corresponding document](https://github.com/BenCloud75/NextCloud/blob/main/InstallationGuide.md)).

![image](https://user-images.githubusercontent.com/75790837/143224504-f22bd715-8de2-4e11-8082-a3f4878df828.png)

Once this part is configured, go to your NextCloud Repository in DSM and access the config.php in the /Config Folder.
The idea is to add the new domain name `exampledomain.com` to the list of trusted domains. 

```
Example
 'trusted_domains' => 
   [ '192.162.0.12','exampledomain.com',
   ],
```

In DSM Control Panel / Security, make sure your FireWall is well configured and allows Port 80 and Port 443 to be opened. If not, add the line to open ports 80 & 443 externally.

#### 2.3.2 On Router

Now that the DSM configuration is done, you need to configure your router to allow port 80 & port 443 to be accessible externally. 
To open Ports on the router, go to the NAT/PAT section of your router interface.

|Description | Internal Port | External Port | Protocol | IP |
|-------------| ------------- | ------------- |------------- | -------------|
|HTTPS| 443  | 443  |TCP/UDP| IP of your NAS|
|HTTP| 80  | 80  |TCP/UDP| IP of your NAS|

Sometimes, your NAS IP may change automatically from one day to another. You therefore need to create a static IP for your router with DHCP. 

|Name | IP Address | MAC address |
|-------------| ------------- | ------------- |
|My NAS| IP Address of my NAS I want to be statis  | MAC Address generated automatically  |

Some routers protect all your devices from externall intrusions. To do so, they do not expose your local device externally and restrict the IP address for internal use only. This may be a problem if you need to access your nextcloud externally. To have your nextCloud accessible externally, you need to configure the DMZ of your router and put the Static IP address and MAC address of your NAS.

|Name | IP Address | MAC address |
|-------------| ------------- | ------------- |
|My NAS| IP Address of my NAS I want to be statis  | MAC Address generated automatically  |

Additionnally, if your router has any firwall, make sure to open your NAS IP.

#### 2.3.3 On DNS provider

On the DNS provider, you need to create a DNS zone redirecting to your NextCloud URL IP_Of_My_Nas/nextcloud `192.165.0.12/nextcloud`. 
To link your Domain to Nextcloud, you need to make sure the DNS Zone linking the domain to your NextCloud IP is written. 

To do so, create a DNS Zone type TXT. 

There are different type of DNS Zone. I let you read the following webpage giving all the [DNS type possible when configuring your DNS Zone](https://en.wikipedia.org/wiki/List_of_DNS_record_types).

- Domain : put your domain name
- TTL corresponds to the time you need to cache a query before requesting a new one. I put 0
- Type: put TXT as you will enter the NextCloud IP in TEXT format
- Target : Put the IP of your NextCloud, in my case `192.165.0.12/nextcloud`

|Domain | TTL | Type | Target |
|-------------| ------------- | ------------- | ------------- |
|exampledomain.com| 0  | TXT  | 192.165.0.12/nextcloud|
