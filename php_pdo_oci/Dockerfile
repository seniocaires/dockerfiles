# Dockerfile
# Imagem para ambiente PHP com PDO_OCI

FROM ubuntu:14.04
MAINTAINER Senio Caires <seniocaires@gmail.com>

ENV PATH_TMP_INSTALL=/tmp/install

RUN mkdir $PATH_TMP_INSTALL
RUN mkdir $PATH_TMP_INSTALL/pacotes
RUN mkdir $PATH_TMP_INSTALL/config

ADD pacotes/instantclient-basic-linux.x64-11.2.0.4.0.zip $PATH_TMP_INSTALL/pacotes
ADD pacotes/instantclient-sdk-linux.x64-11.2.0.4.0.zip $PATH_TMP_INSTALL/pacotes
#ADD pacotes/PDO_OCI-1.0.tgz $PATH_TMP_INSTALL/pacotes
ADD pacotes/PDO_OCI-1.0.zip $PATH_TMP_INSTALL/pacotes
ADD pacotes/oci8-2.0.11.zip $PATH_TMP_INSTALL/pacotes
ADD config/000-default.conf $PATH_TMP_INSTALL/config
ADD config/config.m4.patch $PATH_TMP_INSTALL/config
ADD config/oci8.ini $PATH_TMP_INSTALL/config
ADD config/pdo_oci.c $PATH_TMP_INSTALL/config
ADD config/pdo_oci.ini $PATH_TMP_INSTALL/config
ADD config/sqlnet.ora $PATH_TMP_INSTALL/config
ADD config/teste.php $PATH_TMP_INSTALL/config
ADD config/tnsnames.ora $PATH_TMP_INSTALL/config

#------------------------------------------------
# Instalacao de pacotes pelo apt
#------------------------------------------------

RUN apt-get update
RUN apt-get install -y apache2
RUN apt-get install -y php5 php5-dev php5-cli php5-curl php-pear php5-xmlrpc php-db php5-gd php5-intl php5-ldap libaio-dev build-essential libaio1 #libapache2-mod-php5 php5-mcrypt
RUN apt-get install -y git
RUN apt-get install -y subversion
RUN apt-get install -y zip

#------------------------------------------------
# Configuracao do Apache
#------------------------------------------------

RUN cp $PATH_TMP_INSTALL/config/teste.php /var/www/html/teste.php
RUN rm /etc/apache2/sites-enabled/000-default.conf
RUN cp $PATH_TMP_INSTALL/config/000-default.conf /etc/apache2/sites-enabled/000-default.conf

#RUN cd $PATH_TMP_INSTALL
#------------------------------------------------
# Configuracao do instantclient
#------------------------------------------------

RUN mkdir -p /opt/oracle/instantclient
RUN cp $PATH_TMP_INSTALL/pacotes/instantclient-basic-linux.x64-11.2.0.4.0.zip /opt/oracle/instantclient/instantclient-basic-linux.x64-11.2.0.4.0.zip
RUN cp $PATH_TMP_INSTALL/pacotes/instantclient-sdk-linux.x64-11.2.0.4.0.zip /opt/oracle/instantclient/instantclient-sdk-linux.x64-11.2.0.4.0.zip
RUN cd /opt/oracle/instantclient && unzip instantclient-basic-linux.x64-11.2.0.4.0.zip
RUN cd /opt/oracle/instantclient && unzip instantclient-sdk-linux.x64-11.2.0.4.0.zip
RUN mv /opt/oracle/instantclient/instantclient*/* /opt/oracle/instantclient/
RUN rmdir /opt/oracle/instantclient/instantclient*/
RUN ln -s /opt/oracle/instantclient/libclntsh.so.* /opt/oracle/instantclient/libclntsh.so
RUN ln -s /opt/oracle/instantclient/libocci.so.* /opt/oracle/instantclient/libocci.so
RUN echo /opt/oracle/instantclient >> /etc/ld.so.conf
RUN cd /opt/oracle/instantclient && ldconfig
RUN mkdir -p /opt/oracle/instantclient/network/admin
RUN cp $PATH_TMP_INSTALL/config/tnsnames.ora /opt/oracle/instantclient/network/admin/tnsnames.ora
RUN cp $PATH_TMP_INSTALL/config/sqlnet.ora /opt/oracle/instantclient/network/admin/sqlnet.ora
#RUN cd $PATH_TMP_INSTALL

#RUN cd $PATH_TMP_INSTALL
#------------------------------------------------
# Configuracao do OCI8
#------------------------------------------------


RUN mkdir /tmp/oci8
RUN cp $PATH_TMP_INSTALL/pacotes/oci8-2.0.11.zip /tmp/oci8/oci8-2.0.11.zip
RUN cd /tmp/oci8/ && unzip oci8-2.0.11.zip
RUN cd /tmp/oci8/oci8-2.0.11 && phpize && /tmp/oci8/oci8-2.0.11/./configure --with-oci8=instantclient,/opt/oracle/instantclient
RUN cd /tmp/oci8/oci8-2.0.11 && make && make install
#RUN pecl install oci8-2.0.11 #	instantclient,/opt/oracle/instantclient
RUN cp $PATH_TMP_INSTALL/config/oci8.ini /etc/php5/mods-available/oci8.ini
RUN php5enmod oci8
#RUN cd $PATH_TMP_INSTALL

#RUN cd $PATH_TMP_INSTALL

#------------------------------------------------
# Configuracao do PDO/OCI
#------------------------------------------------

#RUN cd /usr/include/
RUN ln -s /usr/include/php5 /usr/include/php
RUN mkdir -p /opt/oracle/instantclient/include/oracle/11.1/
#RUN cd include/oracle/11.1/
RUN ln -s /opt/oracle/instantclient/sdk/include /opt/oracle/instantclient/include/oracle/11.1/client
RUN mkdir -p /opt/oracle/instantclient/lib/oracle/11.1/client
#RUN cd lib/oracle/11.1/client
RUN ln -s /opt/oracle/instantclient/ /opt/oracle/instantclient/lib

RUN pecl channel-update pear.php.net

RUN mkdir -p /tmp/pear/download/
#RUN cp $PATH_TMP_INSTALL/pacotes/PDO_OCI-1.0.tgz /tmp/pear/download
RUN cp $PATH_TMP_INSTALL/pacotes/PDO_OCI-1.0.zip /tmp/pear/download/PDO_OCI-1.0.zip
#RUN cd /tmp/pear/download/
#RUN tar -xvf $PATH_TMP_INSTALL/pacotes/PDO_OCI-1.0.tgz -C /tmp/pear/download
RUN cd /tmp/pear/download/ && unzip PDO_OCI-1.0.zip
RUN cp $PATH_TMP_INSTALL/config/config.m4.patch /tmp/pear/download/PDO_OCI-1.0/config.m4.patch
RUN cd /tmp/pear/download/PDO_OCI-1.0 && patch --dry-run -i config.m4.patch && patch -i config.m4.patch && phpize
RUN rm /tmp/pear/download/PDO_OCI-1.0/pdo_oci.c
RUN cp $PATH_TMP_INSTALL/config/pdo_oci.c /tmp/pear/download/PDO_OCI-1.0/pdo_oci.c

RUN ORACLE_HOME=/opt/oracle/instantclient
RUN cd /tmp/pear/download/PDO_OCI-1.0 && ./configure --with-pdo-oci=instantclient,/opt/oracle/instantclient,11.1
RUN cd /tmp/pear/download/PDO_OCI-1.0 && make && make test && make install && mv /tmp/pear/download/PDO_OCI-1.0/modules/pdo_oci.so /usr/lib/php5/*+lfs/

RUN cp $PATH_TMP_INSTALL/config/pdo_oci.ini /etc/php5/mods-available/pdo_oci.ini
RUN php5enmod pdo_oci

RUN cd $PATH_TMP_INSTALL

#------------------------------------------------
# Inicializacao dos servicos
#------------------------------------------------

RUN chown -R www-data /var/www/html
RUN a2enmod rewrite 
RUN service apache2 stop
RUN service apache2 start
