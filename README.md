
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


# Disclaimer

Please feel free to use and enjoy. However I will not be responsible for any demage, cost or other liability, either directly or indirectly, caused by the use of this image and the relevant documents.

