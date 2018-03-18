FROM openshift/base-centos7
MAINTAINER Veer Muchandi veer@redhat.com

RUN  rpm --import https://packages.microsoft.com/keys/microsoft.asc && curl -o /etc/yum.repos.d/mssql-release.repo https://packages.microsoft.com/config/rhel/7/prod.repo && ACCEPT_EULA=Y yum install -y msodbcsql mssql-tools unixODBC-devel && yum clean all -y
RUN yum install telnet -y
RUN useradd -M 1001

ADD ./init.sh ./
RUN chown 1001:1001 init.sh && chmod +w init.sh

USER 1001
EXPOSE 8080
CMD ["./init.sh"]
