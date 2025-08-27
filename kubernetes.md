# Kubernetes
Guide for DO Kubernetes


### Alternative DB Copy 
Coping a DB to a dump to be excuted on mariaDB

```
# copy to the DB pod
kubectl cp -n wordpress `
  "C:\Users\KezNorbury\OneDrive - The Family Chemist\Desktop\TFC  Development\TFC Old Website\tfc-kubernetes\mysql\zrahhqqqse-20250126-0327.sql" `
  wordpress-kubernetes-mariadb-0:/tmp/dump.sql

# run the import in the DB pod
kubectl exec -n wordpress -it wordpress-kubernetes-mariadb-0 -- bash -lc `
  'mysql -u "<DB_USER>" -p"<DB_PASSWORD>" "<DB_NAME>" < /tmp/dump.sql'
```
