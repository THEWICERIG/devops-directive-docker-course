# from 1:59:15

# Using bullseye, which is bigger than alpine
# but we will jsut use it for build
FROM node:23-bullseye as build

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

# using nginx for release
FROM nginx:1.27.3-alpine

# copy in nginx conf to serve the site for how we want it to
COPY nginx.conf /etc/nginx/conf.d/default.conf

# copy over static files to stnadard place
# to store nginx files
COPY --from=build usr/src/app/dist/ /usr/share/nginx/html

EXPOSE 80

# start app
CMD ["npm", "run", "dev"]