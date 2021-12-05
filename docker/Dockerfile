FROM node:8-alpine

RUN apk add --update --no-cache \
                            git \
                            libzmq \
                            zeromq-dev \
                            python \
                            make \
                            g++

WORKDIR /insight

# Copy weicore-node
RUN git clone --branch master --single-branch --depth 1 https://github.com/weicrypto/weicore-node.git .

# Copy config file
COPY weicore-node.json .

ARG VERSION

# Install npm packages
RUN npm ci

# Install Insight API module
RUN bin/weicore-node install @weicrypto/insight-api@${VERSION}

FROM node:8-alpine

#todo update the email
LABEL maintainer="Wei Developers <dev@dash.org>"
LABEL description="Dockerised Insight API"

WORKDIR /insight

# Copy project files
COPY --from=0 /insight/ .

EXPOSE 3001

CMD ["bin/weicore-node", "start"]
