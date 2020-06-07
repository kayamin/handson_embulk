# embulk は java8 のみサポート
FROM openjdk:8

# 公式githubの手順でembulk をインストール https://github.com/embulk/embulk
RUN curl --create-dirs -o /usr/local/bin/embulk -L "https://dl.embulk.org/embulk-latest.jar"

RUN chmod +x /usr/local/bin/embulk

# 公式githubの手順でdigdag をインストール https://docs.digdag.io/getting_started.html
RUN curl --create-dirs -o /usr/local/bin/digdag -L "https://dl.digdag.io/digdag-latest"

RUN chmod +x /usr/local/bin/digdag