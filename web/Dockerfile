FROM nginx:alpine

# Remove default site config
RUN rm -f /etc/nginx/conf.d/default.conf

# Copy ONLY the server block here
COPY default.conf /etc/nginx/conf.d/default.conf

# Copy static UI files
COPY static /usr/share/nginx/html

EXPOSE 80

