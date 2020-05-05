# stage1 as builder
FROM node:12-alpine as builder
# install anguler cli
RUN npm i -g @angular/cli@8.3.22
# set work directory
WORKDIR /Appplication
# copy the package.json to install dependencies
COPY . /Appplication
# Install the dependencies and make the folder
RUN npm install
# Build the project and copy the files
RUN npm run build

# build nginx docker image
FROM nginx:alpine
# copy nginx config file
COPY ./.nginx/nginx.conf /etc/nginx/nginx.conf
## Remove default nginx index page
RUN rm -rf /usr/share/nginx/html/*
# Copy from the stahg 1
COPY --from=builder /Appplication/dist/safa-online /usr/share/nginx/html
#expose port 80 to use from out of docker
EXPOSE 80
# run nginx
ENTRYPOINT ["nginx", "-g", "daemon off;"]

