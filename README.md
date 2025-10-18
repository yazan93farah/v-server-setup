# v-server-setup
My V-Server Setup 

First of All my Username is yazan-farah
 and the ServerIP is : 91.99.224.69
 first of all i connect to the server with this command 
```ssh  yazan-farah@91.99.224.69 ```

it askes extra for the passward then after i logged in i copied the ssh public Key to the server and i tried to connect using this for disabled passward it works. so the ssh key works well then i set this: 
```Config.PasswordAuthentication : No ```
and i tried to Connect  
```ssh  yazan-farah@91.99.224.69 ```
it works even without the passward so now the passward i deacktivated and only i can enter the server with my ssh Key 


## Installing Nginx on my Server
for installing the Nginx i did : 
```plaintext
sudo apt update
sudo apt install nginx
```

then i did some change on the Config file so i served the file test.html instead of index.html
and i restarted the server 
``` sudo systemctl restart nginx ```
