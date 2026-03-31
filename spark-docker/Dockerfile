FROM eclipse-temurin:11-jdk

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
RUN pip3 install --break-system-packages --no-cache-dir jupyter pyspark==3.5.0 findspark

# Baixa o driver JDBC do PostgreSQL
RUN curl -L -o /opt/spark/jars/postgresql-42.7.3.jar https://jdbc.postgresql.org/download/postgresql-42.7.3.jar

# Baixa o conector MongoDB para Spark
RUN curl -L -o /opt/spark/jars/mongo-spark-connector_2.12-3.0.1.jar https://repo1.maven.org/maven2/org/mongodb/spark/mongo-spark-connector_2.12/3.0.1/mongo-spark-connector_2.12-3.0.1.jar

# Baixa dependências do conector MongoDB
RUN curl -L -o /opt/spark/jars/mongo-java-driver-3.12.14.jar https://repo1.maven.org/maven2/org/mongodb/mongo-java-driver/3.12.14/mongo-java-driver-3.12.14.jar \
    && curl -L -o /opt/spark/jars/bson-3.12.14.jar https://repo1.maven.org/maven2/org/mongodb/bson/3.12.14/bson-3.12.14.jar

# Cria diretório de trabalho
WORKDIR /opt/spark/apps

# Expõe porta do Jupyter Notebook
EXPOSE 8888

# Comando padrão ao iniciar o container
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root", "--NotebookApp.token=''"]

# Instala psycopg2-binary para conexão com PostgreSQL
RUN pip3 install --break-system-packages --no-cache-dir psycopg2-binary
