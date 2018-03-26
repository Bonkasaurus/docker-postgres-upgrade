FROM postgres:9.4
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y locales
RUN locale-gen en_GB.UTF-8
ENV LANG en_GB.UTF-8
ENV LANGUAGE en_GB:en
ENV LC_ALL en_GB.UTF-8

RUN sed -i -e 's/# en_GB.UTF-8 UTF-8/en_GB.UTF-8 UTF-8/' /etc/locale.gen && \
    sed -i -e 's/# en_GB.UTF-8 UTF-8/en_GB.UTF-8 UTF-8/' /etc/locale.gen && \
    locale-gen && \
    update-locale LANG=en_GB.UTF-8 && \
    echo "LANGUAGE=en_GB.UTF-8" >> /etc/default/locale && \
    echo "LC_ALL=en_GB.UTF-8" >> /etc/default/locale
    
RUN apt-get update && apt-get install -y postgresql-9.4-postgis-2.3=2.3.3+dfsg-1.pgdg80+1