# get buster golang, using docker stages
# stages allow for diff environments to
# be used to build and to release
FROM golang:1.23.4-bullseye as build

# set working directory
WORKDIR /app

# COPY dependency files
COPY go.mod go.sum ./

# Use cache mount to speed up install of
# existing dependencies
RUN --mount=type=cache,target=/go/pkg/mod \
  --mount=type=cache,target=/root/.cache/go-build \
  go mod download

# COPY all
COPY . .

# build go file with external linking and
# static building, so we can copy over
# to the scratch stage with dependencies
# built in
RUN go build \
  -ldflags="-linkmode external -extldflags -static" \
  -tags netgo \
  -o api-golang

# set up a non-root user
RUN useradd -u 1001 nonroot

###

# using official image that only has a valid root
# file system nothing else, menaing a smaller image
FROM scratch

# env variable for GIN, set to release
ENV GIN_MODE=release

# copy password file from build stage to copy
# ove rthe nonroot user
COPY --from=build /etc/passwd /etc/passwd

# copy form the build stage
COPY --from=build /app/api-golang api-golang

# Now use the nonroot user
USER nonroot

# Again, even if define din the app this is good
# documentation
EXPOSE 8080

# run the main go file, now faster
CMD ["./api-golang"]