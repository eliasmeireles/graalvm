FROM ghcr.io/graalvm/jdk-community:24

# Set environment variables
ENV ANT_VERSION=1.10.14 \
    ANT_HOME=/opt/ant \
    PATH=$PATH:/opt/ant/bin

# Install dependencies and Ant (using yum for Oracle Linux)
RUN microdnf install -y unzip && \
    curl -o apache-ant-${ANT_VERSION}-bin.tar.gz https://downloads.apache.org/ant/binaries/apache-ant-${ANT_VERSION}-bin.tar.gz && \
    tar -xzf apache-ant-${ANT_VERSION}-bin.tar.gz -C /opt && \
    ln -s /opt/apache-ant-${ANT_VERSION} /opt/ant && \
    rm apache-ant-${ANT_VERSION}-bin.tar.gz && \
    ant -version

# Set working directory inside the container
WORKDIR /app

# Copy your project files into the container
COPY . .