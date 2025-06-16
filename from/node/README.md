# From Node

> [!NOTE]
> **Specify the Node.js version explicitly** to **significantly** reduce the final image size.

Example

```dockerfile
# Build stage
FROM node:latest AS builder

WORKDIR /app

# Copy only package.json to optimize caching
COPY package*.json ./
RUN npm ci

# Copy the remaining application files
COPY . .

# Run stage
FROM node:latest AS final

WORKDIR /app

# Copy only necessary files from the builder stage
COPY --from=builder /app/dist ./dist

# Optional: Expose the port for external access
EXPOSE 3000

CMD ["npm", "start"]
```

> [!IMPORTANT]
> `npm install`: Build stage vs Run stage
>
> Whether to install dependencies in the build stage or run stage depends on the nature of node_modules:
> - If your `node_modules` depend on machine-native APIs (e.g., `esbuild`, `sqlite`), they should be installed in the run stage to match the runtime environment. However, if you can specify the Linux distribution and ensure both stages use the same environment, then it's best to install them in the build stage and copy `node_modules` to the run stage.
>
>   ```dockerfile
>   FROM --platform=linux/amd64 node:latest AS builder
>   # ...
>   # ...
>   FROM --platform=linux/amd64 node:latest AS final
>   ```
>
> - If your dependencies are purely JavaScript-based, installing in the build stage and copying the node_modules to the run stage reduces image size significantly.
>
