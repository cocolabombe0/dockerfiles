FROM xataz/node:latest
MAINTAINER xataz <https://github.com/xataz/>

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

ONBUILD COPY . /usr/src/app/
ONBUILD RUN PKG_BUILD="git make gcc g++ python linux-headers" && \
	apk add --update ${PKG_BUILD} && \
	if [ -e /usr/src/app/package.json ]; then \
		npm install; \
	fi && if [ -e /usr/src/app/bower.js ]; then \
		npm install -g bower; \
	fi && if [ -e /usr/src/app/gulpfile.js ]; then \
		npm install -g gulp && gulp; \
	fi && if [ -e /usr/src/app/Gruntfile.js ]; then \
		npm install -g grunt && grunt; \
	fi && \
	npm cache clean /root/.npm && apk del ${PKG_BUILD} && rm -rf /var/cache/apk/*

CMD ["npm","start"]
