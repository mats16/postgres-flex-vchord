FROM flyio/postgres-flex:17.2

# 必要に応じて変えられるように ARG にしておく
ARG PG_MAJOR_VERSION=17
# VectorChord のリリースバージョン（GitHub Releases のタグに合わせて適宜更新）
ARG VCHORD_VERSION=1.0.0

# pgvector と VectorChord をインストール
RUN set -eux; \
    apt-get update; \
    # pgvector は Debian/Ubuntu 用の公式パッケージを利用
    apt-get install -y --no-install-recommends \
        wget \
        ca-certificates \
        postgresql-${PG_MAJOR_VERSION}-pgvector; \
    \
    # VectorChord の .deb を GitHub Releases から取得してインストール
    wget -O /tmp/postgresql-${PG_MAJOR_VERSION}-vchord.deb \
      "https://github.com/tensorchord/VectorChord/releases/download/${VCHORD_VERSION}/postgresql-${PG_MAJOR_VERSION}-vchord_${VCHORD_VERSION}-1_$(dpkg --print-architecture).deb"; \
    apt-get install -y --no-install-recommends \
      /tmp/postgresql-${PG_MAJOR_VERSION}-vchord.deb; \
    \
    # キャッシュ掃除
    rm -f /tmp/postgresql-${PG_MAJOR_VERSION}-vchord.deb; \
    rm -rf /var/lib/apt/lists/*
