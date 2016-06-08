# Dockerfile
# Imagem para ambiente PHP com PDO_OCI

FROM ubuntu:14.04
MAINTAINER Senio Caires <seniocaires@gmail.com>

RUN PATH_TMP_INSTALL=/tmp/install

RUN mkdir $PATH_TMP_INSTALL

ADD pacotes/instantclient-basic-linux.x64-11.2.0.4.0.zip $PATH_TMP_INSTALL/pacotes
ADD pacotes/instantclient-sdk-linux.x64-11.2.0.4.0.zip $PATH_TMP_INSTALL/pacotes
ADD pacotes/PDO_OCI-1.0.tgz $PATH_TMP_INSTALL/pacotes
ADD config/000-default.conf $PATH_TMP_INSTALL/config
ADD config/config.m4.patch $PATH_TMP_INSTALL/config
ADD config/oci8.ini $PATH_TMP_INSTALL/config
ADD config/pdo_oci.c $PATH_TMP_INSTALL/config
ADD config/pdo_oci.ini $PATH_TMP_INSTALL/config
ADD config/sqlnet.ora $PATH_TMP_INSTALL/config
ADD config/teste.php $PATH_TMP_INSTALL/config
ADD config/tnsnames.ora $PATH_TMP_INSTALL/config

#RUN echo "------------------------------------------------"
#RUN echo " Instalacao de pacotes pelo apt"
#RUN echo "------------------------------------------------"

#RUN echo "Atualizando apt ..."
#RUN apt-get update
#RUN echo "Instalando Apache ..."
#RUN apt-get install -y apache2
#RUN echo "Instalando Apache/PHP ..."
#RUN apt-get install -y php5 php5-dev php5-cli php5-curl php-pear php5-xmlrpc php-db php5-gd php5-intl php5-ldap libaio-dev build-essential libaio1 #libapache2-mod-php5 php5-mcrypt
#RUN echo "Instalando Git ..."
#RUN apt-get install -y git
#RUN echo "Instalando Subversion ..."
#RUN apt-get install -y subversion

#RUN echo "------------------------------------------------"
#RUN echo " Configuracao do Apache"
#RUN echo "------------------------------------------------"

#RUN echo "Copiando arquivo de teste ..."
#RUN cp $PATH_TMP_INSTALL/config/teste.php /var/www/html/teste.php
#RUN echo "Copiando sites-enabled ..."
#RUN rm /etc/apache2/sites-enabled/000-default.conf
#RUN cp $PATH_TMP_INSTALL/config/000-default.conf /etc/apache2/sites-enabled/000-default.conf

#RUN cd $PATH_TMP_INSTALL
#RUN echo "------------------------------------------------"
#RUN echo " Configuracao do instantclient"
#RUN echo "------------------------------------------------"

#RUN echo "Criando diretorio instantclient ..."
#RUN mkdir -p /opt/oracle/instantclient
#RUN echo "Copiando arquivos ..."
#RUN cp $PATH_TMP_INSTALL/pacotes/instantclient-basic-linux.x64-11.2.0.4.0.zip /opt/oracle/instantclient/instantclient-basic-linux.x64-11.2.0.4.0.zip
#RUN cp $PATH_TMP_INSTALL/pacotes/instantclient-sdk-linux.x64-11.2.0.4.0.zip /opt/oracle/instantclient/instantclient-sdk-linux.x64-11.2.0.4.0.zip
#RUN cd /opt/oracle/instantclient
#RUN echo "Descompactando arquivos ..."
#RUN unzip instantclient-basic-linux.x64-11.2.0.4.0.zip
#RUN unzip instantclient-sdk-linux.x64-11.2.0.4.0.zip
#RUN echo "Atualizando diretorio ..."
#RUN mv instantclient*/* ./
#RUN rmdir instantclient*/
#RUN echo "Criando links ..."
#RUN ln -s libclntsh.so.* libclntsh.so
#RUN ln -s libocci.so.* libocci.so
#RUN echo "Configurando ..."
#RUN echo /opt/oracle/instantclient >> /etc/ld.so.conf
#RUN ldconfig
#RUN echo "Criando network-admin ..."
#RUN mkdir -p /opt/oracle/instantclient/network/admin
#RUN echo "Copiando arquivos network-admin ..."
#RUN cp $PATH_TMP_INSTALL/config/tnsnames.ora /opt/oracle/instantclient/network/admin/tnsnames.ora
#RUN cp $PATH_TMP_INSTALL/config/sqlnet.ora /opt/oracle/instantclient/network/admin/sqlnet.ora
#RUN cd $PATH_TMP_INSTALL

#RUN cd $PATH_TMP_INSTALL
#RUN echo "------------------------------------------------"
#RUN echo " Configuracao do OCI8"
#RUN echo "------------------------------------------------"

#RUN pear config-set http_proxy $PROXY
#RUN echo "Instalando oci8 ..."
#RUN pecl install oci8-2.0.11 #	instantclient,/opt/oracle/instantclient
#RUN echo "Criando oci.ini ..."
#RUN cp $PATH_TMP_INSTALL/config/oci8.ini /etc/php5/mods-available/oci8.ini
#RUN echo "Ativando extensions ..."
#RUN php5enmod oci8
#RUN cd $PATH_TMP_INSTALL

#RUN cd $PATH_TMP_INSTALL
#RUN echo "------------------------------------------------"
#RUN echo " Configuracao do PDO/OCI"
#RUN echo "------------------------------------------------"

#RUN echo "Corrigindo diretorios ..."
#RUN cd /usr/include/
#RUN ln -s php5 php
#RUN cd /opt/oracle/instantclient
#RUN mkdir -p include/oracle/11.1/
#RUN cd include/oracle/11.1/
#RUN ln -s ../../../sdk/include client
#RUN cd -
#RUN mkdir -p lib/oracle/11.1/client
#RUN cd lib/oracle/11.1/client
#RUN ln -s ../../../../ lib
#RUN cd -

#RUN echo "Atualizando pear.php.net ..."
#RUN pecl channel-update pear.php.net

#RUN echo "Baixando PDO/OCI ..."
#RUN mkdir -p /tmp/pear/download/
#RUN cp $PATH_TMP_INSTALL/pacotes/PDO_OCI-1.0.tgz /tmp/pear/download/PDO_OCI-1.0.tgz
#RUN cd /tmp/pear/download/
#RUN echo "Descompactando PDO/OCI ..."
#RUN tar xvf PDO_OCI-1.0.tgz
#RUN cd PDO_OCI-1.0
#RUN echo "Patch PDO/OCI config.m4 ..."
#RUN cp $PATH_TMP_INSTALL/config/config.m4.patch /tmp/pear/download/PDO_OCI-1.0/config.m4.patch
#RUN patch --dry-run -i config.m4.patch && patch -i config.m4.patch && phpize
#RUN echo "Patch PDO/OCI zend_function_entry ..."
#RUN rm /tmp/pear/download/PDO_OCI-1.0/pdo_oci.c
#RUN cp $PATH_TMP_INSTALL/config/pdo_oci.c /tmp/pear/download/PDO_OCI-1.0/pdo_oci.c

#RUN echo "Configurando, compilando e instalando ..."
#RUN ORACLE_HOME=/opt/oracle/instantclient ./configure --with-pdo-oci=instantclient,/opt/oracle/instantclient,11.1
#RUN make && make test && make install && mv modules/pdo_oci.so /usr/lib/php5/*+lfs/

#RUN echo "pdo_oci.ini ..."
#RUN cp $PATH_TMP_INSTALL/config/pdo_oci.ini /etc/php5/mods-available/pdo_oci.ini
#RUN echo "Ativando extensions ..."
#RUN php5enmod pdo_oci

#RUN cd $PATH_TMP_INSTALL

#RUN echo "------------------------------------------------"
#RUN echo " Inicializacao dos servicos"
#RUN echo "------------------------------------------------"	

#RUN chown -R www-data /var/www/html
#RUN echo "Habilitando mod_rewrite do apache ..."
#RUN a2enmod rewrite 
#RUN echo "Parando o apache ..."
#RUN service apache2 stop
#RUN echo "Iniciando o apache ..."
#RUN service apache2 start
