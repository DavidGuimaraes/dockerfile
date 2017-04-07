FROM ubuntu:16.04

MAINTAINER Rafael Ramos de Oliveira <roliveira@azi.com.br>

RUN apt-get update

RUN apt-get -y --force-yes install mc wget curl ssh unzip supervisor nginx redis-server software-properties-common

RUN echo 'deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main 9.5' >> /etc/apt/sources.list.d/postgresql.list

RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - && apt-get update && apt-get -y --force-yes install postgresql-9.5

RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && add-apt-repository ppa:webupd8team/java && apt-get update && apt-get install -y oracle-java8-installer

RUN rm -f /etc/nginx/conf.d/default.conf
ADD nginx/nginx.conf /etc/nginx/nginx.conf
ADD nginx/az /etc/nginx/az

RUN mkdir /opt/database
RUN mkdir /opt/database/create
RUN mkdir /opt/database/create/postgresql

ADD database/alter_role.sql /opt/database/alter_role.sql
ADD database/postgresql/01_database.sql /opt/database/create/postgresql/01_database.sql
ADD database/postgresql/02_efcaz.sql /opt/database/create/postgresql/02_efcaz.sql

RUN service postgresql start \
	&& su - postgres -c "createdb -E UTF8 -T template0 efcaz-test" \
	&& su - postgres -c "psql efcaz-test -f /opt/database/alter_role.sql" \
	&& su - postgres -c "psql efcaz-test -f /opt/database/create/postgresql/01_database.sql" \
	&& su - postgres -c "psql efcaz-test -f /opt/database/create/postgresql/02_efcaz.sql"

ADD database/pg_hba.conf /etc/postgresql/9.5/main/pg_hba.conf
ADD database/postgresql.conf /etc/postgresql/9.5/main/postgresql.conf

RUN chmod -x /etc/postgresql/9.5/main/pg_hba.conf
RUN chmod -x /etc/postgresql/9.5/main/postgresql.conf

RUN mkdir /opt/efcaz-api
ADD output/efcaz-api-desenv.jar /opt/efcaz-api/efcaz-api-desenv.jar
ADD config/application.properties /opt/efcaz-api/application.properties
ADD config/diagramaInicial.bpmn /opt/efcaz-api/diagramaInicial.bpmn

RUN mkdir /opt/repo_file
ADD config/repo_file /opt/repo_file

RUN mkdir /opt/efcaz
ADD output/efcaz /opt/efcaz

RUN mkdir /opt/auto-cadastro
ADD output/auto-cadastro /opt/auto-cadastro

ADD scripts/load-services.sh /opt/load-services.sh

EXPOSE 90 5432

RUN chmod +x /opt/load-services.sh
CMD /bin/bash -C './opt/load-services.sh'