FROM openjdk:8

# Variáveis do Spark
ENV SPARK_VERSION=3.5.0 \
    HADOOP_VERSION=3 \
    SPARK_HOME=/opt/spark \
    PATH=$PATH:/opt/spark/bin

# Instala dependências + Python + pip
RUN apt-get update && apt-get install -y \
    curl \
    python3 \
    python3-pip \
    && rm -rf /var/lib/apt/lists/*

# Baixa e instala o Spark
RUN curl -sL https://archive.apache.org/dist/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz \
    | tar -xz -C /opt \
    && mv /opt/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} /opt/spark

# Instala Jupyter e PySpark compatível com Spark 3.5.0
RUN pip3 install --no-cache-dir jupyter pyspark==3.5.0 findspark

# Cria diretório de trabalho
WORKDIR /opt/spark/apps

# Expõe porta do Jupyter Notebook
EXPOSE 8888

# Comando padrão ao iniciar o container
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root", "--NotebookApp.token=''"]
