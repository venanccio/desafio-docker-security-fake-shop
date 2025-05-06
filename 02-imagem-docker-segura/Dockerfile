FROM node:20-alpine
RUN npm install -g npm@latest
RUN addgroup -S appuser && adduser -S -G appuser -h /home/appuser -s /sbin/nologin appuser
WORKDIR /app
COPY package*.json ./
RUN npm install --only=production && npm cache clean --force
COPY . .
RUN chown -R appuser:appuser /app
USER appuser
EXPOSE 8080
CMD ["node", "server.js"]
