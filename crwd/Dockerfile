# pull official base image
FROM python:3.9

# set work directory
WORKDIR /usr/src/app

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
# ENV POETRY_VIRTUALVENVS_IN_PATH 1
ENV POETRY_VIRTUALVENVS_CREATE 0
ENV POETRY_VERSION 1.1.9

# system deps
RUN pip install "poetry==$POETRY_VERSION"

# install dependencies
# RUN pip install --upgrade pip
# COPY ./requirements.txt .
# RUN pip install -r requirements.txt

# copy project
COPY . .
RUN make dev
