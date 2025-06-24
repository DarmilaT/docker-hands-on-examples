FROM node
WORKDIR /app
COPY my-express-app/package.json /app
RUN npm install
COPY my-express-app /app
CMD ["node", "app.js"]