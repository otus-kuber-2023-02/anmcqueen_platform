FROM nginx:alpine
LABEL maintainer="asetorn@yandex.ru"
RUN mkdir /app && \
    addgroup -g 1001 node && \
    adduser -u 1001 -G node -s /bin/sh -D node && \
    chown -R 1001 /app && \
    chown -R 1001 /etc/nginx/conf.d/ && \
    chown -R 1001 /var/cache/nginx/
WORKDIR /app
ADD nginx.conf /etc/nginx/nginx.conf
EXPOSE 8000
USER 1001
