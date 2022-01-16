FROM python:3.9.9-bullseye
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

RUN pip install --upgrade pip

WORKDIR /app
COPY . .

RUN pip install -r requirements.txt
  
COPY lib_catalog .

RUN sed -i 's/ALLOWED_HOSTS = \[\]/ALLOWED_HOSTS = \[\"\*\"\]/g' lib_catalog/settings.py && \
    echo >> lib_catalog/settings.py && \
    echo CORS_ORIGIN_ALLOW_ALL = True >> lib_catalog/settings.py

EXPOSE 8000

CMD python manage.py migrate && python manage.py runserver 0.0.0.0:8000