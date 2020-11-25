FROM node:alpine
WORKDIR "/app"
COPY ./package.json ./
RUN npm install
COPY . .
# Build the app, so it can be put in the nginx server. 
RUN npm run build

FROM nginx
# Open port 3000 so the routing-nginx can talk to the client. 
EXPOSE 3000
# Overwrite the config of nginx
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

# Put the react code in the nginx to be served
COPY --from=0 /app/build /usr/share/nginx/html