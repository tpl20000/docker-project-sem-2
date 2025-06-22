# Prepare builder
FROM node:23.3-alpine AS builder

# apparently this needs to be set, otherwise we an error "ERR_OSSL_EVP_UNSUPPORTED"
# REMINDER!!!: this is a security risk
ENV NODE_OPTIONS=--openssl-legacy-provider
ENV NODE_ENV=PRODUCTION

WORKDIR /app
COPY package*.json .
RUN npm ci
COPY . .

# Build
RUN npm run build

# Prepare runner
FROM nginxinc/nginx-unprivileged
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/dist /usr/share/nginx/html
USER nginx
EXPOSE 80

# Run nginx
CMD ["nginx", "-g", "daemon off;"]