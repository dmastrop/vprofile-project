FROM nginx

LABEL "Project"="Vprofile"
LABEL "Author"="dmastrop"

# https://hub.docker.com/_/nginx
# We need to change the default conf file for this.
#So if you place templates/default.conf.template file, which contains variable references like this:
#listen       ${NGINX_PORT};
#outputs to /etc/nginx/conf.d/default.conf like this:
#listen       80;
# remove default conf file and replace with our own

RUN rm -rf /etc/nginx/conf.d/default.conf
COPY nginvproapp.conf /etc/nginx/conf.d/vproapp.conf
# this will replace the default conf file
