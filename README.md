# Task-dv9
Docker basics 
#!/bin/bash

echo "========== DEVOPS TASK 9 =========="
echo "Docker Basics - Containerizing App"
echo "===================================="

echo ""
echo "1️⃣ Checking Docker Installation..."
docker --version

echo ""
echo "2️⃣ Creating Project Folder..."
mkdir docker-task9
cd docker-task9

echo ""
echo "3️⃣ Creating Simple Node App..."
cat <<EOF > app.js
const http = require("http");

const server = http.createServer((req, res) => {
  res.writeHead(200, { "Content-Type": "text/plain" });
  res.end("Docker Container is Running 🚀\n");
});

server.listen(3000, () => {
  console.log("Server running on port 3000");
});
EOF

echo ""
echo "4️⃣ Creating package.json..."
cat <<EOF > package.json
{
  "name": "docker-demo",
  "version": "1.0.0",
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  }
}
EOF

echo ""
echo "5️⃣ Creating Dockerfile..."
cat <<EOF > Dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
EOF

echo ""
echo "6️⃣ Building Docker Image..."
docker build -t docker-task9-app .

echo ""
echo "7️⃣ Running Container..."
docker run -d -p 3000:3000 --name mycontainer
