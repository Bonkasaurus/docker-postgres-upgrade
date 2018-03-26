FROM postgres:9.6



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

RUN sed -i 's/$/ 9.4/' /etc/apt/sources.list.d/pgdg.list

RUN apt-get update && apt-get install -y --no-install-recommends \
		postgresql-9.4=9.4.17-1.pgdg80+1 \
		postgresql-contrib-9.4=9.4.17-1.pgdg80+1 \
		postgresql-9.4-postgis-2.2=2.2.2+dfsg-7~137.gite11228b.pgdg80+1 \
		postgresql-9.6-postgis-2.3=2.3.3+dfsg-1.pgdg80+1 \
		postgresql-9.4-postgis-2.3=2.3.3+dfsg-1.pgdg80+1 \
	&& rm -rf /var/lib/apt/lists/*

ENV PGBINOLD /usr/lib/postgresql/9.4/bin
ENV PGBINNEW /usr/lib/postgresql/9.6/bin

ENV PGDATAOLD /var/lib/postgresql/9.4/data
ENV PGDATANEW /var/lib/postgresql/9.6/data

RUN mkdir -p "$PGDATAOLD" "$PGDATANEW" \
	&& chown -R postgres:postgres /var/lib/postgresql

WORKDIR /var/lib/postgresql

COPY docker-upgrade /usr/local/bin/

ENTRYPOINT ["docker-upgrade"]

# recommended: --link
CMD ["pg_upgrade"]
