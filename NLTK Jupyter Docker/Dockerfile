FROM quantworks/four-horsemen:latest
LABEL maintainer="varad.s.tupe@gmail.com"

RUN mkdir /data

RUN apk add --no-cache --virtual .build-deps \
    python3-dev

COPY ./requirements.txt .
COPY ./install_nltk_popular.py .

RUN pip3 install --upgrade pip
RUN pip3 install -r ./requirements.txt
RUN python3 ./install_nltk_popular.py
RUN rm ./requirements.txt \
    && rm ./install_nltk_popular.py \
    && apk del .build-deps

