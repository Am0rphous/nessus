<div align="center">

# Cracked Nessus in Docker

</div>

<br>

Work and creds goes to [elliot-bia](https://github.com/elliot-bia/). <a href="https://twitter.com/Elliot58616851" target="_blank"><img src="https://img.shields.io/twitter/follow/Elliot58616851?style=social"> </a>

<br>

Do not use it for illegal purposes. If any infringement, please create a new issue with the title "Infringement".



## Setup
````
docker pull ramisec/nessus
docker run -d --name=nessus -p 8834:8834 ramisec/nessus
docker exec -it nessus /bin/bash /nessus/update.sh
````

## Migration

If you need to migrate from old versions to new, use the following commands:

```bash
#Crate dir
mkdir ~/nessus_data

#Stop container
docker stop nessus

#copy data
docker cp nessus:/opt/nessus/var/nessus/ ~/nessus_data

#delete old container
docker rm nessus

#run new container
docker run -itd --name=nessus -v ~/nessus_data/nessus/:/opt/nessus/var/nessus/ -p 8834:8834 ramisec/nessus

#update plugins
docker exec -it nessus /bin/bash /nessus/update.sh
```

## Username & Password

Username: `admin`

Reset password by running `docker exec -it nessus /opt/nessus/sbin/nessuscli chpasswd`.
Output:
```
Login to change: admin 
New password: Password123!
New password (again): Password123!
Password changed for admin
```

