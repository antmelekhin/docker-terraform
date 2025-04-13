FROM alpine:3.18.2 AS build

ARG TF_VERSION=1.5.4
RUN set -eux \
    && if [ "$(uname -m)" = 'x86_64' ]; then \
        ARCH=amd64; \
    elif [ "$(uname -m)" = 'aarch64' ]; then \
        ARCH=arm64; \
    fi \
    \
    && wget --quiet "https://releases.hashicorp.com/terraform/${TF_VERSION}/terraform_${TF_VERSION}_linux_${ARCH}.zip" \
    && unzip "terraform_${TF_VERSION}_linux_${ARCH}.zip" \
    && mv terraform /usr/bin/terraform \
    && chmod +x /usr/bin/terraform

ARG TG_VERSION=0.48.5
RUN set -eux \
    && if [ "$(uname -m)" = 'x86_64' ]; then \
        ARCH=amd64; \
    elif [ "$(uname -m)" = 'aarch64' ]; then \
        ARCH=arm64; \
    fi \
    \
    && wget --quiet "https://github.com/gruntwork-io/terragrunt/releases/download/v${TG_VERSION}/terragrunt_linux_${ARCH}" \
    && mv "terragrunt_linux_${ARCH}" /usr/bin/terragrunt \
    && chmod +x /usr/bin/terragrunt

FROM alpine:3.18.2
LABEL maintainer='Anton Melekhin'

RUN apk add --no-cache ca-certificates
COPY --from=build /usr/bin/terraform /usr/bin/terraform
COPY --from=build /usr/bin/terragrunt /usr/bin/terragrunt
