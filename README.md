# nginx







1.  Update the package list:
    
    ```bash
    sudo apt update
    sudo apt upgrade -y
    ```
- **`apt`**:  
The Advanced Package Tool (APT) is a package management system used by Debian-based Linux distributions like Ubuntu. It simplifies installing, updating, and managing software packages.


2. Install NGINX
	```
	sudo apt install nginx -y
	```
3. Verify NGINX
	 ``` 
	 sudo systemctl status nginx
	```
	- Enable NGINX to start on boot:
	```
	sudo systemctl enable nginx 
	```
4. To check whether nginx is installed or not, we can check in browser by enter the IP of that vm. if we get the output welcome to nginx then successfully installed the nginx
5. check the node and npm is installed or not with the command of node -v and npm -v
6. creating the directory for react app
	```
	sudo mkdir -p /var/www/react-app
	```
7. place all the files present in build folder or directly build folder(react-app)
8. Set the correct permissions:
	 ```
	 sudo chown -R www-data:www-data /var/www/react-app
	sudo chmod -R 755 /var/www/react-app
	```
### Configure NGINX
9. Create a new NGINX server block configuration file for the React app: 
	 ```
	 sudo nano /etc/nginx/sites-available/react-app
	 ```
10. add the following configuartions to that file
	```
	server {
    listen 80;
    server_name 10.10.45.83;

    root React_Js/var/www/fgweb;
    index index.html;

    location / {
        try_files $uri /index.html;
    }

    error_page 404 /index.html;

    access_log /var/log/nginx/react-app.access.log;
    error_log /var/log/nginx/react-app.error.log;
	}
	```
11. Create a symbolic link to enable the configuration:
	```
	sudo ln -s /etc/nginx/sites-available/react-app /etc/nginx/sites-enabled/
	```
12. check the syntax errors
	```
	sudo nginx -t
	```
13. Reload NGINX to apply changes
	``` 
	sudo systemctl reload nginx
	   ```
14. finally access the url in the browser with the port number given in the configuration file.
