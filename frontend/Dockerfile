FROM node:20.8.0 as build

WORKDIR /app
COPY package.json package-lock.json ./
RUN npm install --legacy-peer-deps
COPY . ./

ARG API_URL
ARG GOOGLE_AUTH_CLIENT_ID
ARG CLOUDINARY_CLOUD_NAME
ENV REACT_APP_API_URL=$API_URL
ENV REACT_APP_GOOGLE_AUTH_CLIENT_ID=$GOOGLE_AUTH_CLIENT_ID
ENV REACT_APP_CLOUDINARY_CLOUD_NAME=$CLOUDINARY_CLOUD_NAME

RUN npm run build


FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html

COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
