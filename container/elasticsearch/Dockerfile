FROM elasticsearch:7.9.3

ENV VERSION=7.9.3

# WORKDIR /usr/share/elasticsearch

# RUN ./bin/elasticsearch-plugin install -b https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v$VERSION/elasticsearch-analysis-ik-$VERSION.zip 
# RUN ./bin/elasticsearch-plugin install -b https://github.com/medcl/elasticsearch-analysis-pinyin/releases/download/v$VERSION/elasticsearch-analysis-pinyin-$VERSION.zip

COPY elasticsearch-analysis-ik-$VERSION.zip .
COPY elasticsearch-analysis-pinyin-$VERSION.zip .

RUN ./bin/elasticsearch-plugin install -b file:./elasticsearch-analysis-ik-$VERSION.zip
RUN ./bin/elasticsearch-plugin install -b file:./elasticsearch-analysis-pinyin-$VERSION.zip

# 修改elasticsearch用户的 UID GID 和 宿主机用户一致
RUN groupmod -g 1000 elasticsearch && usermod -u 1000 -g 1000 elasticsearch
