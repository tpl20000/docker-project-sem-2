# Prepare builder
FROM node:23.3-alpine AS builder
RUN apk add --no-cache git
WORKDIR /app
COPY . .
RUN npm ci

# Build
RUN npm run build

# Prepare runner
FROM nginx:1.28-alpine
RUN apk add --no-cache ca-certificates tzdata && update-ca-certificates
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/dist /usr/share/nginx/html
#RUN adduser -D -g '' runner
#RUN touch /var/run/nginx.pid
#RUN mkdir /var/cache/nginx -p
#RUN chown -R runner:runner /var/run/nginx.pid
#RUN chown -R runner:runner /usr/share/nginx/html
#RUN chown -R runner:runner /etc/nginx/conf.d
#RUN chown -R runner:runner /var/log/nginx
#RUN chown -R runner:runner /var/cache/nginx
#USER runner
EXPOSE 80

# Run nginx
CMD ["nginx", "-g", "daemon off;"]