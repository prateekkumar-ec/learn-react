# Production
# ====== Stage 1: Build Stage ======
FROM node:18 AS builder

WORKDIR /app

# Copy package files and install dependencies
COPY package.json package-lock.json ./
RUN npm install  # Install ALL dependencies (including dev for TypeScript)

# Copy the rest of the application
COPY . .

# Compile TypeScript → JavaScript
RUN npm run build
RUN ls -l /app/dist

# ====== Stage 2: Production Stage ======
FROM node:18

WORKDIR /app

# Copy only necessary files from builder stage
COPY --from=builder /app/package.json /app/package-lock.json ./
RUN npm install --omit=dev  # Install only production dependencies

# Copy the compiled JavaScript files and other necessary files
COPY --from=builder /app/dist ./dist

# Expose backend port
EXPOSE 5001

# Start the compiled JS server
CMD ["node", "dist/server.js"]






# Local
# FROM node:18
# WORKDIR /app
# COPY package.json tsconfig.json ./
# RUN npm install
# COPY . .
# CMD ["sh", "-c", "npm run dev"]
# EXPOSE 5001