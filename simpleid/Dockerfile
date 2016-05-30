# Dockerfile
# Imagem para OpenID Server usando o SimpleID

FROM ubuntu:16.04
MAINTAINER Senio Caires <seniocaires@gmail.com>

RUN apt-get update
RUN apt-get install -y apache2
RUN apt-get install -y php git php-curl
RUN apt-get install -y curl

ENV composer_path=/opt/composer
ENV simpleid_path=/opt
ENV simpleid_version=simpleid-1.0.1

# Install composer
CMD ["/usr/bin/mkdir", "$composer_path"]
WORKDIR $composer_path
RUN curl -sS https://getcomposer.org/installer | php

#Install simpleid
CMD ["/usr/bin/mkdir", "$simpleid_path"]
WORKDIR $simpleid_path
RUN curl -L http://downloads.sourceforge.net/simpleid/$simpleid_version.tar.gz > $simpleid_version.tar.gz
RUN tar -zxvf $simpleid_version.tar.gz
CMD ["/usr/bin/rm", "$simpleid_version.tar.gz"]
RUN rm $simpleid_path/simpleid/www/config.php.dist
ADD config.php simpleid/www/
RUN mkdir /var/simpleid
RUN mkdir /var/simpleid/identities
RUN mkdir /var/simpleid/cache
RUN mkdir /var/simpleid/store
RUN mkdir /var/www/simpleid
RUN mv simpleid/identities/* /var/simpleid/identities
RUN mv simpleid/cache /var/simpleid/cache
RUN mv simpleid/store /var/simpleid/store
RUN mv simpleid/www/* /var/www/simpleid

# init services
RUN service apache2 start
