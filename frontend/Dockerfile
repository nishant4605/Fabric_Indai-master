FROM node:23-slim

WORKDIR /app

RUN npm install -g npm@latest

COPY package*.json ./
RUN npm install

COPY . .

# Build the Vite React app
RUN npm run build

# Install 'serve' to serve the build folder
RUN npm install -g serve

EXPOSE 3000
CMD ["serve", "-s", "dist", "-l", "3000"]
