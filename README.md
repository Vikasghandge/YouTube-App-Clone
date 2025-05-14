#### YouTube-App-Clone
steps to deploy YouTube Clone 
install first docker 

```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

```



```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```



clone demo image
```
docker pull hello-world
```


add user into docker group

```
usermod -aG docker $USER
```

chnage docker docker sock permisions


```
chmod 666 /var/run/docker.sock
```


now create docker file 

```
# Use Node.js 16 slim as the base image
FROM node:16-slim

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the React app
RUN npm run build

# Expose port 3000 (or the port your app is configured to listen on)
EXPOSE 3000

# Start your Node.js server (assuming it serves the React app)
CMD ["npm", "start"]
```

docker build image 

```
docker build -t YouTube-Clone .
```


deploy container

```
docker run -d --name YouTube-Clone -p 3000:3000 YouTube-Clone
```









