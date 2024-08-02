# HestiaCP Installation and Configuration Guide

## Introduction

HestiaCP is a fork of VestaCP, a bold and smart initiative to offer a lightweight replacement to commercial web server admin panels. This guide includes tips for using HestiaCP with Cloudflare, focusing on port configuration and SSL setup.

## Unattended HestiaCP Installation

My humble contribution to this project is a tiny online app aimed at generating the necessary script line for an unattended HestiaCP installation.

## Tips for Using HestiaCP With Cloudflare

### Changing the HestiaCP Port

Cloudflare doesn’t allow port 8083, so you can change HestiaCP to use port 2083 instead in your terminal:

```bash
sudo su -
v-change-sys-port 2083
```

Make sure you have all the necessary ports allowed in the Oracle ingress rules:

```yaml
2083, 80, 443, 143, 993, 110, 995, 25, 465, 587
```

### Using Cloudflare Origin SSL

For maximum performance, use Cloudflare origin SSL. This also provides 15-year certificates, reducing the need for frequent updates. To add the Cloudflare certificate authority to your server:

```bash
sudo su -
wget https://developers.cloudflare.com/ssl/static/origin_ca_rsa_root.pem
mv origin_ca_rsa_root.pem origin_ca_rsa_root.crt
cp origin_ca_rsa_root.crt /usr/local/share/ca-certificates
update-ca-certificates
```

### Cloudflare Email Tips

For the A records for `mail` and `webmail` DNS, change them to DNS only:

![DNS Settings](https://user-images.githubusercontent.com/4044180/216274625-5e17d1a1-1ee1-4e02-9ba0-fdeb4c7fd8f4.png)

Then use ‘Let’s Encrypt’ for SSL on your mail domain rather than Cloudflare:

![Let’s Encrypt SSL](https://user-images.githubusercontent.com/4044180/216274559-34ceed15-56d8-4b48-bd4a-7cf6d2d69eda.png)


 You may access it here  https://benzntech.github.io/hestiacp-scriptline-generator/

 Feel free to use it, improve it or integrate it
 
 
Credits: https://ideaspot.com.au/blog/cloudflare-hestia-setup/
