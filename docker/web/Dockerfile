FROM  nginx:latest

# conf file
COPY ./conf/nginx.conf /etc/nginx/nginx.conf
COPY ./conf/default.conf /etc/nginx/conf.d/default.conf

# html file
# allocate index.html to the path that specified as "root" in "location" directive in default.conf
COPY ./data/index.html /usr/share/nginx/html/index.html