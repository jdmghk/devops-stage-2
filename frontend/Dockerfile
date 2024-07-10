FROM node:18-alpine

WORKDIR /app
COPY . /app

RUN npm ci
RUN npm run build

EXPOSE 5173

CMD ["npm", "run", "dev", "--", "--host", "0.0.0.0"]
# CMD npm run preview