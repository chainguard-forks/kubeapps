# Copyright 2019-2024 the Kubeapps contributors.
# SPDX-License-Identifier: Apache-2.0

FROM mcr.microsoft.com/playwright:v1.48.1-jammy@sha256:8c8076751fb2936d5ca45eb75d5cfa1a6dc0e5b529f3643862649b7f0515bd3f
WORKDIR /app/

# Copy and install deps
COPY package.json yarn.lock /app/
RUN yarn install --frozen-lockfile

# Install browsers
RUN npx playwright install

# Note that the playwright config and the actual test files
# will be later passed via kubectl cp in runtime

CMD ["tail", "-f", "/dev/null"]
