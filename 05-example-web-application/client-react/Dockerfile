# from 2:03:26

# Using bullseye, which is bigger than alpine
# but we will jsut use it for build
FROM node:23-bullseye AS build

# set work directory on iamge
WORKDIR /usr/src/app

# copy initially only the package info we need
COPY package*.json ./

# Use cache mount to speed up install of existing dependencies
RUN --mount=type=cache,target=/usr/src/app/.npm \
  npm set cache /usr/src/app/.npm && \
  npm ci


# copy everything
COPY . .

# will generate set of static files we can serve
RUN npm run build

###

# using nginx unprivileged for release so we can use non-root user
FROM nginxinc/nginx-unprivileged:alpine3.20-perl

# copy in nginx conf to serve the site for how we want it to
COPY nginx.conf /etc/nginx/conf.d/default.conf

# copy over static files to stnadard place
# to store nginx files
COPY --from=build usr/src/app/dist/ /usr/share/nginx/html

# due to unprivledged nginx we have to have port > 1000
EXPOSE 8080

# start app
CMD ["npm", "run", "dev"]