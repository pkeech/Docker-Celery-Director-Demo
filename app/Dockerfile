## BASE IMAGE
FROM python:3.8.2-slim-buster AS Builder
RUN apt-get update && apt-get upgrade -y && apt-get install -y curl gnupg2 gcc
WORKDIR /app/

## IMAGE DEPENDENCIES
FROM Builder AS Dependencies

## APPLICATION DEPENDENCIES
COPY requirements.txt /app/requirements.txt
RUN pip install -r requirements.txt
COPY ./src /app

## DEV IMAGE
FROM Dependencies AS Development
LABEL Maintainer="Peter Keech <pkeech@ngds.com>"
ENV DIRECTOR_HOME="/app"
RUN director init .
RUN director db upgrade
EXPOSE 8083
CMD ["director","webserver","-b", "0.0.0.0:8083"]