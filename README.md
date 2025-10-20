# Welcome to My First Markdown Tutorial

In this document, I explain step by step how I connected to my server, set up SSH key authentication, disabled password login, and installed Nginx.

---

## Table of Contents

1. [General Information](#general-information)  
2. [Connecting to the Server](#connecting-to-the-server)  
3. [Setting Up the SSH Key](#setting-up-the-ssh-key)  
4. [Disabling Password Authentication](#disabling-password-authentication)  
5. [Installing Nginx](#installing-nginx)  
6. [Modifying the Nginx Configuration](#modifying-the-nginx-configuration)  
7. [Summary](#summary)

---

## General Information

- **Username:** `My-Username`  
- **Server IP Address:** `My-Server-Ipaddress`

---

## Connecting to the Server

First, I connected to the server using SSH:

```bash
ssh yazan-farah@91.99.224.69
```

At first, it asked for my password. After logging in successfully, I copied my SSH public key to the server and tested key-based login.

---

## Setting Up the SSH Key

After copying my **SSH public key** to the server, I tested the connection again.  
It worked without asking for a password, confirming that SSH key authentication is set up correctly.

---

## Disabling Password Authentication

To ensure only SSH keys can be used to log in, I disabled password authentication in the SSH daemon configuration.

**Edit the SSH config (on the server):**

```bash
sudo nano /etc/ssh/sshd_config
```

**Set this option (ensure it’s not commented):**
```conf
PasswordAuthentication no
```

**Apply the change:**
```bash
sudo systemctl reload ssh    # or: sudo systemctl restart ssh
```

**Test again from your client:**
```bash
ssh yazan-farah@91.99.224.69
```

The connection works without a password, meaning password login is deactivated and only my SSH key can access the server.

---

## Installing Nginx

I installed Nginx with the following commands:

```bash
sudo apt update
sudo apt install nginx
```

---

## Modifying the Nginx Configuration

I changed the configuration so the server serves `test.html` instead of the default `index.html`, then restarted Nginx.

> Adjust the **index** directive for the relevant server block (for example in `/etc/nginx/sites-available/default`):

```conf
server {
    # ...
    root /var/www/html;
    index test.html;  # serve test.html instead of index.html
    # ...
}
```

**Restart Nginx to apply changes:**
```bash
sudo systemctl restart nginx
```

---

## Summary

- Connected to the server via SSH  
- Copied and tested the SSH public key (passwordless login works)  
- Disabled password authentication (`PasswordAuthentication no`)  
- Installed Nginx and configured it to serve `test.html` instead of `index.html`
