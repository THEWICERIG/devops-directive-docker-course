# get latest golang
FROM golang

# set working directory
WORKDIR /app

# COPY all
COPY . .

# download what we need
RUN go mod download

# run the main go file
CMD ["go", "run", "./main.go"]