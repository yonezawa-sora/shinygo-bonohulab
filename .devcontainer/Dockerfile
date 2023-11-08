# [Choice] R version: 4, 4.2, 4.1, 4.0
ARG VARIANT="4.1"
# [Choice] Base image. Minimal (r-ver), tidyverse installed (tidyverse), or full image (binder): rocker/r-ver, rocker/tidyverse, rocker/binder
ARG BASE_IMAGE="rocker/r-ver"
FROM ${BASE_IMAGE}:${VARIANT}

# 環境変数を設定
ENV DEBIAN_FRONTEND=noninteractive

# 必要なパッケージをインストール
RUN apt-get update && apt-get install -y --no-install-recommends \
    python3-pip \
    libgit2-dev \
    libcurl4-openssl-dev \
    libssl-dev \
    libxml2-dev \
    libxt-dev \
    libfontconfig1-dev \
    libcairo2-dev \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Pythonパッケージをインストール
RUN python3 -m pip --no-cache-dir install radian

# Rパッケージをインストール
RUN install2.r --error --skipinstalled --ncpus -1 \
    devtools \
    languageserver \
    httpgd

# 任意のユーザーを作成
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID
RUN groupadd --gid $USER_GID $USERNAME \
     && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
     && apt-get update \
     && apt-get install -y sudo \
     && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
     && chmod 0440 /etc/sudoers.d/$USERNAME

# 作業ディレクトリを設定
WORKDIR /workspace

# コンテナが起動したときに実行するコマンド（必要に応じて）
CMD ["bash"]