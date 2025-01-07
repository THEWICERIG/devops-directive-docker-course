# set os 
FROM ubuntu 

# set update and install nodejs, npm 
# (with an automated 'yes')
RUN apt update && apt install nodejs npm -y

# copy entire current directory into image
COPY . .

# grab all the dependencies
RUN npm install

# run the command 'npm run dev' upon launch of 
# image
CMD ["npm", "run", "dev"]