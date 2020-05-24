# embulk は java8 のみサポート
FROM openjdk:8

# 公式githubの手順でembulk をインストール https://github.com/embulk/embulk
RUN curl --create-dirs -o ~/.embulk/bin/embulk -L "https://dl.embulk.org/embulk-latest.jar"

RUN chmod +x ~/.embulk/bin/embulk

ENV PTH ~/.embulk/bin:$PATH