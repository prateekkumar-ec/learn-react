FROM node:18
WORKDIR /app
COPY package.json tsconfig.json ./
RUN npm install
COPY . .
RUN npm run build
CMD ["sh", "-c", "npm run dev"]
EXPOSE 5001
