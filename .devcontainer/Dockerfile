ARG DOCKER_TAG=latest
FROM espressif/idf:${DOCKER_TAG}

ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8

# Instalar pip, pipx y enable-littlefs-cli
RUN apt-get update -y && apt-get install -y udev python3-pip git && \
    pip install --break-system-packages pipx && \
    pipx ensurepath && \
    pipx install --force git+https://github.com/PoleG97/enable-littlefs-cli.git && \
    echo 'export PATH="/root/.local/bin:$PATH"' >> /root/.bashrc && \
    echo 'alias enable_littlefs="enable-littlefs"' >> /root/.bashrc

# Asegurar PATH global para todas las sesiones
ENV PATH="/root/.local/bin:$PATH"

# Export automático del entorno ESP-IDF
RUN echo "source /opt/esp/idf/export.sh > /dev/null 2>&1" >> ~/.bashrc

ENTRYPOINT [ "/opt/esp/entrypoint.sh" ]
CMD ["/bin/bash", "-c"]
