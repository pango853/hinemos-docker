
# Hinemos Images

This collection of images is intended to provide an easy way to start with Hinemos for beginners.


# Supported tags and respective Dockerfile links
- 6.2.2-alpha ([hinemos-manager/Dockerfile](https://github.com/pango853/hinemos-docker/hinemos-manager/Dockerfile))
- ver.6.0.1, latest ([hinemos/Dockerfile](https://github.com/pango853/docker-images/blob/master/hinemos/Dockerfile))


# What is Hinemos?
Hinemos is an open source operations management system which provides a wide range of management features, including monitoring, job scheduling and infrastructure automation.

Click the links below to find the details.
[Hinemos - Wikipedia](https://wikipedia.org/wiki/Hinemos)
[Hinemos Portal (official)](http://www.hinemos.info/)


# Build It Yourself
## Hinemos Agent
```
cd hinemos-agent
docker build -t hinemos/hinemos-agent:6.2.2-alpha -f Dockerfile .
docker run --rm -it -p 24005:24005 hinemos/hinemos-agent:6.2.2-alpha
```

## Hinemos Manager
```
cd hinemos-db
docker build -t hinemos/hinemos-db:6.2.2-alpha -f Dockerfile .
docker run --rm -it -p 24001:24001 hinemos/hinemos-db:6.2.2-alpha
```

```
cd hinemos-manager
docker build -t hinemos/hinemos-manager:6.2.2-alpha -f Dockerfile .
docker run --rm -it -e DB_HOST=172.17.0.1 -p 8080:8080 -p 8081:8081 hinemos/hinemos-manager:6.2.2-alpha
```

Test it.
> curl http://127.0.0.1:8080/HinemosWS/RepositoryEndpoint?wsdl

## Hinemos Web Client

```
cd hinemos-web
docker build -t hinemos/hinemos-web:6.2.2-alpha -f Dockerfile .
docker run --rm -d -p 9090:80 hinemos/hinemos-web:6.2.2-alpha
```

Test it.
> curl http://127.0.0.1:9090/

# Problems

## syslog (TOACK)
```
[root@c4de27314ffa /]# rpm -ivh https://github.com/hinemos/hinemos/releases/download/v6.2.2/hinemos-6.2-agent-6.2.2-1.el.noarch.rpm
Retrieving https://github.com/hinemos/hinemos/releases/download/v6.2.2/hinemos-6.2-agent-6.2.2-1.el.noarch.rpm
Preparing...                          ################################# [100%]
Updating / installing...
   1:hinemos-6.2-agent-0:6.2.2-1.el   ################################# [100%]
/etc/rsyslog.conf and /etc/syslog.conf are not found. Please edit System Logger configuration reffering the Manual
```

## No LOG!!! (TODO)
```
docker run --rm -it hinemos/hinemos-agent:6.2.2-alpha
// Show nothing!!!
```

## Failed to init (RESOLVED)
```
[root@6bf582268c09 sbin]# cat ~/install.log.hinemos_manager
Because environment variable LANG is ,
the DB language is en.

file systems mounted
/dev/sda1 - /etc/hosts
database directory(/opt/hinemos/var/data) will be in partition ( / ).
file system contains log directory(/opt/hinemos/var/log) will be in partition ( / ).

Configuring files (hinemos.cfg, postgresql.conf, persistence.xml, selfcheck-service.properties)...Change of /etc/snmp/snmpd.conf is not required.
[OK]

Changing the permissions of files...[OK]

Initializing internal database...
checking database directory(/opt/hinemos/var/data)... done
checking current user(hinemos)... done
initializing database directory(/opt/hinemos/var/data)... done
...
```

CAUSE: LANGUAGE is empty
       > su -c "${HINEMOS_HOME}/sbin/db_init/pg_init.sh ${LANGUAGE}" - ${HINEMOS_OS_USER} >> ~/install.log.hinemos_manager 2>&1
SOLUTION: LANGUAGE rpm -ivh ...


# Disclaimer

Please feel free to use and enjoy. However I will not be responsible for any demage, cost or other liability, either directly or indirectly, caused by the use of this image and the relevant documents.

