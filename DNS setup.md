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

### 2.3 Installation Detail
