FROM registry.access.redhat.com/rhscl/php-70-rhel7
MAINTAINER Veer Muchandi <veer@redhat.com>

USER root
RUN  rpm --import https://packages.microsoft.com/keys/microsoft.asc && \
     curl -o /etc/yum.repos.d/mssql-release.repo https://packages.microsoft.com/config/rhel/7/prod.repo && \
     ACCEPT_EULA=Y yum install -y msodbcsql mssql-tools unixODBC-devel && \
     wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
     wget http://rpms.remirepo.net/enterprise/remi-release-7.rpm && \
     rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm && \
     yum-config-manager --enable remi-php70 && \
     yum -y install php-pear php-devel  && \
     pear channel-update pear.php.net && \
     pecl channel-update pecl.php.net && \
     pecl install sqlsrv && \
     pecl install pdo_sqlsrv && \
     yum clean all -y && \
     rm -rf /var/cache/yum && \
     cp /usr/lib64/php/modules/sqlsrv.so /opt/rh/rh-php70/root/usr/lib64/php/modules/ && \
     cp /usr/lib64/php/modules/pdo_sqlsrv.so /opt/rh/rh-php70/root/usr/lib64/php/modules/ && \
     chmod +x /opt/rh/rh-php70/root/usr/lib64/php/modules/sqlsrv.so && \
     chmod +x /opt/rh/rh-php70/root/usr/lib64/php/modules/pdo_sqlsrv.so

RUN echo "extension=sqlsrv.so" >> /etc/opt/rh/rh-php70/php.d/30-sqlsrv.ini && \ 
    echo "extension=pdo_sqlsrv.so" >> /etc/opt/rh/rh-php70/php.d/30-pdo_sqlsrv.ini  

RUN  rpm --import https://packages.microsoft.com/keys/microsoft.asc && curl -o /etc/yum.repos.d/mssql-release.repo https://packages.microsoft.com/config/rhel/7/prod.repo && ACCEPT_EULA=Y yum install -y msodbcsql mssql-tools unixODBC-devel && yum -y install python-pip && pip install pymssql && yum clean all -y

RUN useradd -M 1001

USER 1001
