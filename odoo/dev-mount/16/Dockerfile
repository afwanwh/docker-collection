FROM debian:bullseye-slim
LABEL maintainer="afwan.id"
SHELL ["/bin/bash", "-xo", "pipefail", "-c"]
ENV LANG C.UTF-8

RUN mkdir /opt/odoo-dir \
    && mkdir /opt/odoo-dir/odoo \
    && mkdir /opt/odoo-dir/extra-addons \
    && mkdir /opt/odoo-dir/data-dir \
    && mkdir /opt/odoo-dir/config

VOLUME ["/opt/odoo-dir/odoo", "/opt/odoo-dir/extra-addons", "/opt/odoo-dir/data-dir", "/opt/odoo-dir/config"]

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        dirmngr \
        fonts-noto-cjk \
        gnupg \
        libssl-dev \
        libpq-dev \
        node-less \
        npm \
        python3-dev \
        python3-babel \
        python3-chardet \
        python3-dateutil \
        python3-decorator \
        python3-docutils \
        python3-freezegun \
        python3-pil \
        python3-jinja2 \
        python3-libsass \
        python3-lxml \
        python3-num2words \
        python3-ofxparse \
        python3-passlib \
        python3-polib \
        python3-psutil \
        python3-psycopg2 \
        python3-pydot \
        python3-openssl \
        python3-pypdf2 \
        python3-qrcode \
        python3-renderpm \
        python3-reportlab \
        python3-requests \
        python3-stdnum \
        python3-tz \
        python3-vobject \
        python3-werkzeug \
        python3-xlsxwriter \
        python3-xlrd \
        python3-zeep \
    && curl -o wkhtmltox.deb -sSL https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.buster_amd64.deb \
    && echo 'ea8277df4297afc507c61122f3c349af142f31e5 wkhtmltox.deb' | sha1sum -c - \
    && apt-get install -y --no-install-recommends ./wkhtmltox.deb \
    && rm -rf /var/lib/apt/lists/* wkhtmltox.deb

RUN npm install -g rtlcss

ENTRYPOINT ["python3", "/opt/odoo-dir/odoo/odoo-bin", "-c", "/opt/odoo-dir/config/odoo.conf"]

EXPOSE 8069 8072
