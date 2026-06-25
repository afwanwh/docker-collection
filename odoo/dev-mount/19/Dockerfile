FROM ubuntu:noble
LABEL maintainer="afwan.id"
SHELL ["/bin/bash", "-xo", "pipefail", "-c"]
ENV LANG=C.UTF-8

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
        python3-geoip2 \
        python3-pil \
        python3-jinja2 \
        python3-libsass \
        python3-lxml-html-clean \
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
        python3-rjsmin \
        python3-stdnum \
        python3-tz \
        python3-vobject \
        python3-werkzeug \
        python3-xlsxwriter \
        python3-xlrd \
        python3-zeep \
        python3-magic \
        python3-odf \
        python3-pdfminer \
        python3-pip \
        python3-phonenumbers \
        python3-pyldap \
        python3-setuptools \
        python3-slugify \
        python3-watchdog \
        python3-xlwt \
        xz-utils \
    && curl -o wkhtmltox.deb -sSL https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6.1-3/wkhtmltox_0.12.6.1-3.jammy_amd64.deb \
    && echo '967390a759707337b46d1c02452e2bb6b2dc6d59 wkhtmltox.deb' | sha1sum -c - \
    && apt-get install -y --no-install-recommends ./wkhtmltox.deb \
    && rm -rf /var/lib/apt/lists/* wkhtmltox.deb

# install latest postgresql-client
RUN echo 'deb http://apt.postgresql.org/pub/repos/apt/ noble-pgdg main' > /etc/apt/sources.list.d/pgdg.list \
    && GNUPGHOME="$(mktemp -d)" \
    && export GNUPGHOME \
    && repokey='B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8' \
    && gpg --batch --keyserver keyserver.ubuntu.com --recv-keys "${repokey}" \
    && gpg --batch --armor --export "${repokey}" > /etc/apt/trusted.gpg.d/pgdg.gpg.asc \
    && gpgconf --kill all \
    && rm -rf "$GNUPGHOME" \
    && apt-get update  \
    && apt-get install --no-install-recommends -y postgresql-client \
    && rm -f /etc/apt/sources.list.d/pgdg.list \
    && rm -rf /var/lib/apt/lists/*

RUN npm install -g rtlcss

ENTRYPOINT ["python3", "/opt/odoo-dir/odoo/odoo-bin", "-c", "/opt/odoo-dir/config/odoo.conf"]

EXPOSE 8069 8071 8072
