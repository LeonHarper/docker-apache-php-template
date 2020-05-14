ARG APACHE_VERSION=""

FROM httpd:${APACHE_VERSION:+${APACHE_VERSION}-}alpine

RUN apk update; \
    apk upgrade;

# Declaring https://github.com/moby/moby/issues/34482
# the ARG without setting a value, will make it take the default value from the ARG defined in the global stage. 
ARG PRIMARY_DOMAIN
ARG EWH_SHARED_LIBS_DIR
ARG EWH_ADMIN
ARG EWH_MAIN_SITE_ROOT_DIR

# Copy apache vhost file to proxy php requests to php-fpm container
COPY default.apache.conf /usr/local/apache2/conf/${PRIMARY_DOMAIN}.apache.conf
RUN echo "Include /usr/local/apache2/conf/${PRIMARY_DOMAIN}.apache.conf" \
    >> /usr/local/apache2/conf/httpd.conf

#copy certs to apache
COPY ./certs/${PRIMARY_DOMAIN}.crt /usr/local/share/ca-certificates/${PRIMARY_DOMAIN}.crt
COPY ./certs/${PRIMARY_DOMAIN}_chain.crt /usr/local/share/ca-certificates/${PRIMARY_DOMAIN}_chain.crt
COPY ./certs/${PRIMARY_DOMAIN}_pk.key /usr/local/share/ca-certificates/${PRIMARY_DOMAIN}_pk.key
