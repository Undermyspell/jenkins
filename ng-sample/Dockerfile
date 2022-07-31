FROM node:18-alpine As development
WORKDIR /app
COPY package*.json /app/
RUN npm ci

FROM node:18-alpine As build
WORKDIR /app
COPY package*.json ./
COPY --from=development /app/node_modules ./node_modules
COPY . .
RUN npm run build

ENV NODE_ENV=production
RUN npm ci --omit=dev --omit=optional && npm cache clean --force

FROM nginx:stable

COPY ../nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/dist/ng-sample /usr/share/nginx/html

WORKDIR /app

RUN chown -R nginx:nginx /app && chmod -R 755 /app && \
  chown -R nginx:nginx /var/cache/nginx && \
  chown -R nginx:nginx /var/log/nginx && \
  chown -R nginx:nginx /etc/nginx/conf.d

RUN touch /var/run/nginx.pid && \
  chown -R nginx:nginx /var/run/nginx.pid

USER nginx

CMD ["nginx", "-g", "daemon off;"]
