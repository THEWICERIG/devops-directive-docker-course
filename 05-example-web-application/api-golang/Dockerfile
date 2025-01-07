# get alpine golang
FROM golang:1.23.4-alpine

# set working directory
WORKDIR /app

# COPY dependency files
COPY go.mod go.sum ./

# download what we need
RUN go mod download

# COPY all
COPY . .

# build go file
RUN go build -o api-golang

# run the main go file, now faster
CMD ["./api-golang"]