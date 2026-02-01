FROM apache/spark:3.5.0-scala2.12-java11-ubuntu

USER root

# 1. Install lsb-release FIRST so add-apt-repository works
RUN apt-get update && \
    apt-get install -y software-properties-common gnupg2 curl lsb-release && \
    add-apt-repository -y ppa:deadsnakes/ppa && \
    apt-get update && \
    # 2. Install Python 3.11
    apt-get install -y python3.11 python3.11-distutils python3-pip && \
    # 3. Clean up apt cache to keep image small
    rm -rf /var/lib/apt/lists/*

# 4. Install pip specifically for 3.11 using the get-pip script
RUN curl -sS https://bootstrap.pypa.io/get-pip.py | python3.11

# 5. Install PySpark (Ensure it matches the image Spark version)
RUN python3.11 -m pip install pyspark==3.5.0

# 6. Configure Spark to use Python 3.11 explicitly
# We do not need to symlink /usr/bin/python3 (which breaks system tools)
# These env vars tell Spark exactly which binary to run.
ENV PYSPARK_PYTHON=/usr/bin/python3.11
ENV PYSPARK_DRIVER_PYTHON=/usr/bin/python3.11

USER spark
WORKDIR /opt/spark