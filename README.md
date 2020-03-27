
# Agent
cd hinemos-agent
docker build -t hinemos/hinemos-agent:6.2.2-alpha -f Dockerfile .

# Hinemos Manager
cd hinemos-db
docker build -t hinemos/hinemos-db:6.2.2-alpha -f Dockerfile .
docker run --rm -it -p 24001:24001 hinemos/hinemos-db:6.2.2-alpha

cd hinemos-manager
docker build -t hinemos/hinemos-manager:6.2.2-alpha -f Dockerfile .
docker run --rm -it -e DB_HOST=172.17.0.1 -p 8080:8080 -p 8081:8081 hinemos/hinemos-manager:6.2.2-alpha


