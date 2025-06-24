# 🛠️ Hands-On 3: Express JS Web App 🌐

This project demonstrates how to create a simple **Hello World Express.js** application and containerize it using **Docker**.

## 📦 Step 1: Create the Express.js App

1. **Create a new folder and navigate into it:**

   ```bash
   mkdir my-express-app
   cd my-express-app

2. **Initialize a Node.js project:**

   ```bash
   npm init -y
   ```

   > The `-y` flag automatically answers all prompts and creates a default `package.json` file.

3. **Install Express.js:**

   ```bash
   npm install express
   ```

4. **Create the main app file:**

   ```bash
   touch app.js
   ```

   Insert the following sample code:

   ```js
   const express = require("express");
   const app = express();

   app.get("/", function (req, res) {
   return res.send("Hello World");
   });

   app.listen(3000, function () {
   console.log("Listening on port 3000");
   });
   ```


## 🧪 Optional: Run Locally for Testing

1. **Install dependencies (if not already):**

   ```bash
   npm install
   ```

2. **Run the app:**

   ```bash
   node app.js
   ```

3. **Visit in browser:**

   ```
   http://localhost:3000/
   ```

## 🐳 Step 2: Containerize the App Using Docker

1. **Create a `Dockerfile` in the project root with the following:**

   ```dockerfile
   # Base image
   FROM node

   # Set working directory
   WORKDIR /app

   # Copy dependency info into working directory
   COPY my-express-app/package.json /app

   # Install dependencies
   RUN npm install

   # Copy rest of the app
   COPY my-express-app /app

   # Start the app
   CMD ["node", "app.js"]
   ```

## 🛠️ Step 3: Build and Run the Docker Container

1. **Build the Docker image:**

   ```bash
   docker build -t node-application .
   ```

2. **Run the container:**

   ```bash
   docker run -it -p 9000:3000 node-application
   ```

   > Here, the app listens on port **3000** inside the container, and it's mapped to port **9000** on your host machine.
   > So visiting `http://localhost:9000/` will access the Express app inside the container.

## ✅ Result

You should see:

```
Hello, World!
```

when visiting:

```
http://localhost:9000/
```

## 🧹 To Stop and Clean Up

* Press `Ctrl + C` to stop the container.
* Optionally remove it:

  ```bash
  docker ps   # get CONTAINERS running currently
  docker stop <CONTAINER_ID>
  ```

