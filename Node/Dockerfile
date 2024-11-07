# Step 1: Use an official Node.js runtime as the base image
FROM node

# Step 2: Set the working directory inside the container
WORKDIR /usr/src/app

# Step 3: Copy the package.json and package-lock.json files to the container
COPY package*.json ./

# Step 4: Install dependencies
RUN npm install

# Step 5: Copy the application source code to the container
COPY . .

# Step 6: Expose the port the app will run on
EXPOSE 3000

# Step 7: Define the command to run the application
CMD ["npm", "start"]
