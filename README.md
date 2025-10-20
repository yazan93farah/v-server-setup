# 🚀 Server Setup Tutorial – SSH, Git & Nginx

The tutorial provides a step-by-step guide to connecting to a Linux server, securing SSH access, configuring Git, installing Nginx, and adjusting its default configuration.
---

## 📚 Table of Contents

1. [Server Details](#🔐-server-details)  
2. [Connecting via SSH](#🔌-connecting-via-ssh)  
3. [Setting Up SSH Key Authentication](#🔑-setting-up-ssh-key-authentication)  
4. [Disabling Password Authentication](#🚫-disabling-password-authentication)  
5. [Installing Git & Configuring It](#🛠-installing-git--configuring-it)  
6. [Installing Nginx](#🌐-nginx)  
7. [Changing Nginx to Serve `test.html`](#⚙️-changing-nginx-to-serve-testhtml)  
8. [✅ Summary](#✅-summary)

---

## 🔐 Server Details

- **Username:** `your-username`
- **Server IP Address:** `your.server.ip.address`

---

## 🔌 Connecting via SSH

Use the following command to connect to your server:

```bash
ssh your-username@your.server.ip.address
```

If it's your first time, it will ask for your password.

---

## 🔑 Setting Up SSH Key Authentication

1. **On your local machine**, generate an SSH key if you don’t have one:

   ```bash
    ssh-keygen -t ed25519 -C "generated-key-name" 
   ```

2. **Copy your public key to the server:**
   ```bash
    ssh-copy-id -i ~/.ssh/fileToCopy user@remote_host
    
   ```
3. **Test login without password:**
   ```bash
   ssh your-username@your.server.ip.address
   ```

---

## 🚫 Disabling Password Authentication

To improve security, disable password login:

1. SSH into the server and open SSH config:
   ```bash
   sudo nano /etc/ssh/sshd_config
   ```

2. Find and set:
   ```conf
   PasswordAuthentication no
   ```

3. Restart the SSH service:
   ```bash
   sudo systemctl restart ssh
   ```

4. Test the password login : 
   ```bash
   ssh -o PubKeyAuthentication=no -i pfad/zum/private-key your-username@your.server.ip.address
   ```


✅ Now only SSH key authentication works.


---

## 🛠 Installing Git & Configuring It

### Install Git:
```bash
sudo apt update
sudo apt install git
```

### Configure Git (one-time setup):
```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

### Generate ssh-Key for Github (one-time setup):
```bash
 ssh-keygen -t ed25519 -C "generated-key-name" 
 ssh-add ~/.ssh/generated-key-name
 ```
✅ Git is now set up for use with version control.

---

## 🌐 Installing Nginx

To install and start Nginx:

```bash
sudo apt update
sudo apt install nginx
```

After installation, Nginx should be running:

```bash
systemctl status nginx
```

---

## ⚙️ Changing Nginx to Serve `test.html`

Let’s change the default page from `index.html` to `test.html`.

1. **Create the test page**:
```bash
sudo touch /var/www/html/test.html
sudo nano /var/www/html/test.html
```

and added this <div>Hello, World!</div> to the test.html


2. **Edit the Nginx default site config**:
```bash
sudo nano /etc/nginx/sites-available/default
```

3. **Change the index directive**:
```nginx
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    index test.html;

    server_name _;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

4. **Reload Nginx**:
```bash
sudo systemctl reload nginx
```

✅ Your server should now serve `test.html` at `http://your.server.ip.address`.

---

## ✅ Summary

- ✅ Connected via SSH  
- ✅ Set up SSH key login and disabled password login  
- ✅ Installed Git and configured name/email  
- ✅ Installed Nginx and verified it runs  
- ✅ Served a custom `test.html` page via Nginx  

---
 
