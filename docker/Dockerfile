FROM node:lts-alpine
LABEL maintainer="drew0531"
ARG QL_URL=https://github.com/drew0531/3321.git
ARG QL_BRANCH=master
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin \
    LANG=zh_CN.UTF-8 \
    SHELL=/bin/bash \
    PS1="\u@\h:\w \$ " \
    QL_DIR=/ql
WORKDIR ${QL_DIR}
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && apk update -f \
    && apk upgrade \
    && apk --no-cache add -f bash \
                             coreutils \
                             moreutils \
                             git \
                             curl \
                             wget \
                             tzdata \
                             perl \
                             openssl \
                             nginx \
                             python3 \
                             jq \
                             openssh \
                             build-base \
                             g++ \
                             cairo-dev \
                             pango-dev \
                             giflib-dev \
                             zlib-dev \
                             gcc \
                             jpeg-dev \
                             python3-dev \
                             musl-dev \
                             freetype-dev \
    && rm -rf /var/cache/apk/* \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && touch ~/.bashrc \
    && mkdir /run/nginx \
    && git clone -b ${QL_BRANCH} ${QL_URL} ${QL_DIR} \
    && git config --global user.email "qinglong@@users.noreply.github.com" \
    && git config --global user.name "qinglong" \
    && git config --global pull.rebase true \
    && cd ${QL_DIR} \
    && cp -f .env.example .env \
    && chmod 777 ${QL_DIR}/shell/*.sh \
    && chmod 777 ${QL_DIR}/docker/*.sh \
    && npm install -g pm2 \
    && npm install -g pnpm \
    && rm -rf /root/.npm \
    && pnpm install \
    && pnpm build \
    && pnpm build-back \
    && rm -rf node_modules \
    && pnpm install --prod \
    && rm -rf /root/.pnpm-store \
    && npm install  canvas  --build-from-source \
    && npm i -S png-js \
    && npm i -g cnpm \
    && cnpm i \
    && cnpm i -g typescript  \
    && cnpm i -g ts-node \
    && cnpm i -g axios \
    && cnpm i -g  date-fns \
    && cnpm i -g tslib \
    && cnpm i -g fs \    
    && pip3 install requests 
ENTRYPOINT ["./docker/docker-entrypoint.sh"]
