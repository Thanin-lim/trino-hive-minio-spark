# ใช้ Python 3.8-slim-buster ตามที่ต้องการ
FROM python:3.8-slim-bullseye
USER root

# 1. ติดตั้ง System Dependencies
# เพิ่ม build-essential เพราะบางที pandas/numpy เวอร์ชั่นเก่าต้องการ GCC ในการ compile บน slim image
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    openjdk-11-jre-headless \
    curl \
    git \
    procps \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# ตั้งค่า ENV ของ Java (เพื่อให้ Spark หาเจอ)
ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
ENV PATH=$JAVA_HOME/bin:$PATH


RUN pip install --no-cache-dir \
    pyspark==3.5.0 \
    jupyterlab \
    notebook \
    pandas \
    numpy

# ตั้งค่า ENV ตามที่คุณระบุ
ENV PYSPARK_PYTHON=/usr/local/bin/python
ENV PYSPARK_DRIVER_PYTHON=/usr/local/bin/python

# 3. ตั้งค่า Workspace
WORKDIR /home/jovyan/work

# 4. Expose Port สำหรับ Jupyter (ปกติคือ 8888) และ Spark UI (4040)
EXPOSE 8888 4040

# 5. คำสั่งรัน Jupyter Lab เมื่อ Container เริ่มทำงาน
# --ip=0.0.0.0: ให้เข้าถึงได้จากนอก container
# --allow-root: จำเป็นเพราะเราใช้ USER root
# --no-browser: ไม่ต้องพยายามเปิด browser ใน container
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root", "--NotebookApp.token=''"]