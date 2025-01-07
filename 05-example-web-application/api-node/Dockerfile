# use premade image  for node
FROM node:23-alpine

# Define a place all items will be installed to
WORKDIR /usr/src/app

# Node applications look for environment variable
# $NODE_ENV, which if set to 'production' will
# ensure node isn't run in dev mode
ENV NODE_ENV=production

# copy only package json files
# this layer will only be 
# invalidated if we change our dependencies
COPY package*.json ./

# clean install (ci) of only production 
# dependencies
RUN npm ci --only=production

# execute as non-root user for security
# the node buo;d has built in user 'node'
USER node

# now copy only source code directory.
# assign everything to user 'node'
COPY --chown=node:node ./src .

# run the command 'node index.js' upon launch of 
# image
CMD ["node", "index.js"]