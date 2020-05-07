ARG APACHE_VERSION=""
FROM httpd:${APACHE_VERSION:+${APACHE_VERSION}-}alpine

RUN apk update; \
    apk upgrade;

# Copy apache vhost file to proxy php requests to php-fpm container
COPY default.apache.conf /usr/local/apache2/conf/default.co.uk.apache.conf
RUN echo "Include /usr/local/apache2/conf/ecowebhosting.co.uk.apache.conf" \
    >> /usr/local/apache2/conf/httpd.conf

#copy certs to apache
COPY ./certs/ecowebhosting.co.uk.crt /usr/local/share/ca-certificates/ecowebhosting.co.uk.crt
COPY ./certs/ecowebhosting.co.uk_chain.crt /usr/local/share/ca-certificates/ecowebhosting.co.uk_chain.crt
COPY ./certs/ecowebhosting.co.uk_pk.key /usr/local/share/ca-certificates/ecowebhosting.co.uk_pk.key
