# Production
# ====== Stage 1: Build Stage ======
FROM node:18 AS builder

WORKDIR /app

# Copy package files and install dependencies
COPY package.json package-lock.json ./
RUN npm ci
# Copy the rest of the application
COPY . .

# Compile TypeScript → JavaScript
RUN npm run build

# ====== Stage 2: Production Stage ======
FROM node:18

WORKDIR /app

# Copy only necessary files from builder stage
COPY --from=builder /app/package.json /app/package-lock.json ./
COPY --from=builder /app/dist ./dist

# Reinstall only production dependencies
RUN npm ci --omit=dev  

# Expose backend port
EXPOSE 5000

# Start the compiled JS server
CMD ["node", "dist/server.js"]