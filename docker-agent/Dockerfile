# Base Image
FROM ubuntu:latest

# Set environment variables
ENV JAVA_VERSION=17 \
    MAVEN_VERSION=3.8.8 \
    DOCKER_VERSION=24.0.5

# Update and install prerequisites
RUN apt-get update && \
    apt-get install -y \
    curl \
    wget \
    gnupg \
    lsb-release \
    apt-transport-https \
    ca-certificates \
    software-properties-common && \
    rm -rf /var/lib/apt/lists/*

# Install OpenJDK
RUN apt-get update && \
    apt-get install -y openjdk-${JAVA_VERSION}-jdk && \
    java -version

# Install Maven
RUN wget https://archive.apache.org/dist/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz && \
    tar -xvzf apache-maven-${MAVEN_VERSION}-bin.tar.gz -C /opt && \
    ln -s /opt/apache-maven-${MAVEN_VERSION}/bin/mvn /usr/bin/mvn && \
    rm apache-maven-${MAVEN_VERSION}-bin.tar.gz && \
    mvn -version

# Install Docker
# RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - && \
#     add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" && \
#     apt-get update && \
#     apt-get install -y docker-ce=${DOCKER_VERSION}~3-0~ubuntu-$(lsb_release -cs) && \
#     docker --version

# Add Docker's official GPG key
RUN install -m 0755 -d /etc/apt/keyrings && \
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc && \
    chmod a+r /etc/apt/keyrings/docker.asc

# Add Docker repository to Apt sources
RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
    tee /etc/apt/sources.list.d/docker.list > /dev/null && \
    apt-get update

# Install Docker
RUN apt-get install -y docker-ce docker-ce-cli containerd.io && \
    docker --version


# Start Docker Daemon (optional for container environment)
CMD ["dockerd"]

# FROM maven:3.8.3-openjdk-17
# RUN apt update && apt install -y docker.io
