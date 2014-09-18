gridfs-nginx-plugin
===================

gridfs-nginx plugin that works for real!!

I provide this from our company's development department    
after compiling and bug fixing in all of the components in this project.

Nginx 1.6.1 and Nginx-Gridfs Installation
===================================

1. Create a folder that you are going to save all the files by:   
    `mkdir nginx-gridfs`
2. Enter to **nginx-gridfs** folder.
3. Download nginx-1.6.1 from this url:  
    `wget http://nginx.org/download/nginx-1.6.1.tar.gz`
4. Clone this repo by:
    `git clone `
5. (optional - the right driver is in the repo) Enter to **gridfs-nginx-plugin** and clone the mongodb C driver repo by:   
    `git clone https://github.com/eagleas/mongo-c-driver.git`
6. Step out from **gridfs-nginx-plugin** by:   
    `cd ..`
7. Enter to **nginx-1.6.1** folder by:  
    `cd nginx-1.6.1`
8. Run ./configure with the full path to the **gridfs-nginx-plugin** folder by (make sure that ./configure is runnable - chmod +x ./configure):   
    `./configure --add-module=</path/to/gridfs-nginx-plugin folder>`

FOR MAC:  
     in the **gridfs-nginx-plugin** folder change in *config* file **CFLAGS** to  
     `CFLAGS="$CFLAGS -Wno-unused-function -Wno-missing-field-initializers --std=c99 -Isrc"`  
     `./configure --add-module=</path/to/gridfs-nginx-plugin folder> --with-cc-opt="-Wno-deprecated-declarations"`

9. Run make by:
    `make`
10. Run make install by:
    `make install`
11. Now your Nginx + Nginx-Gridfs is installed under:   
    /usr/local/nginx - *the folder of all nginx folders*
    /usr/local/nginx/sbin/nginx - *the nginx executable*

Make Nginx as Linux service
===========================
1. Add the service in /etc/init.d by:  
    `sudo wget https://raw.github.com/JasonGiedymin/nginx-init-ubuntu/master/nginx -O /etc/init.d/nginx`
2. Make sure nginx is execute file by:   
    `chmod +x /etc/init.d/nginx`
3. Now you can use:   
      `service nginx start`   
      `service nginx stop`   
      `service nginx restart`  


Configure Nginx to work with MongoDB Girdfs
===========================================
1. Open nginx.conf by:   
    `cd /usr/local/nginx/conf/nginx.conf`
2. Add the following lines:  
	
	`server {`   
		`listen 80;`   
		`server_name <your url>;`     
		`location /<choose url>/ {`  
		    `gridfs <db-name>`  
			    `root_collection=<the collection of the files>`   
			    `field=_id`  
			    `type=objectid`  
			    `user=<db username>`   
			    `pass=<db password>;`  
		    `mongo 127.0.0.1:27017;`  
		`}`   
	`}`
  
3. Restart nginx by:   
    `service nginx restart`


That all if you have any issues or questions please refer to **barak@socialskycorp.com** !
