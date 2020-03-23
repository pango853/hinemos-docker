# 1. Install and get files with CentOS 7
FROM centos:7.7.1908 AS install-env
LABEL maintainer="Pango Chan <Pango853@gmail.com>"

RUN rpm -ivh https://github.com/hinemos/hinemos/releases/download/v6.2.2/hinemos-6.2-agent-6.2.2-1.el.noarch.rpm

## Build runtime with OpenJDK 8
FROM openjdk:8-jdk
LABEL maintainer="Pango Chan <Pango853@gmail.com>"

WORKDIR /opt
COPY --from=install-env /opt/hinemos_agent hinemos_agent

ENTRYPOINT ["/usr/local/openjdk-8/bin/java", "-Dhostname=$(hostname)", "-server", "-Xms32m", "-Xmx32m", "-Xss256k", "-Dhinemos.agent.conf.dir=/opt/hinemos_agent/conf", "-Dhinemos.agent.log.dir=/opt/hinemos_agent/var/log", "-XX:CMSInitiatingOccupancyFraction=75", "-XX:+UseCMSInitiatingOccupancyOnly", "-XX:+UseConcMarkSweepGC", "-XX:+CMSParallelRemarkEnabled", "-XX:+UseParNewGC", "-XX:+DisableExplicitGC", "-XX:SurvivorRatio=3", "-XX:MaxTenuringThreshold=15", "-XX:TargetSurvivorRatio=90", "-Xloggc:/opt/hinemos_agent/var/log/gc.log", "-XX:+UseGCLogFileRotation", "-XX:NumberOfGCLogFiles=5", "-XX:GCLogFileSize=10M", "-verbose:gc", "-XX:+PrintGCDetails", "-XX:+PrintGCTimeStamps", "-XX:+PrintClassHistogram", "-Dsun.net.inetaddr.ttl=0", "-Dsun.net.inetaddr.negative.ttl=1", "-XX:+HeapDumpOnOutOfMemoryError", "-XX:HeapDumpPath=/opt/hinemos_agent/var/log", "-cp", "/opt/hinemos_agent/lib/AgentWS.jar:/opt/hinemos_agent/lib/HinemosAgent.jar:/opt/hinemos_agent/lib/HinemosCommon.jar:/opt/hinemos_agent/lib/commons-logging-1.2.jar:/opt/hinemos_agent/lib/commons-codec-1.10.jar:/opt/hinemos_agent/lib/commons-cli-1.3.1.jar:/opt/hinemos_agent/lib/commons-io-2.5.jar:/opt/hinemos_agent/lib/log4j-1.2.17.jar:/opt/hinemos_agent/lib/jna-4.2.2.jar:/opt/hinemos_agent/lib/jna-platform-4.2.2.jar:/opt/hinemos_agent/lib/pcap4j-core-1.7.1.jar:/opt/hinemos_agent/lib/pcap4j-packetfactory-propertiesbased-1.7.1.jar:/opt/hinemos_agent/lib/pcap4j-packetfactory-static-1.7.1.jar:/opt/hinemos_agent/lib/slf4j-api-1.7.25.jar:/opt/hinemos_agent/conf", "com.clustercontrol.agent.Agent", "/opt/hinemos_agent/conf/Agent.properties"]

