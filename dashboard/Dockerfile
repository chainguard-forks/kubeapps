# Copyright 2018-2024 the Kubeapps contributors.
# SPDX-License-Identifier: Apache-2.0

FROM node:20.18.0@sha256:a7a3b7ec6de4b11bb2d673b31de9d28c6da09c557ee65453672c8e4f754c23fc AS build
WORKDIR /app

COPY package.json yarn.lock /app/
RUN yarn install --frozen-lockfile

RUN mkdir /app/src
COPY . /app
RUN yarn run prettier-check && yarn run ts-compile-check
RUN yarn run build

FROM bitnamilegacy/nginx:1.27.3-debian-12-r0@sha256:6ea5d37590b27b9f6cc1c5e23bbc6647de5558634963b6155fbeaec5e245caf2
COPY --from=build /app/build /app
