#etapa 1 de recursos:
FROM node:20 AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
#Los siguientes argumentos quieren decir que se pueden pasar variables en tiempo de construccion
ARG API_HOST
ARG API_PORT
ARG API_BASE

ENV VITE_API_HOST=$API_HOST
ENV VITE_API_PORT=$API_PORT
ENV VITE_API_BASE=$API_BASE

RUN npm run build


#etapa 2 de imagen:
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
#comentario: Esta es una imagen de nginx que sirve una aplicacion construida con node.js
#comentario: La primera etapa construye la aplicacion y la segunda etapa sirve los archivos estaticos con nginx

