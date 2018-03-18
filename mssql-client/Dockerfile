FROM openshift/base-centos7
MAINTAINER Veer Muchandi veer@redhat.com

RUN  rpm --import https://packages.microsoft.com/keys/microsoft.asc && curl -o /etc/yum.repos.d/mssql-release.repo https://packages.microsoft.com/config/rhel/7/prod.repo && ACCEPT_EULA=Y yum install -y msodbcsql mssql-tools unixODBC-devel && yum clean all -y
RUN yum install telnet -y

ADD ./init.sh ./
ADD ./uid_entrypoint.sh ./
RUN chown 1001:0 *.sh && chmod +wx *.sh

RUN chmod g=u /etc/passwd

USER 1001
EXPOSE 8080
ENTRYPOINT [ "./uid_entrypoint.sh" ]
CMD ["./init.sh"]
