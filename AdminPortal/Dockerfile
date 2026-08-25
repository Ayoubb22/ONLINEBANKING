FROM node:8 AS build
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
RUN npm run build -- --prod --aot=false

FROM nginx:1.17-alpine
COPY --from=build /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
