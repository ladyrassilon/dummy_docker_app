FROM python:3.11-alpine

RUN pip install --upgrade pip

RUN apk add curl

RUN adduser -D appuser
RUN mkdir -p /var/app/code/
RUN mkdir -p /var/app/log/
RUN touch /var/app/log/stout.log && touch /var/app/log/sterr.log
RUN chown -R appuser:appuser /var/app

WORKDIR /var/app/code

USER appuser

COPY --chown=appuser:appuser ./src/ .

ENV VIRTUAL_ENV=/var/app/env

RUN python -m venv $VIRTUAL_ENV

ENV PATH="$VIRTUAL_ENV/bin:$PATH"

RUN export FLASK_APP=app.py

RUN pip install -r requirements.txt

EXPOSE 5000

CMD ["python", "app.py"]