FROM ruby:2.6.3-slim-stretch

WORKDIR /

COPY prepare-env.sh .

RUN set -x && \
    buildDeps1='git curl libpq-dev libcurl4-gnutls-dev cmake libxml2-dev gnupg pkg-config g++ libsqlite3-dev' && \
    buildDeps2='nodejs postgresql-10 memcached' && \
    apt-get -qq update && \
    apt-get -qq install $buildDeps1 && \
    curl -sL https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - && \
    echo "deb http://apt.postgresql.org/pub/repos/apt/ stretch-pgdg main" > /etc/apt/sources.list.d/pgdg.list && \
    curl -sL https://deb.nodesource.com/setup_11.x | /bin/bash - && \
    apt-get -qq install $buildDeps2 && \
    grep -q '^local\s' /etc/postgresql/10/main/pg_hba.conf || echo "local all all trust" | tee -a /etc/postgresql/10/main/pg_hba.conf && \
    sed -i.bak 's/\(^local\s*\w*\s*\w*\s*\)\(peer$\)/\1trust/' /etc/postgresql/10/main/pg_hba.conf

ENTRYPOINT ["/bin/bash", "-c", "-l"]