# Microsoft SQLServer Tools for OpenShift

1. [MSSQL Client](https://github.com/VeerMuchandi/mssql-openshift-tools/tree/master/mssql-client) : Deploy this container on OpenShift, `rsh` into the container and run `sqlcmd` CLI to connect to a SQL Server database
2. [PHP7 enhanced with MSSQL](https://github.com/VeerMuchandi/mssql-openshift-tools/tree/master/php7-mssql): Connect to MSSQL from a PHP Application.


These images needs to run as a specific user as both `sqlcmd` and `sqlsrv_connect` expect a user added on the system (not a random user). So to use these images your administrator needs to grant relevant access. As an example if you are deploying the application to `mstest` project, your administrator can add a `nonroot` SCC context as follows:

```
#  oc patch scc nonroot -p "priority: 6"
securitycontextconstraints "nonroot" patched
```

```
# oc adm policy add-scc-to-user nonroot system:serviceaccount:mstest:default
scc "nonroot" added to: ["system:serviceaccount:mstest:default"]
# oc adm policy add-scc-to-user nonroot system:serviceaccount:mstest:builder
scc "nonroot" added to: ["system:serviceaccount:mstest:builder"]
```
 
