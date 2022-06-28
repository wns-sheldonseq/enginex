# Dockerfile

FROM python:3.8-slim-buster
# install nginx
RUN apt-get update && apt-get install nginx vim -y --no-install-recommends
COPY nginx.default /etc/nginx/sites-available/default
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

# copy source and install dependencies
RUN mkdir -p /opt/textextraction
RUN mkdir -p /opt/textextraction/pip_cache
RUN mkdir -p /opt/textextraction/app
COPY requirements.txt start-server.sh /opt/textextraction/
#COPY .pip_cache /opt/textextraction/pip_cache/
COPY app /opt/textextraction/app
WORKDIR /opt/textextraction
RUN pip install -r requirements.txt --cache-dir /opt/textextraction/pip_cache
#RUN chown -R www-data:www-data /opt/textextraction
RUN chmod 777 -R /opt/textextraction

# start server
EXPOSE 80
STOPSIGNAL SIGTERM
CMD ["/opt/textextraction/start-server.sh"]