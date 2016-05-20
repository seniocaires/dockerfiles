# Dockerfile
# Imagem para OpenID Server usando o SimpleID

FROM ubuntu:16.04
MAINTAINER Senio Caires <seniocaires@gmail.com>

RUN apt-get update
RUN apt-get install -y php git php-curl
RUN apt-get install -y curl

ENV composer_path=/opt/composer

CMD ["/usr/bin/mkdir", "$composer_path"]
WORKDIR $composer_path
RUN curl -sS https://getcomposer.org/installer | php
