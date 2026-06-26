FROM node:20-alpine AS build

WORKDIR /usr/local/app

COPY package.json yarn.lock ./

RUN corepack enable && corepack prepare yarn@stable --activate
RUN yarn install --frozen-lockfile

COPY ./ .

RUN yarn build


FROM nginx:alpine AS production

COPY nginx.conf /etc/nginx/conf.d/default.conf

COPY --from=build /usr/local/app/dist/bobapp /usr/share/nginx/html

EXPOSE 80