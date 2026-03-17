FROM nginx:latest

EXPOSE 80

LABEL Project="Expense" \
      Author="Murali"

RUN rm -rf /usr/share/nginx/html/*
COPY ./code/* /usr/share/nginx/html/
COPY ./code/expense.conf /etc/nginx/conf.d/default.conf/

# Give ownership of the necessary directories to the nginx user
RUN chown -R nginx:nginx /var/cache/nginx \
    && chown -R nginx:nginx /var/run \
    && chown -R nginx:nginx /run \
    && chown -R nginx:nginx /usr/share/nginx/html \
    && chown -R nginx:nginx /etc/nginx/

# non-root user to run nginx
# nginx image already has a non-root user named 'nginx' with UID 101
USER nginx

CMD ["nginx", "-g", "daemon off;"]