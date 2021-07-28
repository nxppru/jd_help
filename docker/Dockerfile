FROM node:lts-alpine
LABEL maintainer="whyour"
ARG QL_URL=https://github.com/nxppru/jd_help.git
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin \
    LANG=zh_CN.UTF+8 \
    SHELL=/bin/bash \
    PS1="\u@\h:\w \$ " \
    QL_BRANCH=dev \
    QL_DIR=/ql
WORKDIR ${QL_DIR}
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && apk update -f \
    && apk upgrade \
    && apk --no-cache add -f bash coreutils moreutils git curl wget tzdata perl openssl nginx python3 jq openssh libc6-compat build-base g++ cairo-dev pango-dev giflib-dev \
    && rm -rf /var/cache/apk/* \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && touch ~/.bashrc \
    && mkdir /run/nginx \
    && git clone -b ${QL_BRANCH} ${QL_URL} ${QL_DIR} \
    && cd ${QL_DIR} \
    && cp -f .env.example .env \
    && chmod 777 ${QL_DIR}/shell/*.sh \
    && chmod 777 ${QL_DIR}/docker/*.sh \
    && npm install -g pm2 \
    && npm install -g cnpm \
    && npm install canvas --build-from-source \
    && cnpm install -g typescript ts-node ts-md5 tslib @types/node axios crypto-js date-fns dotenv download got http-server png-js qrcode-terminal request tough-cookie tslib tunnel ws \  
    && npm install -g pnpm \
    && rm -rf /root/.npm \
    && pnpm install --prod \
    && rm -rf /root/.pnpm-store
ENTRYPOINT ["./docker/docker-entrypoint.sh"]