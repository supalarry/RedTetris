# ---- Build phase
# Use base OS, install dependencies and then run "npm run build"
# to create production ready file folder.

FROM node:alpine as builder
# here we tagged this phase "as builder"
WORKDIR '/app'
COPY package.json .
RUN yarn install
COPY . .
# Because this is for production, we just COPY . . all source code. We do not
# need to setup any volumes to reflect changes in source files anymore.
RUN yarn build
# This build folder will be created in /app/build



# ---- Run phase
# Here, we use nginx as base OS and simply copy build final folder on it from
# build phase. Everything else gets dropped.
FROM nginx
# as we start writing FROM, docker understands that this is a new block
EXPOSE 80
# because when we run web app from command line, we map ports.
COPY --from=builder /app/build /usr/share/nginx/html
# what we are saying here is that from builder phase /app/build folder we want
# to copy everything to nginx folder that serves user by default
# ngnx does not need RUN command because it runs automatically