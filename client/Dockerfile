FROM node:alpine AS build
WORKDIR /app
COPY . .
RUN npm install
RUN npm run build
RUN npm run start

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html 
EXPOSE 3000
CMD ["nginx", "-g", "daemon off;"]
