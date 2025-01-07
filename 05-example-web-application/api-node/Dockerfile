# use premade image  for node
FROM node:23-alpine

# Define a place all items will be installed to
WORKDIR /usr/src/app

# copy only package json files
# this layer will only be 
# invalidated if we change our dependencies
COPY package*.json ./

# grab all the dependencies
RUN npm install

# now copy only source code directory.
# doing this after npm install speeds
# up the build
COPY ./src .

# run the command 'npm run dev' upon launch of 
# image
CMD ["npm", "run", "dev"]