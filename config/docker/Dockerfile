FROM node:18-alpine AS BUILD_IMAGE

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
COPY package.json yarn.lock ./
RUN yarn install --frozen-lockfile

# Copy app source
COPY . .

# Bundle app source
ENV NODE_ENV=production
ENV GENERATE_SOURCEMAP=false
RUN yarn build

FROM nginx:1-alpine

# Copy build
COPY --from=BUILD_IMAGE /usr/src/app/dist  /usr/share/nginx/html

# Copy nginx config
COPY config/docker/nginx.conf /etc/nginx/conf.d/default.conf
