# Copyright 2020-2024 the Kubeapps contributors.
# SPDX-License-Identifier: Apache-2.0

# syntax = docker/dockerfile:1

FROM rust:1.81.0@sha256:7b7f7ae5e49819e708369d49925360bde2af4f1962842e75a14af17342f08262 AS builder

WORKDIR /pinniped-proxy
ARG VERSION

# Create a release build of pinniped-proxy itself.
COPY ./cmd/pinniped-proxy ./
ENV PINNIPED_PROXY_VERSION=$VERSION
RUN --mount=type=cache,target=/usr/local/cargo/registry \
    --mount=type=cache,target=/pinniped-proxy/target \
    cargo build --release
RUN --mount=type=cache,target=/pinniped-proxy/target \
    cp /pinniped-proxy/target/release/pinniped-proxy /pinniped-proxy/pinniped-proxy

FROM bitnami/minideb:bookworm@sha256:f22253d95fb20ef63474ac93a82c7adf5dba80cb63d795f3687e2f54ea58c1d1
RUN apt-get update && apt-get install -y ca-certificates libssl3 && rm -rf /var/lib/apt/lists/*
COPY --from=builder /pinniped-proxy/pinniped-proxy /pinniped-proxy
ENV PATH="/:$PATH"

EXPOSE 3333
USER 1001
ENTRYPOINT [ "pinniped-proxy" ]
CMD [ "--help" ]
