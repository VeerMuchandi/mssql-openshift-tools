# PHP7 S2I Image with MSSQL 

This image extends RedHat's PHP7 image to provide all dependencies to connect to Microsoft SQL Server using sqlsrv_connect().
Since this image extends a RHEL based imaged, you will need a RHEL host to run the `docker build`.

It also includes CLI (sqlcmd) in case you want to use command line interface to connect to SQL Server. If you want to make the image smaller you can remove the CLI part by elimnating the following section from the Dockerfile. 

```
RUN  rpm --import https://packages.microsoft.com/keys/microsoft.asc && curl -o /etc/yum.repos.d/mssql-release.repo https://packages.microsoft.com/config/rhel/7/prod.repo && ACCEPT_EULA=Y yum install -y msodbcsql mssql-tools unixODBC-devel && yum -y install python-pip && pip install pymssql && yum clean all -y
```

Sqlcmd requires the user running the command to be part of `/etc/passwd`. Hence the entrypoint has been changed to `uid_entrypoint` that adds the random user assigned by the user to `/etc/passwd` with username `container` when the container comes up. This allows container to be used with OpenShift.


## Building this container

You can build and push this image to OpenShift as follows

1. Create a project
```
$ oc new-project mstest
```

2. Log into Docker. If your OpenShift Registry is exposed, you can push it to the registry. 
```
$ oc whoami -t
COPYYOURTOKENDISPLAYEDHERE

$ docker login -u veer -p COPYYOURTOKENDISPLAYEDHERE <your docker-registry-url>`
```

3. Build the S2I image and push it to OpenShift Registry

```
$ docker build . -t docker-registry-default.apps.devday.ocpcloud.com/mstest/php7
$ docker push docker-registry-default.apps.devday.ocpcloud.com/mstest/php7
```

4. Check that the imagestream is created

```
$ oc get is -n mstest

NAME       DOCKER REPO                                        TAGS      UPDATED
php7       docker-registry.default.svc:5000/mstest/php7       latest    10 hours ago
```

## Using this image to deploy an application

Now you can deploy an application in the `mstest` project to your the customized S2I builder image as follows:

```
$ oc new-app mstest/php7~https://github.com/VeerMuchandi/testdb
```

