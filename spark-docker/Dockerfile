FROM apache/spark:3.5.1

USER root

# Atualiza e instala pip e dependências
RUN apt-get update && apt-get install -y python3-pip python3-dev \
    && pip3 install --upgrade pip

# Instala Jupyter Notebook e PySpark
RUN pip3 install notebook jupyterlab pyspark

# Ajusta permissões do usuário spark
RUN mkdir -p /home/spark && chown -R spark:spark /home/spark

USER spark
WORKDIR /opt/spark/apps