FROM ubuntu:20.04
LABEL maintainer="afwan.id"

ENV LANG C.UTF-8

RUN mkdir /opt/odoo-dir \
    && mkdir /opt/odoo-dir/odoo \
    && mkdir /opt/odoo-dir/extra-addons \
    && mkdir /opt/odoo-dir/data-dir \
    && mkdir /opt/odoo-dir/config
VOLUME ["/opt/odoo-dir/odoo", "/opt/odoo-dir/extra-addons", "/opt/odoo-dir/data-dir", "/opt/odoo-dir/config"]

RUN ln -sf /usr/share/zoneinfo/Etc/UTC /etc/localtime

RUN apt update \
  && apt -yq install locales \
  && locale-gen en_US.UTF-8 \
  && update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8

RUN apt install -yq \
    curl \
    libjpeg62-dev \
    libjpeg-turbo8 \
    libxext6 \
    fontconfig \
    libldap2-dev \
    libsasl2-dev \
    libssl-dev \
    libxml2-dev \
    libxrender1 \
    libxslt1-dev \
    libpq-dev \
    postgresql-client \
    python-dev \
    python3-dev \
    python3-pip \
    sudo \
    zlib1g-dev \
    xfonts-base \
    xfonts-75dpi \
    npm

ADD https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.bionic_amd64.deb \
  /opt/wkhtmltox.deb

RUN dpkg -i /opt/wkhtmltox.deb

RUN npm install -g rtlcss

COPY requirements.txt /opt/requirements.txt

RUN pip3 install -r /opt/requirements.txt

ENTRYPOINT ["python3", "/opt/odoo-dir/odoo/odoo-bin", "-c", "/opt/odoo-dir/config/odoo.conf"]

EXPOSE 8069 8072
