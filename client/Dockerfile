# Use an existing docker image as a base for building phase
FROM node:alpine AS builder

WORKDIR /app
COPY ./package.json ./
RUN npm install           

COPY . .
# Tell the image what to do when it starts as a container   # Build and run only used in Dev
#CMD ["npm","run", "start"]                                 # Just build for Prod
RUN npm run build

# Use a web server image.  Doc on docker Hub is the basis for how to use these images
# Deploying to AWS EBS requires the port exposure to be specified
FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/share/nginx/html

