FROM alpine:3.18.2 AS build

ARG TFLINT_VERSION=0.47.0
RUN set -eux \
    && if [ "$(uname -m)" = 'x86_64' ]; then \
        ARCH=amd64; \
    elif [ "$(uname -m)" = 'aarch64' ]; then \
        ARCH=arm64; \
    fi \
    \
    && wget --quiet "https://github.com/terraform-linters/tflint/releases/download/v${TFLINT_VERSION}/tflint_linux_${ARCH}.zip" \
    && unzip "tflint_linux_${ARCH}.zip" \
    && mv tflint /usr/bin/tflint \
    && chmod +x /usr/bin/tflint

FROM alpine:3.18.2
LABEL maintainer='Anton Melekhin'

RUN apk add --no-cache ca-certificates
COPY --from=build /usr/bin/tflint /usr/bin/tflint
