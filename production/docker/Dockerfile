FROM alpine:3.20 AS source

ARG REPO_URL=https://github.com/christroutner/pos-cash.git
ARG REPO_REF=master

RUN apk add --no-cache git

WORKDIR /src
RUN git clone --depth 1 --branch "${REPO_REF}" "${REPO_URL}" pos-cash

FROM nginx:1.27-alpine

COPY --from=source /src/pos-cash/www/ /usr/share/nginx/html/

EXPOSE 80
