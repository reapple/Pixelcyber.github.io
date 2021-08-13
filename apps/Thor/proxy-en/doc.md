---
layout: raw
---

## Sniffer Proxy FAQ

Sniff and debug HTTP traffic on other devices in same LAN with Thor.


### What can be sniffed with Thor

Devices or applications support HTTP Proxy, such as Mac/PC, iOS device, Android device, PS/Xbox, etc.


### 1. Browser & System HTTP Proxy Configuration

#### macOS HTTP proxy settings

a. Go to `System Preferences > Network > Choose a network to configure > Advanced > Proxies`

b. Check `Web Proxy (HTTP)` and `Secure Web Proxy (HTTPS)`

c. Enter proxy server address and port of Thor


#### Windows / Internet Explorer HTTP proxy settings

Network > Connections > Internet Options control panel

Microsoft Edge has an additional setting that you may need to make by browsing to `about:flags`.


#### Mozilla Firefox HTTP proxy settings

Open Firefox > Preferences > General > HTTP Proxy > choose the system proxy settings or others.


#### iOS Device HTTP proxy Settings

Settings > Wi-Fi > find the network you are connected to and then tap it to configure the network > scroll down to the HTTP Proxy setting > tap Manual > enter the proxy address and port of Thor


#### Android Device HTTP proxy Settings

Most Android devices have HTTP proxy settings, just enter the proxy address and port of Thor in it.


### 2. Trust Thor SSL CA on your device

"Thor SSL CA" certificate used in Thor for HTTPS decoding is safe and privacy security, it is generated randomly when Thor first launched and stored in app local keychain only.
Certificates between devices or users are different.

"Thor SSL CA" certificate is unnecessary, if you don't need HTTPS decryption.


#### macOS

Export "Thor SSL CA" certificate (.cer) to mac, then install and trust it in Keychain app.

Double click "Thor SSL CA" on macOS > Find it in Keychain > Get Info > Always Trust.


#### Windows

Export "Thor SSL CA" certificate (.cer) to Windows, then install and trust it in ` Trusted Root Certification Authorities store`.


#### iOS Device

* Send an email with "Thor SSL CA" certificate (.cer) attatched of Thor to target iOS device's Mail app, then tap attatchment in mail in target device, install and trust it in iOS system.

* Export "Thor SSL CA" certificate (.cer) to target device and save it to File app > iCloud Driver, then install it in iCloud Driver of File app.


#### Android Device

Export "Thor SSL CA" certificate (.p12 or .pem) to Android device, install & trust it.


#### Mozilla Firefox

Mozilla Firefox has its own Certificate Authority, Certificate Authority of system would not work on it.

Preferences > Security & Privacy > View Certificates > Certificate Authority > click Import button in bottom and import your "Thor SSL CA" > Check all the trust options > Confirm

