# MSSQL Command Line in a Container

This is a simple container that includes CLI for Microsoft SQLServer. It is useful if you want to connect to a MS SQLServer database from a container running on OpenShift.

This is also available as built container on DockerHub (docker.io/veermuchandi/mssqlcli) that can be deployed as

```
$ oc new-app docker.io/veermuchandi/mssqlcli
```
**NOTE** Administrator needs to add `nonroot` SCC to the service account being used to deploy this container.

Once deployed, you can `rsh` into the pod and connect to the database as follows:

```
$ /opt/mssql-tools/bin/sqlcmd -S <databaseserver> -U <user> -P <password> -d <database>
 
```
