FROM node:16.18

ENV PORT=3000

COPY . /frontend-react-js
COPY script-npm.sh /
WORKDIR /frontend-react-js
RUN npm install
RUN chmod +x /script-npm.sh
EXPOSE ${PORT}
CMD ["/script-npm.sh"]