FROM python:3.9-slim

RUN apt-get update && apt-get install -y curl

ARG NAME
ENV PIPENV_VENV_IN_PROJECT=1
ENV PIP_NO_CACHE_DIR=1
WORKDIR /usr/bin/${NAME}

COPY ./Pipfile* /usr/bin/${NAME}/
RUN pip install pipenv \
  && pipenv install --deploy

COPY . /usr/bin/${NAME}/

EXPOSE ${PORT}

RUN apt-get clean autoclean
RUN apt-get autoremove --yes
RUN rm -rf /var/lib/{apt,dpkg,cache,log}/

CMD pipenv run python app.py
