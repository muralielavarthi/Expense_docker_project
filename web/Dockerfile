FROM nginx:alpine

# Install envsubst
RUN apk add --no-cache gettext

# Create non-root user
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Remove default config
RUN rm /etc/nginx/conf.d/default.conf

# Copy files
COPY nginx.conf /etc/nginx/nginx.conf.template
COPY index.html /usr/share/nginx/html/index.html

# Fix permissions
RUN chown -R appuser:appgroup /usr/share/nginx \
    /var/cache/nginx /var/run /etc/nginx

USER appuser

# Replace ENV variables at runtime
CMD /bin/sh -c "envsubst '\$NGINX_PORT \$BACKEND_PORT' < /etc/nginx/nginx.conf.template > /etc/nginx/nginx.conf && nginx -g 'daemon off;'"